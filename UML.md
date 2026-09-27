# MVP UML Diyagramları

Bu doküman LibreUniversity MVP kapsamı için ilk UML taslağını içerir. Diyagramlar geliştirme başlamadan önce sınırları netleştirmek, topluluk tartışmasını kolaylaştırmak ve ilk mimari kararları görünür yapmak için hazırlanmıştır.

## MVP Use Case Diyagramı

```mermaid
flowchart LR
    Student["Öğrenci"]
    Instructor["Akademisyen"]
    Advisor["Danışman"]
    Admin["İdari Kullanıcı"]
    SysAdmin["Sistem Yöneticisi"]

    subgraph Platform["LibreUniversity MVP"]
        UCLogin["Sisteme giriş yap"]
        UCProfile["Profil ve rol bilgilerini görüntüle"]
        UCCatalog["Ders kataloğunu görüntüle"]
        UCEnroll["Ders seçimi yap"]
        UCApprove["Ders kaydını onayla"]
        UCGrade["Not girişi yap"]
        UCMaterial["Ders materyali paylaş"]
        UCAssignment["Ödev teslim et"]
        UCMeeting["Canlı ders oturumu aç"]
        UCAudit["Denetim kayıtlarını incele"]
        UCManage["Kullanıcı, rol ve birim yönet"]
    end

    Student --> UCLogin
    Student --> UCProfile
    Student --> UCCatalog
    Student --> UCEnroll
    Student --> UCAssignment

    Instructor --> UCLogin
    Instructor --> UCMaterial
    Instructor --> UCGrade
    Instructor --> UCMeeting

    Advisor --> UCApprove

    Admin --> UCManage
    Admin --> UCCatalog

    SysAdmin --> UCManage
    SysAdmin --> UCAudit
```

## MVP Component Diyagramı

```mermaid
flowchart TB
    Web["Web Arayüzü"]
    Mobile["Mobil/Self-Servis Arayüzü"]

    Gateway["API Gateway / Backend Giriş Katmanı"]
    Auth["Kimlik ve Yetki Çekirdeği"]
    Academic["Akademik Çekirdek"]
    OBS["OBS MVP Modülü"]
    LMS["LMS MVP Modülü"]
    Audit["Audit Log"]
    Notify["Bildirim Servisi"]
    Files["Dosya ve Medya Depolama"]
    Reports["Basit Raporlama"]

    DB[(PostgreSQL)]
    ObjectStore[(MinIO / S3 Uyumlu Nesne Depolama)]
    Queue[(Mesaj Kuyruğu)]
    Jitsi["Jitsi/Jibri Adapter"]

    Web --> Gateway
    Mobile --> Gateway

    Gateway --> Auth
    Gateway --> Academic
    Gateway --> OBS
    Gateway --> LMS
    Gateway --> Reports

    Auth --> DB
    Academic --> DB
    OBS --> DB
    LMS --> DB
    Audit --> DB
    Reports --> DB

    OBS --> Audit
    LMS --> Audit
    Auth --> Audit

    OBS --> Notify
    LMS --> Notify
    Notify --> Queue

    LMS --> Files
    Files --> ObjectStore
    LMS --> Jitsi
    Jitsi --> ObjectStore
```

## MVP Deployment Diyagramı

```mermaid
flowchart TB
    Users["Kullanıcılar"]

    subgraph UniversityNetwork["Üniversite Kontrolündeki Altyapı"]
        LB["Reverse Proxy / Load Balancer"]

        subgraph AppNode["Uygulama Sunucuları"]
            WebApp["Web UI"]
            ApiApp["Backend/API"]
            Worker["Arka Plan İşçileri"]
        end

        subgraph CoreServices["Çekirdek Servisler"]
            SSO["SSO / Kimlik Servisi"]
            Queue["Mesaj Kuyruğu"]
            Monitoring["Prometheus/Grafana/Loki"]
        end

        subgraph DataLayer["Veri Katmanı"]
            Postgres[(PostgreSQL)]
            MinIO[(MinIO)]
            Backup["Yedekleme Alanı"]
        end

        subgraph VideoLayer["Canlı Ders Katmanı"]
            Jitsi["Jitsi Meet"]
            JVB["Jitsi Videobridge"]
            Jibri["Jibri Kayıt İşçisi"]
        end
    end

    Users --> LB
    LB --> WebApp
    LB --> ApiApp

    ApiApp --> SSO
    ApiApp --> Postgres
    ApiApp --> Queue
    ApiApp --> MinIO
    Worker --> Queue
    Worker --> Postgres
    Worker --> MinIO

    WebApp --> Jitsi
    Jitsi --> JVB
    Jibri --> MinIO

    Postgres --> Backup
    MinIO --> Backup
    ApiApp --> Monitoring
    Worker --> Monitoring
```

## Ders Kaydı Sequence Diyagramı

```mermaid
sequenceDiagram
    actor Student as Öğrenci
    participant Web as Web/Mobil Arayüz
    participant API as API Katmanı
    participant Auth as Kimlik ve Yetki
    participant OBS as OBS Modülü
    participant Academic as Akademik Çekirdek
    participant Audit as Audit Log
    participant Notify as Bildirim

    Student->>Web: Ders seçimini gönderir
    Web->>API: Ders kayıt isteği
    API->>Auth: Kullanıcı ve yetki doğrula
    Auth-->>API: Rol ve kapsam bilgisi
    API->>OBS: Kayıt kural kontrolü başlat
    OBS->>Academic: Kontenjan, çakışma, ön koşul, dönem kontrolü
    Academic-->>OBS: Uygunluk sonucu
    OBS->>OBS: Kayıt taslağı oluştur
    OBS->>Audit: İşlemi kaydet
    OBS->>Notify: Danışmana onay bildirimi gönder
    OBS-->>API: Kayıt danışman onayında
    API-->>Web: Durum bilgisini döndür
    Web-->>Student: Başvuru durumunu gösterir
```

## Not Girişi Sequence Diyagramı

```mermaid
sequenceDiagram
    actor Instructor as Akademisyen
    participant Web as Web Arayüzü
    participant API as API Katmanı
    participant Auth as Kimlik ve Yetki
    participant OBS as OBS Modülü
    participant Academic as Akademik Çekirdek
    participant Audit as Audit Log
    participant Notify as Bildirim

    Instructor->>Web: Notları girer
    Web->>API: Not kaydetme isteği
    API->>Auth: Ders ve şube yetkisini doğrula
    Auth-->>API: Yetki sonucu
    API->>OBS: Notları doğrula ve kaydet
    OBS->>Academic: Değerlendirme kuralını getir
    Academic-->>OBS: Not hesaplama kuralı
    OBS->>OBS: Harf notu/başarı durumu hesapla
    OBS->>Audit: Not girişini kaydet
    OBS->>Notify: Öğrenciye not bildirimi hazırla
    OBS-->>API: Kayıt sonucu
    API-->>Web: Başarı yanıtı
```

## Canlı Ders Sequence Diyagramı

```mermaid
sequenceDiagram
    actor Instructor as Akademisyen
    actor Student as Öğrenci
    participant LMS as LMS Modülü
    participant Auth as Kimlik ve Yetki
    participant Jitsi as Jitsi Adapter
    participant Store as Nesne Depolama
    participant Audit as Audit Log

    Instructor->>LMS: Canlı ders başlatır
    LMS->>Auth: Moderatör yetkisini doğrula
    Auth-->>LMS: JWT/rol bilgisi
    LMS->>Jitsi: Oda oluştur ve moderatör token üret
    Jitsi-->>LMS: Oda bağlantısı
    LMS->>Audit: Canlı ders başlatma kaydı
    LMS-->>Instructor: Odayı aç

    Student->>LMS: Derse katılmak ister
    LMS->>Auth: Katılım yetkisini doğrula
    Auth-->>LMS: Katılımcı token bilgisi
    LMS-->>Student: Jitsi oda bağlantısı

    Jitsi->>Store: Ders kaydını aktar
    Store-->>LMS: Kayıt dosyası bilgisi
    LMS->>Audit: Kayıt ders haftasına bağlandı
```

## Açık Noktalar

- Kimlik sistemi doğrudan Keycloak ile mi başlayacak, yoksa daha ince bir kimlik çekirdeği mi yazılacak?
- MVP modüler monolith olarak mı başlayacak, yoksa SSO/OBS/LMS ayrı servisler mi olacak?
- Mobil uygulama ilk aşamada responsive web olarak mı ele alınacak?
- Ders kayıt kuyruğu MVP'de gerçek kuyruk sistemiyle mi, yoksa basitleştirilmiş işlem modeliyle mi gösterilecek?
- Jitsi kayıt/VOD pipeline ilk MVP'de tam çalışacak mı, yoksa adapter sınırıyla mı bırakılacak?

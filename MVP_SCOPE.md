# MVP Kapsamı

LibreUniversity çok geniş bir projedir. İlk sürümde her şeyi yapmak yerine, diğer modüllerin üzerine kurulacağı sağlam ve özgür bir çekirdek oluşturmak gerekir.

## MVP Hedefi

İlk MVP'nin hedefi, üniversitenin temel kullanıcı, yetki, akademik yapı ve birkaç kritik öğrenci iş akışını uçtan uca gösterebilen self-hosted bir çekirdek platform sunmaktır.

## MVP'ye Dahil Modüller

### 1. Kimlik ve Yetki Çekirdeği

- Kullanıcı yönetimi.
- Rol ve izin yönetimi.
- Birim bazlı yetkilendirme.
- SSO entegrasyon altyapısı.
- MFA desteği için mimari hazırlık.

### 2. Temel Üniversite Veri Modeli

- Üniversite.
- Fakülte/enstitü/yüksekokul.
- Bölüm/program.
- Akademik dönem.
- Ders.
- Şube.
- Öğrenci.
- Akademisyen.
- İdari kullanıcı.

### 3. OBS Çekirdeği

- Öğrenci kaydı.
- Ders katalog yönetimi.
- Müfredat tanımı.
- Ders açma.
- Ders seçme prototipi.
- Danışman onayı prototipi.
- Not girişi prototipi.

### 4. LMS Çekirdeği

- Ders sayfası.
- Haftalık izlence.
- Materyal paylaşımı.
- Duyuru.
- Basit ödev teslimi.
- Jitsi canlı ders bağlantısı.

### 5. Audit Log ve Gözlemlenebilirlik

- Kritik işlemler için denetim izi.
- Kullanıcı giriş/çıkış kayıtları.
- Not, ders kayıt ve yetki değişikliği logları.
- Temel metrik ve sağlık kontrolleri.

### 6. Self-Hosted Kurulum

- Geliştirici ortamı.
- Test ortamı.
- Üretime yakın örnek kurulum.
- Veritabanı migration altyapısı.
- Yedekleme ve geri dönüş taslağı.

## MVP'ye Dahil Olmayanlar

İlk MVP'de aşağıdakiler tam kapsamlı geliştirilmeyecektir:

- Hastane yönetimi.
- Teknopark yönetimi.
- Gelişmiş ERP.
- Tam EBYS.
- Tam ödeme sistemi.
- Tam yurt/yemekhane/kampüs kartı.
- GIS ve dijital ikiz.
- Gelişmiş BI.
- Gelişmiş online sınav güvenliği.

Bu modüller için yalnızca mimari sınırlar ve entegrasyon noktaları belgelenebilir.

## MVP Başarı Kriterleri

- Sistem self-hosted olarak kurulabilir.
- Kaynak kod ve kurulum adımları açıktır.
- Öğrenci, akademisyen ve yönetici rolleriyle temel akışlar denenebilir.
- Ders açma, ders seçme, danışman onayı ve not girişi prototipleri çalışır.
- Audit log kritik işlemleri kaydeder.
- Kapalı kaynak kritik bağımlılık bulunmaz.
- Yeni katkıcılar geliştirme ortamını dokümantasyonla ayağa kaldırabilir.

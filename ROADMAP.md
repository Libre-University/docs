# Yol Haritası

Bu yol haritası, LibreUniversity'nin fikir aşamasından çalışan özgür yazılım ekosistemine dönüşmesi için önerilen fazları tanımlar. Proje `libre-university` GitHub organizasyonu altında katmanlara göre ayrılmış repolarda geliştirilir ([ADR-0009](docs/adr/0009-organize-repositories-by-layer.md)); iş modülleri ayrı `module-*` repolarında paket olarak geliştirilir ([ADR-0010](docs/adr/0010-develop-modules-as-separate-packages.md)). Her reponun kendi `ROADMAP.md` dosyası bu fazlarla hizalıdır.

## Repolar ve Faz Sorumlulukları

| Repo | Faz 0 | Faz 1 | Faz 2 | Faz 3 | Faz 4+ |
| --- | --- | --- | --- | --- | --- |
| `.github` | Profil, şablonlar | Etiket/süreç iyileştirme | | | |
| `docs` | ADR, gereksinimler | API ve modül sözleşmeleri | Akademik süreç belgeleri | Kullanıcı kılavuzları | Kurumsal modül analizleri |
| `platform-api` | Çekirdek iskelet, modül yükleme, modül şablonu, CI | Kimlik, yetki, audit, bildirim, dosya, temel veri | Çekirdek arayüz iyileştirmeleri | Push bildirim, mobil API | KVKK süreçleri |
| `module-obs` | Modül iskeleti, iş kuralı kabul kriterleri | Öğrenci ve müfredat modelleri | Ders açma, kayıt, danışman onayı, not | Transkript/belge | Staj, mezuniyet |
| `module-lms` | Modül iskeleti, iş kuralı kabul kriterleri | — | Ders sayfası ve materyal temeli | Duyuru, ödev, Jitsi canlı ders | Online sınav, VOD |
| `platform-web` | İskelet, CI | Giriş, yönetim paneli | OBS ekranları | LMS ekranları, self-servis | Kurumsal ekranlar |
| `mobile` | — | — | Prototip | Mobil self-servis 1.0 | Dijital kampüs kartı |
| `adapters` | `libre-ports` taslağı | OIDC, S3, SMTP | | Jitsi, push | Banka, e-Devlet, YÖKSİS |
| `deploy` | Compose geliştirme ortamı | Test/üretime yakın kurulum | Yedekleme | Jitsi yığını | Helm, HA |
| `design-system` | İlkeler, tokenlar | Temel bileşenler | Form/tablo bileşenleri | Mobil uyarlama | |
| `website` | Tanıtım sitesi | Doküman yayını | Demo ortamı | | |

## Gelecek Modül Repoları

MODULES.md'deki diğer modüller için repolar fazı yaklaştıkça açılır ([ADR-0010](docs/adr/0010-develop-modules-as-separate-packages.md)):

- **Faz 4:** `module-cms`, `module-erp`, `module-campus-life`, `module-library`, `module-helpdesk`, `module-bi`
- **Faz 5:** `module-research`, `module-security-ops`, `module-quality`, `module-international`, `module-continuing-education`, `module-career`, `module-hospital`, `module-legal`, `module-gis`, `module-accessibility`, `module-print`, `module-events`, `module-technopark`, `module-real-estate`, `module-fleet`, `module-ohs`, `module-archive`

## Faz 0 Kapanış: Geliştirici Davetinden Önce

Aşağıdakiler tamamlanmadan dış katkıcı çağrısı yapılmamalıdır:

- [ ] Lisans kararının kesinleştirilmesi ([ADR-0002](docs/adr/0002-prefer-agpl-3-or-later-license.md)) ve tüm repolara `LICENSE` eklenmesi.
- [ ] ADR-0004, 0005, 0006, 0008, 0009, 0010'un kabul edilmesi.
- [ ] Organizasyon repolarının açılması ve her repoda `README.md` + `ROADMAP.md`.
- [ ] `.github` reposunda varsayılan katkı rehberi, davranış kuralları, güvenlik politikası ve şablonlar.
- [ ] Ortak etiket seti ([`org-labels.yml`](org-labels.yml): `good first issue`, `help wanted`, `type:*`, `area:*`, `module:*`, `phase:*`, `priority:*`, `kvkk`).
- [ ] `platform-api` ve `platform-web` iskeletlerinin CI ile yeşil olması.
- [ ] `deploy` ile tek komutla çalışan geliştirme ortamı.
- [ ] Her repoda en az 5 adet `good first issue`.
- [ ] İletişim kanalının (Matrix/Discourse gibi özgür bir platform) açılması.

## Faz 0: Topluluk ve Analiz

Amaç: Koddan önce yönü, ilkeleri ve katkı kültürünü netleştirmek.

- Proje vizyonunu yazmak.
- Katkı rehberi ve davranış kurallarını oluşturmak.
- Açık kaynak ve bağımlılık politikasını belirlemek.
- Modül listesini netleştirmek.
- Fonksiyonel ve fonksiyonel olmayan gereksinimleri yazmak.
- MVP kapsamını belirlemek.
- İlk mimari kararları belgelemek.

## Faz 1: Çekirdek Platform MVP

Amaç: Diğer modüllerin üzerine kurulacağı güvenilir çekirdeği oluşturmak.

- Kimlik ve SSO.
- Rol ve yetki yönetimi.
- Kullanıcı, kurum, birim ve dönem temel verileri.
- API Gateway veya servis giriş katmanı.
- Audit log.
- Bildirim altyapısı.
- Temel yönetim paneli.
- Geliştirici ortamı ve self-hosted kurulum.

## Faz 2: İlk Akademik İş Akışları

Amaç: Üniversitenin en temel akademik süreçlerini çalışır hale getirmek.

- Öğrenci temel kayıtları.
- Program, bölüm, ders ve müfredat yönetimi.
- Ders açma ve şube yönetimi.
- Ders kayıt prototipi.
- Not girişi prototipi.
- Öğrenci belgesi/transkript taslak üretimi.

## Faz 3: LMS ve Mobil Self-Servis

Amaç: Öğrenci ve akademisyenin günlük kullanım yüzünü oluşturmak.

- Ders sayfası.
- Materyal paylaşımı.
- Duyuru ve forum.
- Ödev teslimi.
- Jitsi canlı ders entegrasyonu.
- Mobil/web self-servis ana sayfa.
- Bildirim merkezi.

## Faz 4: Kurumsal Süreçler

Amaç: Üniversite yönetiminin idari ve operasyonel ihtiyaçlarını kapsamak.

- EBYS entegrasyon modeli.
- Finans ve ödeme adapterleri.
- Yurt, yemekhane ve kampüs kartı süreçleri.
- Destek masası.
- Kütüphane temel entegrasyonları.
- Raporlama ve BI temeli.

## Faz 5: Genişleme Modülleri

Amaç: Araştırma, kalite, uluslararası ilişkiler, kariyer, GIS, hastane ve teknokent gibi geniş modülleri topluluk katkısıyla geliştirmek.

- Araştırma ve BAP.
- Kalite ve akreditasyon.
- Değişim programları.
- Kariyer merkezi.
- Kampüs GIS.
- Engelsiz üniversite.
- HBYS entegrasyon sınırları.
- Teknokent yönetimi.

## Sürekli İşler

- Güvenlik testleri.
- Erişilebilirlik denetimleri.
- Dokümantasyon güncellemeleri.
- Bağımlılık lisans denetimi.
- Performans ve yük testleri.
- Topluluk toplantıları ve karar kayıtları.

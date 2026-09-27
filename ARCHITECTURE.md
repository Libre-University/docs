# Mimari Taslak

Bu doküman, geliştirme başlamadan önce LibreUniversity için önerilen üst seviye mimari yaklaşımı özetler. Ayrıntılı mimari kararlar [docs/adr/](docs/adr/) altında karar kayıtlarıyla belgelenecektir.

## Mimari Hedefler

- Self-hosted kurulabilirlik.
- Kapalı kaynak kritik bağımlılık kullanmama.
- Modüler geliştirme.
- Açık API sözleşmeleri.
- Merkezi kimlik ve yetki yönetimi.
- Güçlü audit log.
- Dış sistemleri adapter katmanında izole etme.
- Üniversiteler arası uyarlanabilirlik.

## Önerilen Başlangıç Yaklaşımı

İlk MVP için modüler monolith veya iyi sınırlandırılmış servis modülleri tercih edilebilir. Çok erken mikroservisleşme operasyon yükünü artırabilir.

Başlangıçta önemli olan:

- Modül sınırlarını doğru çizmek.
- Veri sahipliğini netleştirmek.
- API sözleşmelerini belgelemek.
- Audit ve yetkilendirmeyi çekirdeğe yerleştirmek.
- İleride ayrıştırılabilecek bir yapı kurmak.

## Ana Katmanlar

- **Kimlik ve Yetki:** Kullanıcı, rol, izin, SSO, MFA hazırlığı.
- **Çekirdek Akademik Veri:** Öğrenci, akademisyen, birim, program, ders, dönem.
- **İş Modülleri:** OBS, LMS, CMS, ERP, kütüphane, yurt, yemekhane, destek.
- **Entegrasyon Katmanı:** Kamu, banka, e-imza, KEP, sağlık, dış veri kaynakları.
- **Bildirim Katmanı:** E-posta, SMS, push, acil durum duyuruları.
- **Dosya ve Medya:** Belge, ders materyali, video, OCR çıktıları.
- **Audit ve Gözlemlenebilirlik:** Log, metrik, izleme, SIEM aktarımı.
- **Raporlama:** Veri ambarı, KPI, kalite ve yönetim panelleri.

## Dış Sistem Yaklaşımı

Dış sistemler çekirdek iş kurallarına gömülmez. Her dış sistem için adapter yaklaşımı kullanılır.

Örnek:

- Banka adapteri.
- e-Devlet adapteri.
- YÖKSİS adapteri.
- ÖSYM adapteri.
- KEP/e-imza adapteri.
- Medula/e-Nabız adapteri.

Bu sayede sağlayıcı değişse bile çekirdek modüller bozulmaz.

## Veri Sahipliği

Her ana veri türü için kaynak sistem belirlenmelidir.

Örnek:

- Öğrenci akademik kaydı: OBS.
- Ders materyali: LMS.
- Kullanıcı kimliği: Kimlik çekirdeği/SSO.
- Resmi belge: EBYS veya belge modülü.
- Ödeme hareketi: Finans modülü.
- Audit log: Denetim çekirdeği.

## Güvenlik

Yetki kontrolleri yalnızca arayüzde değil, sunucu tarafında uygulanmalıdır. Kritik işlemler audit log'a yazılmalıdır.

Özellikle şu işlemler yüksek hassasiyetlidir:

- Not değişikliği.
- Ders kayıt onayı.
- Belge üretimi.
- Ödeme iadesi.
- Yetki değişikliği.
- Sağlık/disiplin/hukuk verisine erişim.

## Karar Durumu

Geliştirme öncesi açık sorular aşağıdaki ADR'lerle yanıtlanmıştır:

| Soru | Karar | ADR |
| --- | --- | --- |
| Modüler monolith mi, servisler mi? | MVP modüler monolith | [ADR-0004](docs/adr/0004-start-with-modular-monolith-for-mvp.md) |
| Ana veritabanı? | PostgreSQL | [ADR-0005](docs/adr/0005-use-postgresql-as-primary-database.md) |
| Kimlik sistemi? | OIDC/SAML, Keycloak birincil aday, adapter üzerinden | [ADR-0006](docs/adr/0006-use-open-identity-provider-adapter.md) |
| Uygulama dili ve framework? | Python/Django + React/TypeScript | [ADR-0008](docs/adr/0008-use-python-django-and-react.md) |
| Repo yapısı? | Katmanlara göre ayrılmış repolar | [ADR-0009](docs/adr/0009-organize-repositories-by-layer.md) |
| Modüller nerede geliştirilecek? | Her modül ayrı `module-*` reposunda paket; tek uygulama olarak dağıtım | [ADR-0010](docs/adr/0010-develop-modules-as-separate-packages.md) |
| İlk UI web mi, mobil mi? | Önce responsive web; mobil uygulama Faz 3'te | [ADR-0008](docs/adr/0008-use-python-django-and-react.md) |

Yeni sorular ortaya çıktıkça yeni ADR önerisiyle tartışılmalıdır.

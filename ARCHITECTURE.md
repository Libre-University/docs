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

## Açık Sorular

- İlk uygulama dili ve framework seçimi ne olacak?
- Modüler monolith ile mi başlanacak, yoksa belirli çekirdek servisler ayrılacak mı?
- Ana veritabanı PostgreSQL mi olacak?
- Kimlik sistemi doğrudan Keycloak gibi hazır özgür yazılım üzerinden mi kurulacak?
- İlk UI web odaklı mı, mobil öncelikli mi olacak?

Bu sorular geliştirme başlamadan önce topluluk tartışmasıyla netleştirilmelidir.

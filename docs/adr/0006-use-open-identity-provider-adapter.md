# ADR-0006: Kimlik İçin Açık SSO Sağlayıcı ve Adapter Yaklaşımı Kullanılsın

## Durum

Önerildi

## Bağlam

Üniversite sistemlerinde kimlik doğrulama merkezi olmalıdır. OBS, LMS, CMS, mobil uygulama ve idari modüller aynı kullanıcı kimliğiyle çalışmalıdır. Aynı zamanda proje kapalı kimlik sağlayıcılarına veya belirli bir firmaya bağımlı kalmamalıdır.

Kimlik sistemi güvenlik açısından kritik olduğu için açık, denetlenebilir ve standart protokolleri destekleyen bir yaklaşım gerekir.

## Karar

MVP için kimlik doğrulama katmanı OIDC/SAML gibi açık standartları desteklemelidir. Keycloak gibi özgür yazılım SSO sağlayıcıları birincil aday olarak değerlendirilecektir.

Uygulama çekirdeği doğrudan belirli bir ürüne gömülmemeli; kimlik sağlayıcı ile adapter veya standart protokol katmanı üzerinden konuşmalıdır.

## Sonuçlar

- SSO, MFA ve merkezi oturum yönetimi daha hızlı sağlanabilir.
- Üniversite mevcut LDAP/AD/FreeIPA altyapılarına bağlanabilir.
- Keycloak veya benzeri sistem değiştirilebilir kalır.
- Yetkilendirme modelinin hangi kısmının SSO'da, hangi kısmının uygulamada tutulacağı netleştirilmelidir.

## Değerlendirilen Alternatifler

- **Tüm kimlik sistemini sıfırdan yazmak:** Güvenlik riski ve bakım yükü yüksektir.
- **Kapalı kimlik sağlayıcı kullanmak:** Proje ilkeleriyle uyumsuzdur.
- **Sadece uygulama içi kullanıcı/parola:** Üniversite ölçeğinde SSO ihtiyacını karşılamaz.

## İlgili Dokümanlar

- [ARCHITECTURE.md](../../ARCHITECTURE.md)
- [DATA_MODEL.md](../../DATA_MODEL.md)
- [SECURITY.md](../../SECURITY.md)

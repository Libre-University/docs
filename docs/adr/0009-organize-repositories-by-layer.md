# ADR-0009: Repolar Katmanlara Göre Ayrılsın

## Durum

Önerildi

## Bağlam

Proje `libre-university` GitHub organizasyonu altında geliştirilecektir. Backend, web, mobil, kurulum, entegrasyon, tasarım ve topluluk sitesi farklı yetkinlikte katkıcılar gerektirir. Repo yapısı; katkıcının doğru yere kolayca ulaşmasını, sorumlulukların (CODEOWNERS) netleşmesini ve bağımsız sürümlemeyi desteklemelidir.

## Karar

Kod ve içerik katmanlara göre ayrı repolarda tutulur:

| Repo | Sorumluluk |
| --- | --- |
| `.github` | Organizasyon profili, varsayılan katkı rehberi, davranış kuralları, güvenlik politikası, issue/PR şablonları. |
| `docs` | Vizyon, gereksinimler, mimari, veri modeli, ADR'ler ve ana yol haritası. Mimari kararların tek kaynağı. |
| `platform-api` | Django modüler monolith: kimlik/yetki, akademik çekirdek, OBS, LMS, audit, bildirim, dosya. |
| `platform-web` | React/TypeScript web arayüzü (öğrenci, akademisyen, idari kullanıcı, yönetici). |
| `mobile` | React Native mobil self-servis uygulaması. |
| `adapters` | `libre-ports` arayüz paketi ve dış sistem adapterleri (Keycloak/OIDC, Jitsi, S3/MinIO, SMTP; ileride YÖKSİS, e-Devlet, banka). |
| `deploy` | Docker Compose geliştirme ortamı, üretime yakın kurulum, Helm/Ansible, yedekleme ve gözlemlenebilirlik yığını. |
| `design-system` | Tasarım ilkeleri, Penpot kaynakları, erişilebilir React bileşen kütüphanesi ve Storybook. |
| `website` | Proje tanıtım sitesi ve yayınlanmış dokümantasyon. |

Kurallar:

- `platform-api` backend için tek sürüm birimidir (modüler monolith, [ADR-0004](0004-start-with-modular-monolith-for-mvp.md)); modüller ayrı repoya bölünmez.
- Repolar arası sözleşmeler versiyonlanır: REST API için OpenAPI dosyası (`platform-api`), adapterler için `libre-ports` paketi (`adapters`), UI için `@libre-university/ui` paketi (`design-system`).
- Her repo kendi `README.md` ve `ROADMAP.md` dosyasını tutar; fazlar ve kilometre taşları `docs/ROADMAP.md` ile hizalıdır.
- Mimariyi etkileyen değişiklikler önce `docs` reposunda ADR olarak önerilir.

## Sonuçlar

- Katkıcılar ilgi alanına göre doğrudan ilgili repoya yönlenir.
- Repo başına CI, CODEOWNERS ve sürüm döngüsü bağımsız yönetilir.
- Repolar arası değişiklikler koordinasyon gerektirir; sözleşme versiyonlama disiplini zorunludur.
- Uçtan uca geliştirme ortamı `deploy` reposundaki Docker Compose ile tek komutla ayağa kalkmalıdır.

## Değerlendirilen Alternatifler

- **Tek monorepo:** Koordinasyon kolay, ancak farklı yetkinlikteki katkıcılar için giriş karmaşık ve CI ağır.
- **Modül başına repo (obs, lms, ...):** Modüler monolith kararıyla çelişir; erken mikroservis yükü getirir.

## İlgili Dokümanlar

- [ROADMAP.md](../../ROADMAP.md)
- [ADR-0008](0008-use-python-django-and-react.md)

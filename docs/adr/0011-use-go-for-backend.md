# ADR-0011: Backend Go ile Geliştirilsin

## Durum

Önerildi. [ADR-0008](0008-use-python-django-and-react.md) kararının backend (Python/Django) bölümünün yerini alır; web ve mobil kararları (React/TypeScript, React Native) geçerliliğini korur.

## Bağlam

ADR-0008 backend için Python/Django önermişti. Henüz backend kodu yazılmadan bu karar yeniden değerlendirildi. Belirleyici ihtiyaçlar:

- **Performans:** Ders kayıt dönemlerinde on binlerce öğrencinin aynı anda işlem yapması ([NFR-01, NFR-02](../../NON_FUNCTIONAL_REQUIREMENTS.md)).
- **Kolay kurulum:** Üniversite bilgi işlem ekiplerinin sistemi az bileşenle, kendi sunucularında kurabilmesi ([ADR-0003](0003-self-hosted-first.md)).
- **Ekip yetkinliği:** Çekirdek geliştirici ekibin Go deneyimi.
- **Uzun vadeli bakım:** Kamu kurumu yazılımının 10+ yıl bakımı; statik tipler, geriye uyumluluk, az bağımlılık.

## Karar

**Backend (`platform-api`, `module-*`, `adapters`) Go ile geliştirilir.**

| İhtiyaç | Seçim | Lisans |
| --- | --- | --- |
| Dil | Go (desteklenen son iki sürüm) | BSD-3-Clause |
| HTTP | `net/http` + [chi](https://github.com/go-chi/chi) | MIT |
| API sözleşmesi | OpenAPI 3 önce yazılır; sunucu ve istemci kodu [oapi-codegen](https://github.com/oapi-codegen/oapi-codegen) ile üretilir | Apache-2.0 |
| Veritabanı erişimi | [pgx](https://github.com/jackc/pgx) + [sqlc](https://github.com/sqlc-dev/sqlc) (SQL yazılır, tip güvenli Go kodu üretilir) | MIT |
| Migration | [goose](https://github.com/pressly/goose); her modülün kendi migration dizini | MIT |
| Arka plan işleri ve kuyruk | [River](https://github.com/riverqueue/river) (PostgreSQL üzerinde) | MPL-2.0 |
| Kimlik (OIDC) | [go-oidc](https://github.com/coreos/go-oidc) + `golang.org/x/oauth2` | Apache-2.0 / BSD |
| Log ve metrik | `log/slog` (JSON), Prometheus `client_golang` | BSD / Apache-2.0 |
| Test | `testing`, [testcontainers-go](https://github.com/testcontainers/testcontainers-go) | MIT |
| Kalite | `gofmt`, `go vet`, [golangci-lint](https://github.com/golangci/golangci-lint) | GPL-3.0 (yalnızca geliştirme aracı) |

İlkeler:

- **Modül sınırları derleyiciyle korunur:** Modüllerin iç kodu Go `internal/` paketlerinde tutulur; başka modüller bu kodu içe aktaramaz. Ek kurallar `golangci-lint` `depguard` ile denetlenir.
- **Kuyruk için Redis gerekmez:** Arka plan işleri ve ders kayıt kuyruğu River ile PostgreSQL üzerinde çalışır. Önbellek ihtiyacı doğarsa Valkey (BSD) kullanılır.
- **Tek binary:** Uygulama statik derlenmiş tek bir çalıştırılabilir dosya ve bu dosyayı içeren konteyner imajı olarak dağıtılır.
- **Yönetim ekranları:** Django admin'in karşılığı yoktur; yönetim ekranları `platform-web`'de geliştirilir.
- Modüllerin derleme zamanı yapısı için bkz. [ADR-0010](0010-develop-modules-as-separate-packages.md).

## Sonuçlar

- Yüksek eşzamanlılık ve düşük bellek kullanımı; ders kayıt anları için güçlü temel.
- Kurulum: tek binary + PostgreSQL + Keycloak + nesne depolama. Redis/Celery işçileri yoktur.
- Tip güvenliği SQL'den (sqlc) API'ye (oapi-codegen) kadar uzanır.
- CRUD ağırlıklı işlerde Django'ya göre daha fazla kod yazılır; kod üretimi (sqlc, oapi-codegen) bu yükü azaltır.
- Yönetim paneli sıfırdan yazılır; `platform-web` iş yükü artar.
- Python bilen ama Go bilmeyen katkıcılar için öğrenme eşiği oluşur; katkı rehberlerinde Go'ya giriş kaynakları verilmelidir.

## Değerlendirilen Alternatifler

- **Python/Django (ADR-0008):** Hızlı CRUD geliştirme ve hazır admin; ancak performans, dağıtım karmaşıklığı (Python ortamı, Celery, Redis) ve ekip yetkinliği açısından geride kaldı.
- **Java/Spring:** Olgun, ancak ağır çalışma zamanı ve yüksek bellek kullanımı.
- **TypeScript/NestJS:** Tek dil avantajı; ancak performans ve uzun vadeli bağımlılık yönetimi açısından zayıf.

## İlgili Dokümanlar

- [ADR-0008](0008-use-python-django-and-react.md)
- [ADR-0010](0010-develop-modules-as-separate-packages.md)
- [ARCHITECTURE.md](../../ARCHITECTURE.md)

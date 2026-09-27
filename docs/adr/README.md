# Mimari Karar Kayıtları

Bu klasör LibreUniversity için alınan veya önerilen önemli mimari kararları içerir.

## Durum Anlamları

- **Önerildi:** Topluluk tartışmasına açık, varsayılan yön olarak yazılmış karar.
- **Kabul edildi:** Proje ilkeleri veya mevcut kapsam için benimsenmiş karar.
- **Değiştirildi:** Daha yeni bir ADR tarafından geçersiz kılınmış karar.
- **Reddedildi:** Değerlendirilmiş ancak uygulanmamasına karar verilmiş seçenek.

## Kararlar

| ADR | Başlık | Durum |
| --- | --- | --- |
| [0001](0001-use-adr-for-architecture-decisions.md) | Mimari karar kayıtları kullanılsın | Kabul edildi |
| [0002](0002-prefer-agpl-3-or-later-license.md) | Ana lisans için AGPL-3.0-or-later tercih edilsin | Kabul edildi |
| [0003](0003-self-hosted-first.md) | Self-hosted öncelikli mimari benimsensin | Kabul edildi |
| [0004](0004-start-with-modular-monolith-for-mvp.md) | MVP için modüler monolith ile başlansın | Önerildi |
| [0005](0005-use-postgresql-as-primary-database.md) | Birincil veritabanı PostgreSQL olsun | Önerildi |
| [0006](0006-use-open-identity-provider-adapter.md) | Kimlik için açık SSO sağlayıcı ve adapter yaklaşımı kullanılsın | Önerildi |
| [0007](0007-isolate-external-systems-with-adapters.md) | Dış sistemler adapter katmanında izole edilsin | Kabul edildi |
| [0008](0008-use-python-django-and-react.md) | Python/Django ve React/TypeScript kullanılsın | Kısmen değiştirildi (backend: ADR-0011) |
| [0009](0009-organize-repositories-by-layer.md) | Repolar katmanlara göre ayrılsın | Önerildi (ADR-0010 ile kısmen değiştirildi) |
| [0010](0010-develop-modules-as-separate-packages.md) | Modüller ayrı repolarda, tek uygulamaya derlenen paketler olsun | Önerildi |
| [0011](0011-use-go-for-backend.md) | Backend Go ile geliştirilsin | Önerildi |

## Yeni ADR Yazarken

Yeni dosya adı şu formatı izlemelidir:

`0012-short-decision-title.md`

Her ADR; durum, bağlam, karar, sonuçlar, alternatifler ve ilgili dokümanlar bölümlerini içermelidir.

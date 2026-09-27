# ADR-0005: Birincil Veritabanı PostgreSQL Olsun

## Durum

Önerildi

## Bağlam

MVP; kullanıcı, rol, akademik dönem, ders, şube, ders kayıt, not, LMS materyali, audit log ve bildirim gibi ilişkisel tutarlılığı yüksek veriler içerir. Bu veriler için olgun, özgür yazılım, self-hosted çalışabilen ve güçlü transaction desteği olan bir veritabanı gerekir.

## Karar

LibreUniversity MVP için birincil ilişkisel veritabanı olarak **PostgreSQL** kullanılması önerilir.

## Sonuçlar

- Güçlü transaction ve ilişki modelleme desteği sağlanır.
- Açık kaynak ve yaygın operasyon bilgisi vardır.
- JSONB, full-text search, partitioning ve gelişmiş index özellikleri ileride işe yarar.
- Üniversite bilgi işlem ekipleri tarafından self-hosted işletilebilir.
- Çok büyük audit veya analitik ihtiyaçlarında ileride ek veri depoları gerekebilir.

## Değerlendirilen Alternatifler

- **MariaDB/MySQL:** Olgun ve açık kaynak seçeneklerdir, ancak PostgreSQL akademik ve kurumsal veri modeli için daha güçlü varsayılan tercih olarak değerlendirildi.
- **NoSQL birincil veritabanı:** MVP'nin ilişkisel yapısına uygun değildir.
- **Ticari veritabanları:** Tedarikçi bağımlılığı ve lisans maliyeti nedeniyle proje ilkeleriyle uyumsuzdur.

## İlgili Dokümanlar

- [DATA_MODEL.md](../../DATA_MODEL.md)
- [ARCHITECTURE.md](../../ARCHITECTURE.md)
- [OPEN_SOURCE_POLICY.md](../../OPEN_SOURCE_POLICY.md)

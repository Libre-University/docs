# ADR-0008: Python/Django ve React/TypeScript Kullanılsın

## Durum

Kısmen değiştirildi. Backend bölümünün (Python/Django) yerini [ADR-0011](0011-use-go-for-backend.md) almıştır; web (React/TypeScript) ve mobil (React Native) kararları geçerlidir.

## Bağlam

Geliştiricileri davet etmeden önce uygulama dili ve framework seçimi netleşmelidir. Seçim; modüler monolith yaklaşımını ([ADR-0004](0004-start-with-modular-monolith-for-mvp.md)), PostgreSQL'i ([ADR-0005](0005-use-postgresql-as-primary-database.md)) ve OIDC tabanlı kimliği ([ADR-0006](0006-use-open-identity-provider-adapter.md)) iyi desteklemeli, öğrenci ve akademisyen katkıcılar için öğrenme eşiği düşük olmalı ve tamamen özgür yazılımdan oluşmalıdır.

## Karar

**Backend (`platform-api`):**

- Python 3.12+ ve Django 5.2 LTS.
- Django REST Framework ile REST API; `drf-spectacular` ile OpenAPI 3 sözleşmesi.
- Her iş modülü ayrı bir Django uygulaması (`identity`, `academic`, `obs`, `lms`, `audit`, `notifications`, `files`); modüller arası erişim yalnızca her modülün `services`/`api` katmanı üzerinden.
- Arka plan işleri ve ders kayıt kuyruğu için Celery + Redis (veya Valkey).
- OIDC istemcisi olarak `mozilla-django-oidc`; parola uygulamada tutulmaz.
- Test: `pytest`, `pytest-django`, `factory_boy`. Kalite: `ruff`, `mypy`, `django-upgrade`. Bağımlılık yönetimi: `uv`.

**Web (`platform-web`):**

- React + TypeScript, Vite.
- API istemcisi OpenAPI sözleşmesinden üretilir (`openapi-typescript`); sunucu durumu TanStack Query ile.
- Çok dillilik `i18next` (tr, en). Test: Vitest, Testing Library, Playwright, axe-core.

**Mobil (`mobile`):** React Native + Expo (açık kaynak araçlar). Derleme yerel/CI üzerinde yapılır; kapalı kaynak bulut derleme servislerine zorunlu bağımlılık kurulmaz.

**İlk arayüz:** Önce responsive web; mobil uygulama Faz 3'te.

## Sonuçlar

- Django admin, ORM ve migration altyapısı MVP'yi hızlandırır.
- Python ve React, üniversite öğrencileri arasında yaygın olduğundan katkıcı havuzu geniştir.
- Web ve mobilde aynı dil (TypeScript) kullanıldığı için bileşen ve tip paylaşımı mümkündür.
- Yüksek eşzamanlılık gerektiren ders kayıt anları için kuyruk ve önbellek tasarımına özen gösterilmelidir; gerekirse bu akış ileride ayrı servise çıkarılır.
- Modül sınırlarını korumak için `import-linter` ile otomatik kontrol uygulanır.

## Değerlendirilen Alternatifler

- **Java/Spring + React:** Kurumsal olgunluk yüksek, ancak katkı eşiği ve kurulum ağırlığı fazla.
- **TypeScript/NestJS + React:** Tek dil avantajı var, ancak admin, ORM ve migration ekosistemi Django kadar bütünleşik değil.
- **Go + React:** Performanslı, fakat CRUD ağırlıklı iş uygulamalarında geliştirme maliyeti yüksek.

## İlgili Dokümanlar

- [ARCHITECTURE.md](../../ARCHITECTURE.md)
- [ADR-0009](0009-organize-repositories-by-layer.md)

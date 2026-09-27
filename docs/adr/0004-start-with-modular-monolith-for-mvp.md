# ADR-0004: MVP İçin Modüler Monolith ile Başlansın

## Durum

Önerildi

## Bağlam

LibreUniversity kapsamı çok geniştir. OBS, LMS, kimlik, audit, bildirim, dosya yönetimi ve entegrasyonlar zamanla ayrı servisler haline gelebilir. Ancak geliştirme başlangıcında erken mikroservisleşme dağıtım, gözlemleme, ağ, test ve veri tutarlılığı yükünü artırır.

MVP'nin amacı, çekirdek akademik akışları hızlı ve anlaşılır biçimde doğrulamaktır.

## Karar

MVP geliştirmesine modül sınırları açık olan bir **modüler monolith** yaklaşımıyla başlanması önerilir.

Modüller kod içinde ayrıştırılmalı, veri sahipliği ve API sınırları belgelenmelidir. İleride ihtiyaç duyulan modüller ayrı servise çıkarılabilecek şekilde tasarım yapılmalıdır.

## Sonuçlar

- İlk kurulum ve geliştirme daha basit olur.
- Yeni katkıcılar sistemi daha kolay çalıştırır.
- Transaction yönetimi ve veri tutarlılığı daha anlaşılır kalır.
- Modül sınırları gevşek bırakılırsa ileride ayrıştırma zorlaşabilir.
- Kod organizasyonu ve iç mimari disiplin önemli hale gelir.

## Değerlendirilen Alternatifler

- **Başlangıçtan mikroservis:** Büyük ekip ve olgun operasyon gerektirir.
- **Tek parça düzensiz monolith:** İlk başta hızlı görünür, ancak modül sınırlarını yok eder.
- **Tam plugin mimarisi:** Esnek olabilir, fakat MVP için fazla karmaşıktır.

## İlgili Dokümanlar

- [ARCHITECTURE.md](../../ARCHITECTURE.md)
- [MVP_SCOPE.md](../../MVP_SCOPE.md)
- [DATA_MODEL.md](../../DATA_MODEL.md)

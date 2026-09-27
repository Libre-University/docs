# ADR-0007: Dış Sistemler Adapter Katmanında İzole Edilsin

## Durum

Kabul edildi

## Bağlam

LibreUniversity; YÖKSİS, ÖSYM, e-Devlet, SGK, MERNİS, KEP, e-imza, banka, Medula, UYAP ve benzeri dış sistemlerle entegre olabilir. Bu sistemlerin bazıları kapalı, mevzuata bağlı veya sağlayıcıya özgü olabilir.

Bu entegrasyonların çekirdek iş kurallarına gömülmesi, tedarikçi bağımlılığı ve bakım zorluğu yaratır.

## Karar

Tüm dış sistem entegrasyonları adapter katmanı üzerinden izole edilecektir.

Her adapter:

- Açık bir iç arayüz arkasında çalışır.
- Sağlayıcıya özgü ayrıntıları çekirdek modüllerden saklar.
- Hata yönetimi, tekrar deneme ve mutabakat mekanizması içerir.
- Log ve audit gereksinimlerini karşılar.
- Alternatif sağlayıcıya geçişi mümkün kılar.

## Sonuçlar

- Çekirdek modüller dış sistem değişikliklerinden daha az etkilenir.
- Kapalı servisler mimarinin merkezine yerleşmez.
- Test için mock/fake adapter yazmak kolaylaşır.
- Adapter sözleşmelerinin iyi belgelenmesi gerekir.

## Değerlendirilen Alternatifler

- **Dış servis SDK'larını doğrudan modüllere gömmek:** Hızlı başlatır, ancak uzun vadede bağımlılığı artırır.
- **Tüm entegrasyonları tek büyük servis yapmak:** Merkezi karmaşıklık yaratır.
- **Dış entegrasyonları MVP'de tamamen yok saymak:** Çekirdek tasarımda sınırlar düşünülmezse sonradan zorlaşır.

## İlgili Dokümanlar

- [ARCHITECTURE.md](../../ARCHITECTURE.md)
- [OPEN_SOURCE_POLICY.md](../../OPEN_SOURCE_POLICY.md)
- [FUNCTIONAL_REQUIREMENTS.md](../../FUNCTIONAL_REQUIREMENTS.md)

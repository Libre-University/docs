# ADR-0001: Mimari Karar Kayıtları Kullanılsın

## Durum

Kabul edildi

## Bağlam

LibreUniversity; OBS, LMS, kimlik, audit, entegrasyon, raporlama ve self-hosted altyapı gibi çok sayıda kritik alanı kapsıyor. Proje toplulukla gelişeceği için önemli teknik kararların yalnızca sohbetlerde, issue yorumlarında veya kişisel hafızada kalması sürdürülebilir değildir.

Kararların neden alındığı, hangi seçeneklerin değerlendirildiği ve gelecekte hangi koşullarda değiştirilebileceği açıkça görülebilmelidir.

## Karar

Proje, önemli teknik ve mimari kararlar için `docs/adr/` altında Architecture Decision Record kullanacaktır.

ADR dosyaları şu formatı izler:

- Başlık.
- Durum.
- Bağlam.
- Karar.
- Sonuçlar.
- Değerlendirilen alternatifler.
- İlgili dokümanlar.

## Sonuçlar

- Yeni katkıcılar karar geçmişini okuyabilir.
- Mimari yön değişiklikleri gerekçeli yapılır.
- Topluluk tartışmaları daha sağlıklı yürür.
- Kararlar gerektiğinde yeni ADR ile değiştirilebilir.

## Değerlendirilen Alternatifler

- Kararları yalnızca README veya ARCHITECTURE içinde tutmak.
- Kararları issue yorumlarında bırakmak.
- Karar kaydı tutmamak.

Bu alternatifler uzun vadede izlenebilirlik sağlamadığı için tercih edilmedi.

## İlgili Dokümanlar

- [ARCHITECTURE.md](../../ARCHITECTURE.md)
- [GOVERNANCE.md](../../GOVERNANCE.md)

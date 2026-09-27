# ADR-0003: Self-Hosted Öncelikli Mimari Benimsensin

## Durum

Kabul edildi

## Bağlam

LibreUniversity'nin temel amacı üniversitelerin verisini, kurumsal hafızasını ve dijital işleyişini kapalı kutu sistemlere teslim etmemesidir. Bu hedef için sistemin yalnızca belirli bir firmanın bulutunda veya lisans sunucusunda çalışması kabul edilemez.

Üniversite bilgi işlem ekipleri sistemi kendi veri merkezlerinde veya kendi kontrol ettikleri açık altyapıda çalıştırabilmelidir.

## Karar

LibreUniversity self-hosted öncelikli tasarlanacaktır.

Bu karar şu ilkeleri içerir:

- Kritik bileşenler üniversite kontrolündeki altyapıda çalışabilmelidir.
- Kurulum, yedekleme, geri dönüş ve yükseltme süreçleri belgelenmelidir.
- Dış servisler çekirdek mimariye gömülmemelidir.
- Kapalı kaynak SaaS servisleri kritik işlevlerin zorunlu parçası olamaz.

## Sonuçlar

- Üniversiteler veri egemenliğini korur.
- Operasyon sorumluluğu daha görünür hale gelir.
- Kurulum ve bakım dokümantasyonu kritik hale gelir.
- İlk geliştirme aşamasında deployment otomasyonu erken düşünülmelidir.

## Değerlendirilen Alternatifler

- **SaaS öncelikli mimari:** Operasyon yükünü azaltabilir, ancak proje felsefesiyle çelişir.
- **Sadece container imajı dağıtmak:** Yeterli değildir; kurulum, yedekleme ve işletim belgeleri de gerekir.
- **Bulut sağlayıcıya özgü mimari:** Taşınabilirliği ve tedarikçi bağımsızlığını zayıflatır.

## İlgili Dokümanlar

- [ARCHITECTURE.md](../../ARCHITECTURE.md)
- [MVP_SCOPE.md](../../MVP_SCOPE.md)
- [OPEN_SOURCE_POLICY.md](../../OPEN_SOURCE_POLICY.md)

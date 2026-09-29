# ADR-0002: Ana Lisans İçin AGPL-3.0-or-later Tercih Edilsin

## Durum

Kabul edildi. Yazılım repoları AGPL-3.0-or-later, belge repoları (`docs`, `.github`) CC BY-SA 4.0 ile lisanslanır.

Karar verenler: Kurucu. Tartışma: [docs#1](https://github.com/Libre-University/docs/issues/1). Karar 27 Eylül 2026'da tüm repolara `LICENSE` eklenerek kesinleşti.

## Bağlam

LibreUniversity ağ üzerinden hizmet olarak sunulabilecek bir üniversite bilgi sistemi ekosistemidir. Böyle sistemlerde yazılım kullanıcıya doğrudan dağıtılmadan, web arayüzü üzerinden kullandırılabilir.

Projenin özgür yazılım karakterini korumak için, projeyi alıp değiştirerek kapalı SaaS hizmetine dönüştürmeyi zorlaştıran bir lisans tercih edilmelidir.

## Karar

Projenin ana lisansı **AGPL-3.0-or-later** olacaktır; belge repoları CC BY-SA 4.0 kullanır.

Katkıcı lisans sözleşmesi (CLA) veya DCO gerekip gerekmediği ayrı bir ADR ile ele alınır ([docs#13](https://github.com/Libre-University/docs/issues/13)).

## Sonuçlar

- Ağ üzerinden hizmet olarak sunulan değişikliklerin de özgür kalması teşvik edilir.
- Üniversiteler arası ortak geliştirme korunur.
- Kapalı türev ve tedarikçi kilidi riski azaltılır.
- Bazı ticari aktörler için katkı veya kullanım kararı daha fazla hukuki değerlendirme gerektirebilir.

## Değerlendirilen Alternatifler

- **GPL-3.0-or-later:** Güçlü copyleft sağlar, ancak ağ üzerinden kullanım senaryosunda AGPL kadar koruyucu değildir.
- **EUPL:** Kamu kurumları için anlamlı olabilir; uyumluluk ayrıca incelenmelidir.
- **MPL-2.0:** Daha esnektir, ancak kapalı türevleri önleme gücü daha sınırlıdır.
- **Apache-2.0/MIT:** Katkı eşiğini düşürür, fakat kapalı türevleri engellemez.

## İlgili Dokümanlar

- [LICENSE_PROPOSAL.md](../../LICENSE_PROPOSAL.md)
- [OPEN_SOURCE_POLICY.md](../../OPEN_SOURCE_POLICY.md)
- [ARCHITECTURAL_PRINCIPLES.md](../../ARCHITECTURAL_PRINCIPLES.md)

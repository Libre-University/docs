# Lisans Önerisi

LibreUniversity için önerilen ana lisans **AGPL-3.0-or-later** lisansıdır.

**Karar:** Öneri kabul edilmiştir ([ADR-0002](docs/adr/0002-prefer-agpl-3-or-later-license.md)). Yazılım repoları AGPL-3.0-or-later, belge repoları CC BY-SA 4.0 ile lisanslanır. Bu belge kararın gerekçesini açıklar.

## Neden AGPL?

LibreUniversity ağ üzerinden hizmet olarak sunulabilecek bir sistemdir. Üniversite bilgi sistemleri çoğu zaman kullanıcıya web arayüzüyle sunulur ve yazılım doğrudan kullanıcı bilgisayarına dağıtılmaz.

AGPL, bu tür ağ üzerinden kullanımda yapılan değişikliklerin de özgür kalmasına yardımcı olur.

Bu proje için AGPL şu nedenle güçlü bir adaydır:

- Bir firma projeyi alıp değiştirerek kapalı hizmete çeviremesin.
- Üniversiteler arası ortak geliştirme korunabilsin.
- Kamu yararıyla üretilen emek yeniden kapalı kutuya dönüşmesin.
- İyileştirmeler topluluğa geri dönebilsin.

## Değerlendirilebilecek Alternatifler

- **GPL-3.0-or-later:** Dağıtılan yazılım için güçlü copyleft sağlar, ancak ağ üzerinden hizmet sunma boşluğu AGPL kadar güçlü değildir.
- **EUPL:** Avrupa kamu kurumları için anlamlı bir seçenek olabilir; uyumluluk ayrıca incelenmelidir.
- **MPL-2.0:** Daha esnek dosya bazlı copyleft sağlar; ancak kapatmaya karşı AGPL kadar güçlü değildir.
- **Apache-2.0/MIT:** Katkıyı kolaylaştırır ama kapalı türevleri engellemez.

## Lisans Kararında Sorulacak Sorular

- Üniversitelerin özgürlüğünü en iyi hangi lisans korur?
- Ticarileşmeye izin verip kapatmayı engellemek istiyor muyuz?
- Kamu kurumları ve üniversiteler açısından hukuki uyumluluk nasıl sağlanır?
- Katkıcı lisans sözleşmesi gerekir mi?
- Üçüncü taraf bağımlılık lisanslarıyla uyumlu mu?

## Önerilen Yol

1. İlk topluluk tartışmasında lisans hedefleri netleştirilsin.
2. AGPL, GPL, EUPL ve MPL seçenekleri karşılaştırılsın.
3. Hukuki görüş alınabiliyorsa alınsın.
4. Nihai karar `LICENSE` dosyasıyla sabitlensin.
5. Bağımlılık politikası lisans kararına göre güncellensin.

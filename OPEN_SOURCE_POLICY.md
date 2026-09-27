# Açık Kaynak ve Bağımlılık Politikası

LibreUniversity'nin temel gücü, özgür yazılım felsefesine bağlı kalmasıdır. Bu politika, projede hangi tür yazılımların kullanılabileceğini ve bağımlılıkların nasıl değerlendirileceğini tanımlar.

## Temel Kural

Kritik işlevler kapalı kaynak, denetlenemeyen, tek tedarikçiye bağımlı veya lisans sunucusuna bağlı ürünler üzerine kurulamaz.

## Kabul Edilebilir Lisanslar

Genel olarak aşağıdaki lisans aileleri kabul edilebilir:

- AGPL.
- GPL.
- LGPL.
- MPL.
- Apache-2.0.
- MIT.
- BSD.

Her bağımlılık için lisans uyumluluğu ayrıca değerlendirilmelidir.

## Riskli veya Kabul Edilmeyen Durumlar

- Kaynak kodu kapalı kritik bileşenler.
- Sadece belirli bir firmanın bulutunda çalışan servisler.
- Üniversitenin verisini dışa aktarmayı kısıtlayan ürünler.
- Lisans süresi bitince sistemin çalışmasını durduran kritik altyapılar.
- Denetlenemeyen sınav, not, ödeme, kimlik, belge veya raporlama bileşenleri.
- Üretimde zorunlu telemetri gönderen ve kapatılamayan yazılımlar.

## Bağımlılık Değerlendirme Kriterleri

Yeni bir bağımlılık eklenmeden önce şu kriterler incelenmelidir:

- Lisans uyumu.
- Kaynak kod erişimi.
- Aktif bakım durumu.
- Güvenlik geçmişi.
- Paket büyüklüğü ve karmaşıklığı.
- Alternatiflerinin olup olmadığı.
- Self-hosted çalışıp çalışmadığı.
- Veri egemenliği üzerindeki etkisi.
- Tedarikçi kilidi riski.
- Projeden kaldırılmasının maliyeti.

## Zorunlu Kapalı Dış Sistemler

Banka, kamu kurumu veya mevzuat nedeniyle bağlanılması gereken kapalı dış sistemler olabilir. Bu sistemler çekirdeğe gömülmez.

Bu tür entegrasyonlar:

- Adapter katmanında izole edilir.
- Açık arayüz arkasına alınır.
- Alternatif sağlayıcıya geçiş mümkün olacak şekilde tasarlanır.
- Log, hata yönetimi ve mutabakat mekanizmasıyla denetlenir.

## Önerilen Lisans

Projenin ana lisansı için öneri **AGPL-3.0-or-later** lisansıdır.

Gerekçe:

- Sistem ağ üzerinden hizmet olarak sunulabilir.
- AGPL, değiştirilen sürümlerin kapatılıp SaaS olarak sunulmasını engellemeye yardımcı olur.
- Üniversiteler arası ortak geliştirme ruhunu korur.

Nihai lisans kararı topluluk yönetişimiyle kesinleştirilmelidir.

## Bağımlılık Envanteri

Geliştirme başladığında her bileşen için bağımlılık envanteri tutulmalıdır:

- Paket adı.
- Sürüm.
- Lisans.
- Kullanıldığı modül.
- Neden gerekli olduğu.
- Alternatifleri.
- Güvenlik notları.

Bu envanter ileride `DEPENDENCIES.md` veya otomatik SBOM çıktısı olarak tutulabilir.

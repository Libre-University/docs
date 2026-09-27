# Mimari İlkeler ve Özgür Yazılım Felsefesi

LibreUniversity, üniversitelerin kapalı kutu sistemlere, belirsiz tedarikçi pratiklerine ve küçük/orta ölçekli yazılım şirketlerinin uzun vadeli kilitleme modellerine mahkum olmaması için tasarlanır. Projenin temel amacı; denetlenebilir, özgür, kendi kendine barındırılabilir, kurumsal hafızası üniversitede kalan bir dijital kampüs ekosistemi oluşturmaktır.

## Temel Felsefe

- **Özgür yazılım önceliği:** Kaynak kodu kapalı, lisansı denetlenemeyen veya üniversiteyi tek firmaya bağımlı hale getiren bileşenler kullanılmamalıdır.
- **Kapalı kutu karşıtlığı:** Sistemin ne yaptığı, hangi veriyi işlediği, hangi dış servise bağlandığı ve hangi kararları nasıl verdiği açıkça denetlenebilmelidir.
- **Tedarikçi bağımsızlığı:** Üniversite isterse sistemi kendi bilgi işlem ekibiyle çalıştırabilmeli, başka bir firmaya devredebilmeli veya toplulukla birlikte geliştirebilmelidir.
- **Self-hosted yaklaşım:** Kritik modüller üniversitenin kendi sunucularında veya kendi kontrol ettiği açık altyapıda çalışmalıdır.
- **Veri egemenliği:** Öğrenci, personel, akademik, mali, sağlık ve disiplin verileri üniversitenin kontrolünde kalmalıdır.
- **Açık standartlar:** Entegrasyonlar mümkün olduğunca açık protokoller, açık veri formatları ve belgelenmiş API sözleşmeleriyle yapılmalıdır.

## Bağımlılık Politikası

- **Kapalı kaynak bağımlılık yok:** Kritik işlevler kapalı kaynak SDK, SaaS, veritabanı, raporlama aracı, sınav aracı, video konferans aracı veya kimlik sistemi üzerine kurulamaz.
- **Tek tedarikçi bağımlılığı yok:** Bir modül belirli bir firma, marka, lisans sunucusu veya bulut sağlayıcısı olmadan çalışamaz hale getirilmemelidir.
- **Asgari teknik bağımlılık:** Kullanılan paket, framework ve servisler gerçekten gerekli olmalı; her bağımlılık lisans, güvenlik, sürdürülebilirlik ve değiştirilebilirlik açısından incelenmelidir.
- **Özgür lisans şartı:** Kullanılan yazılım bileşenleri AGPL, GPL, LGPL, MPL, Apache-2.0, MIT, BSD veya benzeri özgür/açık kaynak lisanslarla uyumlu olmalıdır.
- **Yerine koyulabilirlik:** Her harici bileşen için alternatif açık kaynak seçenekler veya adapter tabanlı değişim noktaları tanımlanmalıdır.
- **Kapalı servis izolasyonu:** Banka, kamu kurumu veya yasal zorunluluk nedeniyle bağlanılması gereken kapalı dış servisler çekirdek mimariye gömülmemeli; ayrı adapter katmanında izole edilmelidir.

## Geliştirme İlkeleri

- **Kod üniversitenin malıdır:** Üniversite, tüm kaynak koda, build süreçlerine, veritabanı şemalarına, deployment betiklerine ve dokümantasyona erişebilmelidir.
- **Denetlenebilir kararlar:** Not hesaplama, mezuniyet uygunluğu, lojman puanı, burs sıralaması, ders kayıt önceliği ve benzeri algoritmalar açık kurallarla çalışmalıdır.
- **Gizli iş kuralı yok:** Sistemde sadece geliştirici firmanın bildiği saklı kural, manuel arka kapı veya görünmeyen işlem akışı bulunmamalıdır.
- **Yerel çalıştırılabilirlik:** Geliştirici ortamı, test ortamı ve üretim kurulumu açık dokümantasyonla yeniden ayağa kaldırılabilir olmalıdır.
- **Açık gözlemlenebilirlik:** Log, metrik, izleme ve alarm mekanizmaları açık araçlarla kurulmalı ve üniversite ekipleri tarafından anlaşılabilir olmalıdır.
- **Toplulukla gelişebilirlik:** Proje başka üniversitelerin katkı verebileceği modüler, belgeli ve lisans açısından paylaşılabilir bir yapıda tasarlanmalıdır.

## Kabul Edilmeyen Yaklaşımlar

- Kaynak kodu teslim edilmeyen veya sadece firma sunucusunda çalışan kritik modüller.
- Lisans süresi bitince üniversitenin kendi verisine veya iş akışına erişemediği sistemler.
- Kapalı kaynak sınav, canlı ders, intihal, BI, CMS, kimlik veya belge yönetimi altyapılarına zorunlu bağımlılık.
- Veriyi dışarı aktarmayı zorlaştıran, şema dokümantasyonu vermeyen veya açık API sunmayan ürünler.
- Güvenlik gerekçesiyle denetlenebilirliği ortadan kaldıran kapalı kutu bileşenler.
- Kamu/üniversite işleyişini firma personelinin manuel müdahalesine bağımlı hale getiren süreçler.

## Tercih Edilecek Açık Kaynak Bileşen Örnekleri

- **Kimlik ve SSO:** Keycloak, OpenLDAP, FreeIPA.
- **Canlı ders:** Jitsi, Jibri, Jitsi Videobridge.
- **Nesne depolama:** MinIO veya S3 uyumlu özgür alternatifler.
- **Video işleme:** FFmpeg.
- **Arama:** OpenSearch, Meilisearch.
- **Gözlemlenebilirlik:** Prometheus, Grafana, Loki, OpenTelemetry.
- **SIEM/Güvenlik:** Wazuh, Zeek, Suricata.
- **Veritabanı:** PostgreSQL, MariaDB, Redis/Valkey.
- **Mesaj kuyruğu:** RabbitMQ, NATS, Apache Kafka uyumlu açık kaynak seçenekler.
- **Baskı altyapısı:** CUPS ve açık protokol tabanlı yazıcı entegrasyonları.

Bu liste bağlayıcı ürün listesi değil, felsefeyi gösteren örnek listedir. Nihai teknoloji seçimi her zaman özgür lisans, sürdürülebilirlik, güvenlik, performans ve tedarikçi bağımsızlığı kriterleriyle yapılmalıdır.

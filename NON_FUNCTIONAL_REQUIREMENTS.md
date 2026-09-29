# Fonksiyonel Olmayan Gereksinimler

Bu doküman LibreUniversity sisteminin kalite, güvenlik, performans, işletim ve uyumluluk beklentilerini tanımlar. Fonksiyonel gereksinimler sistemin ne yapacağını, bu doküman ise bunu hangi kalite seviyesinde yapacağını açıklar.

## NFR-00 Özgür Yazılım, Şeffaflık ve Tedarikçi Bağımsızlığı

- **NFR-00.01:** Kritik bileşenler kaynak kodu kapalı, denetlenemeyen veya lisans sunucusuna bağımlı ürünler üzerine kurulamaz.
- **NFR-00.02:** Sistem self-hosted çalışabilmeli; üniversite kendi veri merkezinde veya kontrol ettiği açık altyapıda sistemi ayağa kaldırabilmelidir.
- **NFR-00.03:** Kullanılan tüm bağımlılıklar lisans, güvenlik, bakım durumu, kaynak kod erişimi ve alternatif bulunabilirliği açısından kayıt altına alınmalıdır.
- **NFR-00.04:** Harici paket ve servis bağımlılıkları asgari seviyede tutulmalı; her bağımlılık için gerekçe ve değiştirme planı bulunmalıdır.
- **NFR-00.05:** Kapalı kaynak SaaS servisleri; OBS, LMS, SSO, CMS, EBYS, BI, sınav, intihal, ödeme orkestrasyonu ve denetim izi gibi kritik işlevlerin zorunlu parçası olamaz.
- **NFR-00.06:** Veri dışa aktarma, yedekten geri dönme ve başka kurulum ortamına taşıma süreçleri açık formatlarla ve firma iznine gerek kalmadan yapılabilmelidir.
- **NFR-00.07:** Build, test, deployment ve migration süreçleri açık araçlarla otomasyon halinde dokümante edilmelidir.

## NFR-01 Performans

- **NFR-01.01:** Öğrenci, akademisyen ve personel self-servis ekranlarında standart sayfa yanıt süresi normal yük altında 2 saniyenin altında olmalıdır.
- **NFR-01.02:** Ders kayıt dönemi gibi yoğun süreçlerde sistem en az 50.000 eşzamanlı öğrenciyi kuyruklama ve durum bilgilendirme mekanizmasıyla yönetebilmelidir.
- **NFR-01.03:** Kritik işlemler için p95 API yanıt süresi 500 ms, p99 yanıt süresi 1500 ms hedefini aşmamalıdır.
- **NFR-01.04:** Raporlama ve BI sorguları operasyonel sistemleri yavaşlatmayacak şekilde veri ambarı veya okuma replikaları üzerinden çalışmalıdır.
- **NFR-01.05:** Canlı ders altyapısı eşzamanlı yüzlerce sınıfı yatay ölçeklenebilir Jitsi Videobridge havuzuyla desteklemelidir.

## NFR-02 Ölçeklenebilirlik

- **NFR-02.01:** Uygulama durumsuz (stateless) tasarlanmalı; web, API ve arka plan işçileri birden fazla örnek olarak yatay ölçeklenebilmelidir. Tek uygulama olarak dağıtım ([ADR-0004](docs/adr/0004-start-with-modular-monolith-for-mvp.md), [ADR-0011](docs/adr/0011-use-go-for-backend.md)) bu gereksinimi ortadan kaldırmaz.
- **NFR-02.02:** Dosya, video ve ders kayıtları nesne depolama üzerinde tutulmalı; uygulama sunucularına bağlı kalmamalıdır.
- **NFR-02.03:** Yoğun toplu işler, VOD dönüştürme, bildirim gönderimi ve entegrasyon senkronizasyonları asenkron kuyruklarla yürütülmelidir.
- **NFR-02.04:** Birim siteleri çok kiracılı mimaride birbirinden izole olmalı; bir kiracının yoğunluğu diğer kiracıları etkilememelidir.

## NFR-03 Kullanılabilirlik ve Süreklilik

- **NFR-03.01:** Uygulama, kimlik sağlayıcı (SSO), veritabanı, nesne depolama ve ters vekil sunucu yüksek erişilebilirlik mimarisiyle çalışabilmelidir; ödeme ve kampüs kartı gibi kritik modüller bu altyapıya dahildir.
- **NFR-03.02:** Akademik dönem içindeki kritik servisler için aylık kullanılabilirlik hedefi en az %99,9 olmalıdır.
- **NFR-03.03:** Planlı bakım pencereleri önceden duyurulmalı ve kritik akademik takvim dönemlerinde bakım yapılmamalıdır.
- **NFR-03.04:** Tek bir uygulama düğümü veya veritabanı replikasının arızası sistemin tamamını durdurmamalıdır.
- **NFR-03.05:** Dış kurum entegrasyonları kesildiğinde sistem kullanıcıya anlamlı hata göstermeli ve işlemleri tekrar denenebilir kuyruğa almalıdır.

## NFR-04 Güvenlik

- **NFR-04.01:** Tüm kullanıcı erişimleri merkezi SSO ve MFA destekli kimlik doğrulama üzerinden yapılmalıdır.
- **NFR-04.02:** Yetkilendirme rol, birim, görev, veri kapsamı ve işlem türüne göre ayrıntılı şekilde uygulanmalıdır.
- **NFR-04.03:** Hassas işlemler için denetim izi tutulmalı; not, ödeme, sağlık, disiplin, hukuk ve kişisel veri erişimleri ayrıca izlenmelidir.
- **NFR-04.04:** Tüm ağ trafiği TLS ile şifrelenmeli; uygulamanın kimlik sağlayıcı, veritabanı, nesne depolama ve dış sistem adapterleriyle iletişiminde güvenli kimlik doğrulama kullanılmalıdır.
- **NFR-04.05:** Parola, token, API anahtarı, sertifika ve entegrasyon sırları merkezi secret yönetimiyle saklanmalıdır.
- **NFR-04.06:** Dosya yükleme alanlarında zararlı içerik taraması, dosya tipi kontrolü ve boyut sınırı uygulanmalıdır.
- **NFR-04.07:** Web uygulamaları OWASP Top 10 risklerine karşı güvenli geliştirme ve test süreçlerinden geçirilmelidir.

## NFR-05 KVKK, Gizlilik ve Veri Yönetişimi

- **NFR-05.01:** Kişisel veriler veri minimizasyonu, amaç sınırlılığı ve saklama süresi ilkelerine uygun işlenmelidir.
- **NFR-05.02:** Açık rıza, aydınlatma metni, iletişim izni ve veri işleme amacı kayıtları sistemde takip edilebilmelidir.
- **NFR-05.03:** Sağlık, disiplin, hukuk, finans ve engellilik bilgileri özel nitelikli veri olarak daha sıkı erişim kontrolleriyle korunmalıdır.
- **NFR-05.04:** Kullanıcılar yetkileri dahilinde veri düzeltme, erişim, silme/anonimleştirme ve başvuru süreçlerini başlatabilmelidir.
- **NFR-05.05:** Test ve geliştirme ortamlarında gerçek kişisel veriler maskeleme veya anonimleştirme olmadan kullanılmamalıdır.

## NFR-06 Uyumluluk ve Standartlar

- **NFR-06.01:** Üniversite süreçleri YÖK, YÖKAK, KVKK, e-Devlet, e-imza, KEP ve ilgili kamu mevzuatıyla uyumlu olmalıdır.
- **NFR-06.02:** Sağlık süreçlerinde HL7/FHIR, e-Nabız ve Medula gereklilikleri dikkate alınmalıdır.
- **NFR-06.03:** Akademik entegrasyonlarda YÖKSİS, ÖSYM ve ilgili veri formatları desteklenmelidir.
- **NFR-06.04:** Erişilebilirlik için web ve mobil arayüzler en az WCAG 2.2 AA seviyesini hedeflemelidir.
- **NFR-06.05:** EBYS ve resmi belge süreçleri e-imza, zaman damgası ve arşiv standartlarına uygun olmalıdır.

## NFR-07 Erişilebilirlik ve Kullanıcı Deneyimi

- **NFR-07.01:** Arayüzler öğrenci, akademisyen, idari personel ve dış paydaşların sık kullandığı işlemleri hızlı bulabileceği şekilde rol bazlı tasarlanmalıdır.
- **NFR-07.02:** Mobil ve web arayüzleri duyarlı tasarımla masaüstü, tablet ve telefon ekranlarında kullanılabilir olmalıdır.
- **NFR-07.03:** Formlar açık doğrulama mesajları, kayıt taslağı, otomatik tamamlama ve işlem durumu göstergeleri sunmalıdır.
- **NFR-07.04:** Kritik işlemlerde kullanıcıya geri alınabilirlik, onay ekranı veya işlem özeti sağlanmalıdır.
- **NFR-07.05:** Ekran okuyucu, klavye navigasyonu, yeterli kontrast, altyazı/transkript ve erişilebilir belge üretimi desteklenmelidir.

## NFR-08 Entegrasyon ve Birlikte Çalışabilirlik

- **NFR-08.01:** Modüller arası veri alışverişi dokümante edilmiş API sözleşmeleriyle yapılmalıdır.
- **NFR-08.02:** API giriş katmanı (ters vekil sunucu ve uygulama) hız sınırlama, kimlik doğrulama, yetkilendirme, loglama ve API versiyonlama desteklemelidir; ayrı bir API Gateway bileşeni MVP kapsamında değildir.
- **NFR-08.03:** Dış sistem entegrasyonlarında tekrar deneme, idempotency, hata kuyruğu ve mutabakat raporu bulunmalıdır.
- **NFR-08.04:** Sistem dışa veri aktarımında CSV, XLSX, JSON, PDF ve gerektiğinde XML formatlarını desteklemelidir.
- **NFR-08.05:** Entegrasyonlar ortam bazlı ayrılmalı; test ve canlı kurum servisleri birbirine karışmamalıdır.

## NFR-09 Veri Bütünlüğü ve Tutarlılık

- **NFR-09.01:** Not, ödeme, ders kayıt, mezuniyet ve resmi belge işlemleri işlem bütünlüğü sağlayacak şekilde tasarlanmalıdır.
- **NFR-09.02:** Kritik iş kuralları yalnızca istemci tarafında değil, sunucu tarafında da doğrulanmalıdır.
- **NFR-09.03:** Aynı verinin birden fazla modülde kullanıldığı durumlarda kaynak sistem ve senkronizasyon kuralları açıkça tanımlanmalıdır.
- **NFR-09.04:** Toplu veri aktarımı sonrası hata, atlanan kayıt ve mutabakat raporu üretilebilmelidir.

## NFR-10 Yedekleme, Felaket Kurtarma ve Arşiv

- **NFR-10.01:** Veritabanları, nesne depolama, konfigürasyonlar ve kritik dosyalar düzenli olarak yedeklenmelidir.
- **NFR-10.02:** Kritik sistemler için RPO en fazla 15 dakika, RTO en fazla 2 saat hedeflenmelidir.
- **NFR-10.03:** Yedeklerden geri dönüş düzenli olarak test edilmeli ve test sonuçları raporlanmalıdır.
- **NFR-10.04:** Resmi belge, akademik kayıt ve mali kayıt arşivleri mevzuattaki saklama sürelerine uygun korunmalıdır.
- **NFR-10.05:** Felaket kurtarma planı veri merkezi, ağ, kimlik sistemi, ödeme, OBS ve LMS senaryolarını kapsamalıdır.

## NFR-11 Gözlemlenebilirlik ve Operasyon

- **NFR-11.01:** Uygulama ve her modül yapılandırılmış log, metrik ve izleme verisi üretmelidir.
- **NFR-11.02:** Kritik iş akışları için teknik metriklerin yanında iş metrikleri de izlenmelidir; örneğin ders kayıt başarı oranı, ödeme mutabakatı ve canlı ders hata oranı.
- **NFR-11.03:** Alarm kuralları öncelik, sorumlu ekip, eskalasyon ve müdahale süresiyle tanımlanmalıdır.
- **NFR-11.04:** Sürüm geçişleri geriye dönüş planı, değişiklik kaydı ve minimum kesinti prensibiyle yapılmalıdır.
- **NFR-11.05:** Loglar SIEM'e aktarılmalı ve güvenlik olayları operasyonel izleme olaylarından ayrıştırılmalıdır.

## NFR-12 Bakım Yapılabilirlik ve Geliştirilebilirlik

- **NFR-12.01:** Kod, API, veri modeli ve entegrasyon sözleşmeleri sürüm kontrollü ve dokümante olmalıdır.
- **NFR-12.02:** Modüller gevşek bağlı tasarlanmalı; OBS, LMS, ERP, CMS ve mobil katman bağımsız geliştirilebilir olmalıdır.
- **NFR-12.03:** İş kuralları konfigüre edilebilir olmalı; akademik takvim, not sistemi, ödeme kalemi ve onay akışları kod değişikliği gerektirmeden yönetilebilmelidir.
- **NFR-12.04:** Kritik modüllerde birim, entegrasyon, güvenlik ve yük testleri CI/CD sürecine dahil edilmelidir.
- **NFR-12.05:** Veritabanı şeması değişiklikleri migration yaklaşımıyla izlenebilir ve geri alınabilir olmalıdır.

## NFR-13 Çok Kiracılık ve İzolasyon

- **NFR-13.01:** Fakülte, enstitü, kulüp, araştırma merkezi ve teknokent gibi kiracılar içerik, yetki ve veri kapsamı açısından ayrıştırılmalıdır.
- **NFR-13.02:** Kiracı bazlı tema, alan adı, menü, içerik ve onay akışı tanımlanabilmelidir.
- **NFR-13.03:** Bir kiracının yetkili kullanıcısı başka kiracıya ait içerik veya veriye yetkisiz erişememelidir.
- **NFR-13.04:** Kiracı bazlı kullanım, trafik, depolama ve içerik metrikleri raporlanabilmelidir.

## NFR-14 Bildirim ve Mesajlaşma Kalitesi

- **NFR-14.01:** Bildirimler hedef kitle, kanal, öncelik, zamanlama ve iletişim izni kurallarına göre gönderilmelidir.
- **NFR-14.02:** SMS, e-posta ve push gönderimlerinde teslim durumu, başarısızlık nedeni ve tekrar deneme bilgileri saklanmalıdır.
- **NFR-14.03:** Acil durum bildirimleri normal pazarlama veya duyuru trafiğinden öncelikli işlenmelidir.
- **NFR-14.04:** Kullanıcılar mevzuatın izin verdiği bildirim türleri için tercihlerini yönetebilmelidir.

## NFR-15 Medya, Dosya ve İçerik Yönetimi

- **NFR-15.01:** Ders videoları HLS/MP4 gibi yaygın formatlarda sunulmalı ve bant genişliği koşullarına uyum sağlayabilmelidir.
- **NFR-15.02:** Büyük dosya yüklemeleri kesintiye dayanıklı ve devam ettirilebilir olmalıdır.
- **NFR-15.03:** İçeriklere telif, sahiplik, erişim seviyesi ve saklama süresi metadata bilgileri eklenebilmelidir.
- **NFR-15.04:** Kamuya açık web içerikleri arama motorları ve sosyal paylaşım önizlemeleri için uygun metadata üretmelidir.

## NFR-16 Denetlenebilirlik

- **NFR-16.01:** Kim, neyi, ne zaman, hangi IP/cihaz üzerinden yaptı bilgisi kritik işlemler için değiştirilemez denetim kaydı olarak tutulmalıdır.
- **NFR-16.02:** Denetim kayıtları yetkisiz silme ve değiştirmeye karşı korunmalıdır.
- **NFR-16.03:** İç denetim, dış denetim, akreditasyon ve adli talepler için yetki kontrollü rapor üretilebilmelidir.
- **NFR-16.04:** Denetim kayıtlarında kişisel veri görünürlüğü asgari yetki prensibiyle sınırlandırılmalıdır.

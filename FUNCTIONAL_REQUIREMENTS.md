# Fonksiyonel Gereksinimler

Bu doküman LibreUniversity kapsamındaki üniversite dijital ekosisteminin kullanıcıya görünen işlevlerini tanımlar. Gereksinimler modül bazlı yazılmıştır ve her madde doğrulanabilir bir sistem davranışı olarak ele alınmalıdır.

## Proje İlkesi

- **FR-00.01:** Sistem, kapalı kutu ürünlere ve tek tedarikçiye bağımlı kalmadan özgür yazılım felsefesiyle geliştirilmeli ve çalıştırılabilmelidir.
- **FR-00.02:** Üniversite; kaynak koduna, veritabanı şemasına, deployment betiklerine, entegrasyon sözleşmelerine ve teknik dokümantasyona eksiksiz erişebilmelidir.
- **FR-00.03:** Kritik iş kuralları ve algoritmalar sistem içinde denetlenebilir olmalı; gizli, firma tarafında saklanan veya dışarıdan görülemeyen karar mekanizması bulunmamalıdır.
- **FR-00.04:** Zorunlu banka, kamu kurumu ve mevzuat entegrasyonları çekirdek sisteme gömülmeden, değiştirilebilir adapter katmanı üzerinden yürütülmelidir.

## Roller

- **Öğrenci:** Ders kaydı, not, belge, LMS, yurt, yemekhane, ödeme, başvuru ve destek işlemlerini yürütür.
- **Akademisyen:** Ders, not, yoklama, LMS içerikleri, sınav, araştırma, BAP ve danışmanlık süreçlerini yönetir.
- **İdari Personel:** Öğrenci işleri, insan kaynakları, mali işler, EBYS, satın alma, destek ve operasyon süreçlerini yürütür.
- **Yönetici/Rektörlük:** Raporlama, KPI, kalite, bütçe, risk, güvenlik ve stratejik karar panellerini kullanır.
- **Dış Paydaş:** Aday öğrenci, mezun, işveren, ziyaretçi, firma, hasta, veli veya SEM kursiyeri olarak sınırlı portalları kullanır.
- **Sistem Yöneticisi:** Kimlik, yetki, entegrasyon, izleme, güvenlik, log ve platform konfigürasyonlarını yönetir.

## FR-01 Çok Kiracılı Web ve İçerik Yönetimi

- **FR-01.01:** Sistem ana portal, fakülte/enstitü/yüksekokul, araştırma merkezi, laboratuvar ve öğrenci kulübü sitelerinin tek CMS altyapısından yönetilmesini sağlamalıdır.
- **FR-01.02:** Her birim kendi içeriklerini rol bazlı yetkilerle oluşturabilmeli, düzenleyebilmeli, yayına alabilmeli ve arşivleyebilmelidir.
- **FR-01.03:** Haber, duyuru ve etkinlik içerikleri merkezi portalda ve ilgili alt sitelerde hedef kitleye göre yayınlanabilmelidir.
- **FR-01.04:** Akademisyen profil sayfaları ders, yayın, proje ve iletişim verilerini ilgili sistemlerden otomatik çekebilmelidir.
- **FR-01.05:** İçerikler için taslak, onay, yayın, geri çekme ve sürüm geçmişi iş akışları desteklenmelidir.

## FR-02 Öğrenci Bilgi Sistemi (OBS/SIS)

- **FR-02.01:** Aday öğrenci başvurusu, evrak yükleme, doğrulama, değerlendirme, kabul ve kesin kayıt süreçleri sistem üzerinden yürütülmelidir.
- **FR-02.02:** Program, bölüm, müfredat, AKTS, ön koşul, eşdeğer ders ve mezuniyet kuralı tanımları yönetilebilmelidir.
- **FR-02.03:** Öğrenciler ders kayıt döneminde ders seçebilmeli; sistem kontenjan, ön koşul, çakışma, borç ve danışman onayı kontrollerini yapmalıdır.
- **FR-02.04:** Ders kayıt yoğunluğunda işlemler sıraya alınmalı ve kullanıcılara işlem durumu gösterilmelidir.
- **FR-02.05:** Akademisyenler sınav, ödev, final, bütünleme, mazeret ve harf notu girişlerini yapabilmelidir.
- **FR-02.06:** Sistem çan eğrisi, mutlak değerlendirme ve fakülte/bölüm bazlı not hesaplama kurallarını desteklemelidir.
- **FR-02.07:** Öğrenciler not itirazı, maddi hata başvurusu, ders saydırma, muafiyet, staj ve intibak süreçlerini başlatabilmelidir.
- **FR-02.08:** Yoklama QR, NFC veya manuel yöntemlerle alınabilmeli; devamsızlık sınırına yaklaşan öğrencilere uyarı gönderilmelidir.
- **FR-02.09:** Öğrenci belgesi, transkript, diploma eki ve mezuniyet uygunluk kontrolleri sistem tarafından üretilebilmelidir.

## FR-03 LMS, Canlı Ders ve Ölçme-Değerlendirme

- **FR-03.01:** Her ders için haftalık izlence, materyal, duyuru, forum, ödev, sınav ve kayıtlı ders içerikleri yönetilebilmelidir.
- **FR-03.02:** Canlı dersler LMS içinde gömülü Jitsi oturumu olarak açılmalı ve kullanıcı rolleri SSO/JWT üzerinden atanmalıdır.
- **FR-03.03:** Ders kayıtları Jibri ile alınmalı, MinIO/S3 uyumlu depolamaya aktarılmalı ve VOD pipeline sonrası ilgili haftaya otomatik bağlanmalıdır.
- **FR-03.04:** Online sınavlar soru bankası, rastgele soru üretimi, süre yönetimi, güvenli tarayıcı entegrasyonu ve otomatik notlandırma desteklemelidir.
- **FR-03.05:** Ödev teslimleri son tarih, geç teslim cezası, dosya sürümü ve intihal/benzerlik denetimi kurallarıyla yönetilmelidir.

## FR-04 Akademik Araştırma ve BAP

- **FR-04.01:** Akademisyen yayın, patent, bildiri, kitap, atıf, proje ve akademik teşvik verilerini yönetebilmelidir.
- **FR-04.02:** Sistem YÖKSİS ve dış akademik veri kaynaklarıyla veri aktarımı veya doğrulama yapabilmelidir.
- **FR-04.03:** BAP başvurusu, hakem değerlendirmesi, bütçe kalemi, ara rapor, sonuç raporu ve ödeme onay süreçleri yürütülmelidir.
- **FR-04.04:** Etik kurul başvuru, gündem, karar, revizyon ve arşiv süreçleri sistemde takip edilebilmelidir.
- **FR-04.05:** TTO; patent, lisanslama, sanayi iş birliği, kuluçka ve firma görüşmelerini kayıt altına alabilmelidir.

## FR-05 Akıllı Kampüs ve Yaşam

- **FR-05.01:** Kampüs kartı; turnike, otopark, laboratuvar, yemekhane, kütüphane ve etkinlik geçişlerinde kullanılabilmelidir.
- **FR-05.02:** Yurt başvurusu, oda/yatak yerleştirme, izin, aidat ve kapasite yönetimi yapılabilmelidir.
- **FR-05.03:** Yemekhane menüsü, kalori bilgisi, bakiye yükleme, öğün rezervasyonu ve turnike düşümü desteklenmelidir.
- **FR-05.04:** Ring araçlarının anlık konumu mobil uygulama ve web üzerinden görüntülenebilmelidir.
- **FR-05.05:** Spor alanı, salon, çalışma odası, konferans salonu ve benzeri mekanlar rezervasyon kurallarıyla yönetilmelidir.
- **FR-05.06:** Mediko ve psikolojik danışmanlık için randevu, kayıt, yönlendirme ve yetki kısıtlı sağlık notları tutulabilmelidir.

## FR-06 Kurumsal Yönetim ve ERP

- **FR-06.01:** Harç, yaz okulu, yurt, yemekhane, SEM ve etkinlik ödemeleri sanal POS/banka entegrasyonlarıyla alınabilmelidir.
- **FR-06.02:** Burs, indirim, taksit, iade, borç ve tahsilat süreçleri öğrenci finans kayıtlarına yansıtılmalıdır.
- **FR-06.03:** Personel özlük, izin, rapor, nöbet, bordro ve maaş süreçleri yönetilebilmelidir.
- **FR-06.04:** Satın alma, doğrudan temin, teklif, ihale komisyonu, sözleşme ve teslim alma süreçleri yürütülmelidir.
- **FR-06.05:** Demirbaşlar barkod/RFID ile zimmetlenmeli, bakım, sayım ve amortisman bilgileri takip edilmelidir.
- **FR-06.06:** EBYS üzerinden resmi yazışma, e-imza, KEP, paraf, havale, arşiv ve gelen/giden evrak süreçleri yönetilmelidir.

## FR-07 Kütüphane ve Dijital Kaynaklar

- **FR-07.01:** Kitap, dergi, tez, elektronik kaynak ve materyal katalogları yönetilebilmelidir.
- **FR-07.02:** Ödünç, iade, uzatma, gecikme cezası, rezerve ve RFID kapı entegrasyonu desteklenmelidir.
- **FR-07.03:** Kampüs dışı erişim için yetkilendirilmiş proxy veya federasyon tabanlı veri tabanı erişimi sağlanmalıdır.

## FR-08 İletişim, Destek ve Mezunlar

- **FR-08.01:** Kullanıcılar öğrenci işleri, bilgi işlem, teknik servis, temizlik ve diğer birimler için destek bileti açabilmelidir.
- **FR-08.02:** Destek talepleri kategori, öncelik, SLA, atama, eskalasyon ve memnuniyet değerlendirmesiyle takip edilmelidir.
- **FR-08.03:** SMS, e-posta, mobil push ve anket gönderimleri hedef kitle filtreleriyle yapılabilmelidir.
- **FR-08.04:** Mezun profili, iletişim izni, kariyer geçmişi, bağış/fon ve mezun etkinliği süreçleri yönetilebilmelidir.

## FR-09 Sistem Çekirdeği ve Entegrasyon

- **FR-09.01:** Tüm modüller merkezi SSO ile kimlik doğrulamalı ve rol/izin yönetimi merkezi olarak yapılmalıdır.
- **FR-09.02:** API Gateway; iç servisler, mobil uygulamalar ve dış kurum entegrasyonları için güvenli erişim sağlamalıdır.
- **FR-09.03:** e-Devlet, YÖKSİS, SGK, MERNİS, ÖSYM, KBS, UYAP, e-Nabız ve diğer dış sistemlerle entegrasyon noktaları yönetilebilmelidir.
- **FR-09.04:** Raporlama ve BI katmanı akademik, idari, mali, kalite ve kampüs operasyon verilerini yetkiye göre sunmalıdır.
- **FR-09.05:** Kullanıcı işlemleri denetim izi olarak kayıt altına alınmalı; hassas veri erişimleri ayrıca izlenmelidir.

## FR-10 Siber Güvenlik ve Gözetlenebilirlik

- **FR-10.01:** Sunucu, uygulama, ağ ve kimlik logları merkezi SIEM sistemine aktarılmalıdır.
- **FR-10.02:** Başarısız giriş, yetki ihlali, anormal trafik, veri sızıntısı ve şüpheli davranışlar için alarm üretilebilmelidir.
- **FR-10.03:** Uygulama ve altyapı bileşenleri için düzenli zafiyet taraması, bulgu takibi ve kapatma iş akışı bulunmalıdır.
- **FR-10.04:** Servis sağlığı, hata oranı, gecikme, kapasite ve kullanılabilirlik metrikleri izlenebilmelidir.

## FR-11 Kalite, Akreditasyon ve Stratejik Planlama

- **FR-11.01:** Stratejik hedef, KPI, faaliyet, sorumlu birim ve gerçekleşme verileri takip edilmelidir.
- **FR-11.02:** YÖKAK, MÜDEK, ABET ve benzeri akreditasyon süreçleri için kanıt dosyaları ve özdeğerlendirme raporları yönetilebilmelidir.
- **FR-11.03:** Ders değerlendirme, memnuniyet, 360 derece değerlendirme ve geri bildirim anketleri yapılabilmelidir.
- **FR-11.04:** Program çıktısı, ders çıktısı ve ölçme-değerlendirme ilişkileri müfredat matrisi olarak izlenebilmelidir.

## FR-12 Uluslararası İlişkiler ve Değişim Programları

- **FR-12.01:** Erasmus, Farabi, Mevlana ve diğer değişim programları için anlaşma, kontenjan, başvuru ve değerlendirme süreçleri yönetilmelidir.
- **FR-12.02:** Gelen ve giden öğrenci/personel için evrak, vize, öğrenim anlaşması, hibe ve oryantasyon süreçleri takip edilmelidir.
- **FR-12.03:** Hibe hesaplama, ödeme, kesinti ve bütçe raporları üretilebilmelidir.

## FR-13 SEM ve Yaşam Boyu Öğrenme

- **FR-13.01:** Dış katılımcılar ücretli veya ücretsiz sertifika programlarına başvurabilmeli ve ödeme yapabilmelidir.
- **FR-13.02:** SEM eğitimleri için kontenjan, eğitmen, takvim, yoklama, sınav ve sertifika süreçleri yönetilmelidir.
- **FR-13.03:** Eğitim sonunda e-imzalı, QR doğrulamalı ve e-Devlet entegrasyonuna hazır sertifika üretilebilmelidir.

## FR-14 Kariyer Merkezi ve Yetenek Yönetimi

- **FR-14.01:** İşverenler onay sürecinden geçerek staj, part-time ve tam zamanlı ilan yayınlayabilmelidir.
- **FR-14.02:** Öğrenciler CV, yetkinlik, portfolyo ve başvuru geçmişini yönetebilmelidir.
- **FR-14.03:** Sistem öğrenci yetkinlikleri ile işveren beklentilerini eşleştirerek öneri ve bildirim üretebilmelidir.
- **FR-14.04:** Cumhurbaşkanlığı Yetenek Kapısı ve Ulusal Staj Programı verileriyle çift yönlü entegrasyon desteklenmelidir.

## FR-15 Üniversite Hastanesi ve Klinik Yönetimi

- **FR-15.01:** Hasta randevu, poliklinik, tetkik, laboratuvar, ameliyathane, eczane ve faturalama süreçleri HBYS kapsamında yönetilmelidir.
- **FR-15.02:** Tıp ve diş hekimliği öğrencileri için vaka logbook, intörn nöbeti ve yetki kısıtlı eğitim süreçleri desteklenmelidir.
- **FR-15.03:** e-Nabız, Medula ve HL7/FHIR standartlarında sağlık veri entegrasyonları sağlanmalıdır.

## FR-16 Hukuk ve Disiplin

- **FR-16.01:** Dava, icra, duruşma, vekalet, belge ve UYAP entegrasyon kayıtları takip edilmelidir.
- **FR-16.02:** Öğrenci ve personel disiplin soruşturmaları gizlilik seviyesine göre yetkilendirilmiş iş akışlarıyla yürütülmelidir.
- **FR-16.03:** Sözleşme yaşam döngüsü; taslak, hukuk onayı, imza, yürürlük, yenileme ve fesih adımlarını içermelidir.

## FR-17 Kampüs GIS ve Dijital İkiz

- **FR-17.01:** Bina, kat, oda, yol, altyapı hattı, enerji, su, doğalgaz ve fiber varlıkları GIS üzerinde yönetilmelidir.
- **FR-17.02:** Mobil uygulamada erişilebilir rota ve iç mekan yönlendirme sağlanmalıdır.
- **FR-17.03:** Akıllı sayaç verileriyle bina/fakülte bazlı enerji ve su tüketimi izlenebilmelidir.

## FR-18 Engelsiz Üniversite ve Kapsayıcılık

- **FR-18.01:** Engelli öğrenciler sınav uyarlaması, ek süre, okuyucu/işaretleyici ve erişilebilir materyal taleplerini iletebilmelidir.
- **FR-18.02:** Talepler ilgili komisyon, öğretim elemanı ve öğrenci işleri tarafından iş akışıyla sonuçlandırılmalıdır.
- **FR-18.03:** Kampüs haritası erişilebilir rota, asansör, rampa ve uygun mekan filtrelerini sunmalıdır.

## FR-19 Merkezi Baskı ve Doküman Yönetimi

- **FR-19.01:** Öğrenci ve personel baskı kotası, bakiye, ücretlendirme ve raporlama süreçleri yönetilmelidir.
- **FR-19.02:** Follow-Me Printing ile çıktı güvenli biçimde kuyruğa alınmalı ve kullanıcı kartını okuttuğunda ilgili yazıcıdan alınmalıdır.

## FR-20 Etkinlik, Kongre ve Ziyaretçi Yönetimi

- **FR-20.01:** Etkinlik, kongre, tören ve şenlikler için kayıt, LCV, koltuk, bilet ve QR kontrol süreçleri yönetilmelidir.
- **FR-20.02:** Ziyaretçiler süreli/kısıtlı geçiş QR kodlarıyla kampüs turnikelerinden yetkili biçimde geçebilmelidir.

## FR-21 Teknokent / Teknopark Yönetimi

- **FR-21.01:** Firma başvurusu, hakem değerlendirmesi, kabul, proje, ofis tahsisi ve sözleşme süreçleri yönetilmelidir.
- **FR-21.02:** Ar-Ge proje, personel muafiyeti ve giriş-çıkış verileri Sanayi ve Teknoloji Bakanlığı entegrasyonuna hazırlanmalıdır.
- **FR-21.03:** Kuluçka programları, girişimci başvuruları, mentor görüşmeleri ve yatırımcı temasları takip edilmelidir.

## FR-22 Taşınmaz, Ticari Alan ve Lojman Yönetimi

- **FR-22.01:** Kampüsteki ticari alan, ATM, kantin, kafeterya, kuaför, kırtasiye ve benzeri kiralanabilir alanlar kayıt altına alınmalıdır.
- **FR-22.02:** Sözleşme bitiş tarihi, kira, ciro payı, tahsilat, gecikme ve yenileme süreçleri takip edilebilmelidir.
- **FR-22.03:** Lojman başvuruları puanlama, sıra, tahsis, itiraz ve boşaltma süreçleriyle yönetilebilmelidir.

## FR-23 Araç Filosu, İş Makinesi ve Lojistik Yönetimi

- **FR-23.01:** Üniversite araçları, iş makineleri, makam araçları ve servis/ring araçları envanter olarak yönetilebilmelidir.
- **FR-23.02:** Araç talebi, şoför görevlendirme, güzergah, harcırah, yakıt ve GPS takibi yapılabilmelidir.
- **FR-23.03:** Kasko, sigorta, TÜVTÜRK muayenesi, bakım, onarım ve arıza süreçleri tarih ve maliyetleriyle izlenebilmelidir.

## FR-24 İSG ve Afet Yönetimi

- **FR-24.01:** Bina, laboratuvar, atölye ve saha çalışmaları için risk değerlendirme, denetim ve ramak kala kayıtları tutulabilmelidir.
- **FR-24.02:** Yangın tüpü, asansör, acil çıkış, iş ekipmanı ve periyodik kontrol tarihleri izlenebilmelidir.
- **FR-24.03:** Afet anında kampüste bulunan kişilere lokasyon bazlı SMS/push bildirimi gönderilebilmeli ve toplanma alanları GIS üzerinde gösterilebilmelidir.
- **FR-24.04:** Kimyasal, tıbbi ve tehlikeli atık teslim, bertaraf firması, miktar ve belge kayıtları tutulabilmelidir.

## FR-25 Fiziksel Arşiv, Müze ve Kültür Varlıkları Yönetimi

- **FR-25.01:** Fiziksel arşiv kutu, raf, depo, dosya ve belge seviyesinde barkod/RFID ile konumlandırılabilmelidir.
- **FR-25.02:** Eski evraklar OCR sürecinden geçirilerek tam metin aranabilir dijital arşive aktarılabilmelidir.
- **FR-25.03:** Müze ve kültür varlıkları için envanter, sigorta değeri, restorasyon, sergileme ve ödünç verme süreçleri takip edilebilmelidir.

## FR-26 Mobil Uygulama ve Self-Servis Portal

- **FR-26.01:** Kullanıcılar rolüne göre kişiselleştirilmiş mobil/web ana sayfa üzerinden ders, duyuru, ödeme, randevu, bildirim ve başvuru özetlerini görebilmelidir.
- **FR-26.02:** Mobil uygulama dijital kampüs kartı, QR/NFC kimlik, etkinlik bileti, yemekhane ve kütüphane işlemlerini desteklemelidir.
- **FR-26.03:** Belge, izin, yurt, burs, ders itirazı, destek, randevu ve etkinlik başvuruları self-servis olarak başlatılabilmeli ve durumları izlenebilmelidir.
- **FR-26.04:** Acil durum, ders, sınav, ring, yemekhane, ödeme ve destek bildirimleri tek bildirim merkezinden yönetilmelidir.

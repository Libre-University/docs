# Modüller

> **Proje ilkesi:** LibreUniversity; kapalı kutu, kaynak kodu teslim edilmeyen, üniversiteyi tek firmaya veya lisans sunucusuna bağımlı bırakan sistemlerden kaçınmak için özgür yazılım, açık standartlar, self-hosted kurulum ve tedarikçi bağımsızlığı ilkeleriyle geliştirilecektir. Zorunlu dış entegrasyonlar çekirdek mimariye gömülmeyecek, adapter katmanında izole edilecektir.

### 1. Çok Kiracılı Web ve İçerik Yönetim Sistemi (Multi-Tenant CMS)

_Milyonlarca ziyaretçiyi kaldıracak, tüm birimlerin kendi sitelerini yönetebileceği ana omurga._

- **Ana Portal:** Üniversitenin ana web sitesi (Haberler, duyurular, etkinlik takvimi).
    
- **Fakülte/Enstitü/Yüksekokul Siteleri:** Her akademik birim için kurumsal kimliğe uygun, alt alan adıyla (örn. _muhendislik.universite.edu.tr_) çalışan bağımsız ama merkeze bağlı siteler.
    
- **Akademik Kişisel Sayfalar (CV/Profil Siteleri):** Her akademisyen için dinamik olarak oluşturulan, yayınlarının ve verdiği derslerin otomatik çekildiği kişisel web sayfaları.
    
- **Öğrenci Kulübü Siteleri:** SKS (Sağlık, Kültür, Spor) Daire Başkanlığı onaylı, kulüplerin etkinliklerini duyurduğu alt siteler.
    
- **Laboratuvar ve Araştırma Merkezi Siteleri:** Spesifik araştırma projeleri için izole sayfalar.

### 2. Çekirdek Öğrenci Bilgi Sistemi (Core SIS / OBS)

_Öğrencinin üniversiteye adım atmasından mezuniyetine kadar olan resmi süreçleri._

- **Aday ve Kabul Modülü:** Lise tanıtım CRM'i, YKS/YÖS başvuru portali, yabancı uyruklu evrak doğrulama ve kesin kayıt.
    
- **Katalog ve Müfredat Yöneticisi:** Bölüm, program, AKTS, ön-koşul/bağlı ders konfigürasyonları.
    
- **Ders Kayıt ve Çakışma Motoru:** 50.000 öğrencinin aynı anda sisteme girdiği anlarda çökmeyi engelleyen sıraya alma (queue) algoritmalı kayıt modülü ve mekan/saat çakışma engelleyici.
    
- **Not ve Değerlendirme Modülü:** Ara sınav, final, mazeret notu girişleri; çan eğrisi, harf notu hesaplama ve not itiraz (maddi hata) iş akışları.
    
- **Yoklama ve Devamsızlık Modülü:** NFC veya mobil uygulama üzerinden (QR kod ile) yoklama çekme ve devamsızlık sınırı uyarısı.
    
- **Staj ve İntibak Yöneticisi:** Ders saydırma, muafiyet işlemleri, staj yeri onay ve defter değerlendirme süreçleri.
    
- **Mezuniyet ve Belge Modülü:** E-imzalı anlık transkript, öğrenci belgesi üretimi, diploma eki (Diploma Supplement) ve mezuniyet komisyonu algoritmaları.
    

### 3. Dijital Kampüs Eğitim Ağacı (LMS & EdTech) — Jitsi Entegreli

- **Öğrenme Yönetim Modülü (LMS):** Haftalık ders izlencesi, asenkron video/PDF materyal paylaşımı, şube bazlı etkileşimli tartışma forumları ve duyuru panosu.
    
- **Jitsi Tabanlı Canlı Ders ve VOD Altyapısı:**
    
    - **Gömülü Sanal Sınıf (Jitsi IFrame API):** Dış bir uygulamaya (Zoom/Teams gibi) yönlendirme yapmadan, LMS arayüzü içinde doğrudan çalışan tarayıcı tabanlı sanal sınıflar.
        
    - **Dinamik Yetkilendirme (JWT & SSO Entegrasyonu):** Üniversitenin merkezi kimlik yönetiminden (IAM/SSO) üretilen token'lar ile hocalara otomatik "Oda Moderatörü", öğrencilere ise dinleyici/katılımcı rolleri atanması; odaya yetkisiz girişlerin (zoombombing) engellenmesi.
        
    - **Kayıt ve Otomasyon Motoru (Jibri):** Jitsi'nin açık kaynak kayıt servisi (Jibri) ile oturumların otomatik başlatılması, ham kayıtların okulun yerel **MinIO (S3)** nesne depolama sunucusuna aktarılması.
        
    - **Arka Plan VOD Pipeline:** Ders bittiğinde kaydın FFmpeg işçileriyle MP4/HLS formatına sıkıştırılması ve LMS üzerindeki ilgili haftanın ders izlencesine "Geçmiş Ders Kaydı" olarak otomatik eklenmesi.
        
    - **Ölçeklenebilir SFU Havuzu (Jitsi Videobridge - JVB):** Eşzamanlı açılan yüzlerce sınıfı kampüs içi sunucularda donma ve kesinti olmadan dağıtan yatay ölçekli JVB düğümleri.
        
- **Online Ölçme ve Değerlendirme:** Güvenli tarayıcı kilidi (Safe Exam Browser - SEB), soru bankasından şube ve öğrenci bazlı rastgele soru havuzu oluşturma, süre kısıtlı çevrimiçi sınavlar ve otomatik notlandırma.
    
- **Ödev ve İntihal Denetimi:** Öğrenci proje/kod teslim portali, geç teslim cezalandırma algoritmaları ve açık kaynak benzerlik/intihal denetim araçlarıyla otomatik kontrol.

### 4. Akademik Araştırma ve BAP (Araştırma Bilgi Sistemi)

- **Akademik Veri Yönetim Sistemi:** Akademisyenlerin makale, patent, bildiri, kitap, atıf verilerinin tutulduğu, YÖKSİS ile entegre performans ve teşvik hesaplama modülü.
    
- **BAP (Bilimsel Araştırma Projeleri):** Kurum içi araştırma fonu başvuru, hakem değerlendirme, bütçe serbest bırakma ve ara rapor onaylama iş akışları.
    
- **Etik Kurul Modülü:** İnsan ve hayvan araştırmaları için etik kurul onayı başvuru ve karar takip sistemi.
    
- **Teknoloji Transfer Ofisi (TTO) Modülü:** Üniversite-Sanayi işbirlikleri, patent başvuruları ve kuluçka merkezi firma takibi.
    

### 5. Akıllı Kampüs ve Yaşam (Smart Campus & IoT)

- **Kampüs Kartı ve Fiziksel Geçiş Kontrolü:** Turnikeler, otopark bariyerleri ve laboratuvar kapıları için RFID, NFC veya plaka tanıma entegrasyonu; merkezi kimlik yönetimiyle yetki senkronizasyonu.
    
- **Yurt Yönetim Modülü:** 50.000 öğrencinin yatak/oda kapasite planlaması, online yurt başvurusu, izin işlemleri ve yurt aidat tahsilatları.
    
- **Yemekhane ve Kafeterya Modülü:** Kampüs kartına online para yükleme, günlük kalori bazlı menü gösterimi, öğün rezervasyonu ve gişe/turnike düşüm sistemi.
    
- **Ulaşım ve Ring Takibi:** Kampüs içi ring otobüslerinin anlık GPS konumlarının öğrencilere mobil uygulamadan gösterilmesi.
    
- **Tesis ve Mekan Rezervasyonu:** Halı saha, tenis kortu, konferans salonu, kütüphane çalışma odası randevu ve kiralama modülü.
    
- **Sağlık ve Mediko Modülü:** Kampüs içi revir randevuları, psikolojik danışmanlık merkezi işleyişi ve öğrenci sağlık kayıtları.
    

### 6. Kurumsal Yönetim ve ERP (İdari/Mali İşler)

- **Öğrenci Finans Modülü:** Harç, yaz okulu ücreti, yurt ve yemekhane ödemeleri için açık sözleşmeli banka/sanal POS adapter entegrasyonları, taksitlendirme ve burs indirim oranları.
    
- **İnsan Kaynakları ve Bordro (İK):** Akademik ve idari personelin özlük dosyaları, izin/rapor/nöbet takibi ve maaş/bordro yönetimi (Devlet üniversitesi ise Maliye KBS entegrasyonu).
    
- **Satın Alma ve İhale:** Doğrudan temin, e-teklif, ihale komisyon onayları.
    
- **Taşınır/Demirbaş (Envanter) Modülü:** Bilgisayarlardan laboratuvar cihazlarına kadar tüm demirbaşların barkodlanması, zimmetlenmesi ve amortisman takibi.
    
- **EBYS (Elektronik Belge Yönetim Sistemi):** Üniversite içi ve dışı tüm resmi evrak akışının, e-İmza ve KEP (Kayıtlı Elektronik Posta) ile kağıtsız yönetilmesi.
    

### 7. Kütüphane ve Dokümantasyon (ILS)

- **Kütüphane Otomasyonu:** Kitap/dergi kataloglama, ödünç/iade, gecikme cezası ve rezerve işlemleri (RFID kapı sistemleriyle entegre).
    
- **Dijital Kütüphane ve Proxy:** Öğrencilerin ve akademisyenlerin kampüs dışından uluslararası makale veritabanlarına (IEEE, Elsevier vb.) güvenli erişim portalı.
    

### 8. İletişim, Destek ve Topluluk (Helpdesk & Alumni)

- **Destek Masası (Ticketing):** Öğrenci işleri, bilgi işlem, temizlik veya teknik servis talepleri için anlık bilet oluşturma ve SLA (çözüm süresi) takibi.
    
- **Çoklu Kanal İletişim Merkezi (Omnichannel):** Tüm öğrencilere veya spesifik bir gruba (örn. "sadece 3. sınıf makine mühendislerine") anlık SMS, E-posta, Mobil Push bildirimi veya anket gönderme modülü.
    
- **Mezunlar Ağı (Alumni):** Mezun bilgi sistemi, kariyer merkezi iş/staj ilanları panosu ve mezun bağış/fon yönetimi.
    

### 9. Arka Plan Güvenlik ve Mimari Modülleri (System Core)

- **SSO (Single Sign-On):** Öğrencinin "Öğrenci Numarası ve Şifre" ile giriş yapıp, bir daha şifre girmeden LMS, OBS, Web siteleri, Yemekhane ve Eduroam Wi-Fi sistemine otomatik bağlanmasını sağlayan merkezi kimlik yönetimi (Keycloak gibi özgür bir kimlik sağlayıcı; mevcut LDAP/Active Directory dizinleri yalnızca adapter üzerinden kaynak olarak bağlanabilir).
    
- **Veri Ambarı ve İş Zekası (BI):** Yönetim (Rektörlük) için raporlama ekranları; Hangi fakülte ne kadar bütçe yaktı? Hangi derste kalma oranı yüksek? Üniversite geneli doluluk oranları nedir?
    
- **API Gateway:** Diğer modüllerin birbiriyle ve devlet sistemleriyle (e-Devlet, YÖKSİS, SGK, MERNİS, ÖSYM) veri alışverişini güvenli bir şekilde yöneten kapı.
    
- **Log, Denetim İzi ve KVKK Yönetimi:** Kimin, hangi nota ne zaman müdahale ettiğini ve kimin hangi veriyi indirdiğini değiştirilmez şekilde kaydeden güvenlik denetim izleri; veri saklama, açık rıza, maskeleme ve silme/anonimleştirme süreçleri.

### 10. Siber Güvenlik, SOC ve Gözetlenebilirlik (Observability)

Sistem çekirdeğinde (9. Madde) log yönetimi var ancak 50.000 cihazın bağlandığı bir ağda proaktif güvenlik ve anomali tespiti için ayrı bir katman şarttır.

- **SIEM ve Tehdit Avcılığı:** Kampüs içi ağ trafiği, IAM/SSO giriş denemeleri ve sunucu loglarının merkezi olarak (örneğin Wazuh gibi açık kaynak araçlarla) izlenmesi.
    
- **Ağ Seviyesi Gözetlenebilirlik:** Sunuculardaki yoğun trafiği ve potansiyel DDoS/Ransomware saldırılarını çekirdek seviyesinde (eBPF/XDP destekli araçlarla) paket düşürerek analiz etme ve engelleme.
    
- **Zafiyet Yönetimi:** Geliştirdiğiniz tüm bu mikroservislerin ve fakülte web sitelerinin düzenli olarak otomatik zafiyet taramalarından geçirilmesi.
    

### 11. Kalite, Akreditasyon ve Stratejik Planlama Modülü

Üniversitelerin YÖKAK (Yükseköğretim Kalite Kurulu) ve MÜDEK, ABET gibi kurumlara her yıl devasa raporlar sunması gerekir.

- **Özdeğerlendirme ve KPI Takibi:** Üniversitenin stratejik hedeflerinin (örn. "Bu yıl SCI endeksli makale sayısını %20 artırmak") fakülte ve bölüm bazlı gerçekleşme oranlarının takibi.
    
- **Anket ve Geri Bildirim Yönetimi:** 360 derece değerlendirme (Öğrencinin hocayı, personelin yönetimi değerlendirmesi) ve ders kalite anketleri.
    
- **Müfredat Haritalama:** Hangi dersin hangi program çıktısını (mühendislik etiği, analitik düşünme vb.) ne kadar sağladığının matrislerle kanıtlanması.
    

### 12. Uluslararası İlişkiler ve Değişim Programları (Mobility)

Erasmus, Farabi, Mevlana gibi değişim programları OBS'den ayrı, ciddi bir bütçe ve ikili anlaşma yönetimi gerektirir.

- **İkili Anlaşmalar Veritabanı:** Hangi Avrupa üniversitesiyle kaç kişilik kontenjan anlaşması var, anlaşma süresi ne zaman doluyor?
    
- **Hibe (Grant) Yönetimi:** Giden öğrenci/personele verilecek Avrupa Birliği hibelerinin hesaplanması, banka entegrasyonu ile ödenmesi ve kesintilerin takibi.
    
- **Gelen Öğrenci (Incoming) Portali:** Yurt dışından gelecek öğrencilerin henüz OBS'ye kayıt olmadan önceki başvuru, vize evrakı kabulü ve oryantasyon süreçleri.
    

### 13. Sürekli Eğitim Merkezi (SEM) / Yaşam Boyu Öğrenme

Üniversitenin sadece kendi öğrencilerine değil, dışarıdaki vatandaşlara da ücretli eğitim satarak gelir elde ettiği modüldür.

- **B2C Eğitim E-Ticaret Portali:** Vatandaşların kredi kartıyla dışarıdan online/yüz yüze sertifika programı (örn. "İleri Düzey Excel", "Siber Güvenlik Kampı") satın alabildiği vitrin.
    
- **Sertifikasyon ve e-Devlet Entegrasyonu:** Eğitim bittiğinde e-imzalı, QR kodlu ve doğrudan e-Devlet'e (Sertifikalarım bölümüne) düşen resmi evrak üretimi.
    

### 14. Kariyer Merkezi ve Yetenek Yönetimi

Mezun ağından (Alumni) farklı olarak, aktif öğrencilerin iş dünyasıyla buluşturulduğu aktif modüldür.

- **İşveren Portali:** Şirketlerin üniversite sistemine kayıt olup (İK onayıyla) doğrudan öğrencilere özel staj ve part-time iş ilanı açabilmesi.
    
- **Yetenek Havuzu ve Eşleştirme:** Öğrencilerin CV'lerindeki yetkinliklerle (örn. Python, C, Go), şirketlerin aradığı niteliklerin algoritma ile eşleştirilip öğrenciye bildirim atılması.
    
- **Cumhurbaşkanlığı Yetenek Kapısı Entegrasyonu:** Türkiye'deki zorunlu Ulusal Staj Programı verilerinin üniversite sistemine çift yönlü aktarımı.

### 15. Üniversite Hastanesi ve Klinik Yönetimi (HBYS/Diş)

50.000 nüfuslu bir üniversitenin Tıp veya Diş Hekimliği fakültesi (ve araştırma hastanesi) olma ihtimali %99'dur. Hastane süreçleri, standart üniversite işleyişinden tamamen farklıdır.

- **HBYS (Hastane Bilgi Yönetim Sistemi):** Hasta randevu, poliklinik, ameliyathane, eczane ve laboratuvar yönetim modülleri.
    
- **Stajyer ve Asistan Doktor Entegrasyonu:** Tıp öğrencilerinin intörn nöbetleri, vaka log defterleri (Logbook) ve hasta verilerine yetki kısıtlamalı (anonimleştirilmiş) erişimi.
    
- **Sağlık Bakanlığı ve SGK Entegrasyonları:** e-Nabız, Medula (fatura kesimi) ve HL7/FHIR standartlarında sağlık verisi haberleşme protokolleri.
    

### 16. Hukuk Müşavirliği ve Disiplin Otomasyonu

Büyük üniversitelerde her yıl yüzlerce sözleşme imzalanır, davalar açılır ve disiplin soruşturmaları yürütülür. Bu veriler standart EBYS'de tutulamayacak kadar gizlidir.

- **Dava ve İcra Takibi:** Üniversitenin taraf olduğu davaların, duruşma günlerinin ve UYAP (Ulusal Yargı Ağı Bilişim Sistemi) entegrasyonu ile resmi evraklarının takibi.
    
- **Disiplin Soruşturmaları Yönetimi:** Öğrenci (kopya, kavgaya karışma) veya personel (görev ihlali) disiplin kurullarının toplanması, savunma isteme süreçleri ve YÖKSİS ceza bildirimleri.
    
- **Sözleşme Yaşam Döngüsü:** Dış firmalarla yapılan satın alma sözleşmelerinin hukuki onay ve yenilenme süreçleri.
    

### 17. Kampüs GIS (Coğrafi Bilgi Sistemi) ve Dijital İkiz

Devasa bir kampüsün sadece binalarını değil, yeraltı ve yerüstü tüm fiziksel altyapısını yönetmek gerekir.

- **Altyapı Haritalama:** Kampüsün yeraltı fiber optik kablo hatları, su ve doğalgaz borularının dijital harita (GIS) üzerinde tutulması (olası bir kazıda fiberin kopmasını önlemek için).
    
- **İç Mekan Navigasyonu (Indoor Routing):** Yeni gelen bir öğrencinin, mobil uygulamayı kullanarak "B Blok 3. Kat 304 Nolu Laboratuvarı" bulmasını sağlayan 3D harita ve yönlendirme sistemi.
    
- **Bina Enerji Yönetimi:** Akıllı sayaçlarla entegre olarak hangi fakültenin ne kadar elektrik/su tükettiğini gösteren anlık kontrol paneli.
    

### 18. Engelsiz Üniversite ve Kapsayıcılık Modülü

Dezavantajlı öğrencilerin (görme, işitme veya bedensel engelli) üniversite yaşamına adaptasyonu kanuni bir zorunluluktur.

- **Sınav Uyarlamaları:** Engelli öğrenci OBS'den sınav talep ettiğinde; ek süre tanınması, okuyucu/işaretleyici personel atanması veya sınav kağıdının Braille/Büyük punto basılması için otomatik iş akışları.
    
- **Fiziksel Erişim Haritası:** Kampüs GIS modülüyle entegre çalışarak, tekerlekli sandalyeye uygun rotaların ve asansörlü binaların mobil uygulamada filtrelenebilmesi.
    

### 19. Merkezi Baskı ve Doküman Yönetimi (Follow-Me Printing)

50.000 öğrenci ve binlerce personelin kampüs içindeki yazıcı (printer) kullanımı ciddi bir maliyet ve güvenlik kalemidir.

- **Kota ve Kredi Sistemi:** Her öğrenciye dönemlik 100 sayfa ücretsiz baskı kotası tanımlanması, aşımında kampüs kartından (sanal POS ile) bakiye düşülmesi.
    
- **Güvenli Baskı (Follow-Me):** Öğrenci bilgisayarından/telefonundan çıktıyı gönderir ancak kağıt hemen basılmaz. Hangi fakültedeki yazıcının yanına gidip öğrenci kartını okutursa (RFID), çıktı o an o makineden alınır; altyapı CUPS ve açık protokol tabanlı özgür yazılım bileşenleriyle kurulmalıdır.
    

### 20. Etkinlik, Kongre ve Dış Misafir Yönetimi (Event & Ticketing)

Bahar şenlikleri, uluslararası akademik kongreler ve mezuniyet törenleri kampüse on binlerce "dış misafir" çeker.

- **Biletleme ve LCV:** Etkinlikler için QR kodlu dijital bilet üretimi ve koltuk rezervasyonu.
    
- **Ziyaretçi Geçiş Kontrolü:** Etkinliğe dışarıdan gelen misafirlerin T.C. Kimlik doğrulaması ile turnikelerden (kampüs güvenlik kapılarından) süreli/kısıtlı geçiş yapabilmesi için tek kullanımlık QR kod entegrasyonu.

### 21. Teknoloji Geliştirme Bölgesi (Teknokent / Teknopark) Yönetimi

Büyük üniversitelerin kampüsünde, vergi muafiyeti ile çalışan yüzlerce Ar-Ge firması bulunur. Bu firmalar üniversite öğrencisi veya personeli değildir ama kampüsü kullanırlar.

- **Firma ve Proje Kabul Süreçleri:** Teknokent'e başvuran şirketlerin hakem heyeti (akademisyenler) tarafından değerlendirilmesi.
    
- **Sanayi ve Teknoloji Bakanlığı Entegrasyonu:** Firmaların Ar-Ge projelerinin, personel muafiyet sürelerinin ve giriş-çıkış loglarının (turnike verilerinin) bakanlık portaline API ile otomatik basılması.
    
- **Kuluçka (Incubation) Fonu:** Öğrenci girişimlerine (start-up) tahsis edilen ofislerin ve melek yatırımcı görüşmelerinin takibi.

### 22. Taşınmaz, Ticari Alan ve Lojman (Emlak) Yönetimi

Kampüsteki kafeler, bankamatikler (ATM), kuaförler ve kırtasiyeler üniversiteye kira öder. Ayrıca akademisyenlere ev (lojman) tahsis edilir.

- **Sözleşme ve Kira Takibi:** Kampüsteki ticari işletmelerin sözleşme bitiş tarihleri, ciro üzerinden alınan kira payları ve banka entegrasyonu ile otomatik tahsilat/gecikme ihbarnamesi.
    
- **Lojman Puanlama Algoritması:** Hangi akademisyenin lojmana yerleşeceğini belirleyen (hizmet yılı, unvan, medeni durum, çocuk sayısı) otomatik puanlama ve sıra bekleme sistemi.
    

### 23. Araç Filosu, İş Makinesi ve Lojistik Yönetimi

Böyle bir üniversitenin kendi otobüsleri, rektörlük makam araçları, çöp kamyonları, kar küreme araçları ve hatta traktörleri vardır.

- **Taşıt Tanıma (Akaryakıt) ve GPS:** Hangi aracın nerede olduğu, ne kadar yakıt tükettiği (Petrol şirketlerinin taşıt tanıma sistemleriyle entegre).
    
- **Şoför Vardiya ve Görevlendirme:** Araç taleplerinin (örn. "Kazı alanına gitmek için arkeoloji bölümüne arazi aracı lazım") toplanması, şoför atanması ve harcırah hesaplanması.
    
- **Periyodik Bakım ve Muayene:** Filodaki araçların kasko, sigorta, TÜVTÜRK muayenesi ve sanayi onarım süreçleri.
    

### 24. İş Sağlığı ve Güvenliği (İSG) ile Afet Yönetimi

Laboratuvarlarda tehlikeli kimyasallar kullanılır, inşaatlar yapılır. Olası bir kazada veya depremde kriz yönetimi şarttır.

- **Risk Değerlendirme ve Ramak Kala:** Kampüsteki tüm binaların (yangın tüpü tarihleri, asansör bakımları) İSG uzmanları tarafından dijital formlarla denetlenmesi.
    
- **Afet ve Kriz İletişimi:** Olası bir deprem anında kampüsteki (turnike veya Wi-Fi verisine göre) mevcut 35.000 kişiye lokasyon bazlı SMS/Push bildirim atılması ve toplanma alanlarının GIS haritasında gösterilmesi.
    
- **Kimyasal Atık Yönetimi:** Mühendislik/Tıp laboratuvarlarından çıkan tıbbi/kimyasal atıkların bertaraf firmalarına teslim logları.
    



### 25. Fiziksel Arşiv, Müze ve Kültür Varlıkları Yönetimi

Üniversitenin 50 yıllık geçmişi, milyonlarca kağıt evrak ve muhtemelen dekanlıklara/bölümlere ait küçük müzeler barındırır.

- **Kutu ve Raf (Barkod/RFID) Navigasyonu:** "1998 yılı Makine Mühendisliği mezuniyet tutanakları"nın arşivin hangi dehlizinde, hangi rafın kaçıncı kutusunda olduğunun 3D olarak haritalanması.
    
- **Dijitalleştirme (OCR) Boru Hattı:** Eski evrakların taranıp, yapay zeka (OCR/Tesseract) ile indekslenerek Elasticsearch/Meilisearch üzerinde tam metin (full-text) aranabilir hale getirilmesi.
    
- **Envanter ve Restorasyon:** Üniversiteye bağışlanan tarihi tablolar, heykeller veya antika cihazların sigorta değerleri ve restorasyon tarihleri.

### 26. Mobil Uygulama ve Self-Servis Portal

Birçok modülün öğrenci, akademisyen, personel ve dış paydaş tarafındaki gündelik kullanım yüzüdür.

- **Rol Bazlı Mobil Ana Sayfa:** Öğrenci, akademisyen, idari personel, mezun ve misafir kullanıcıların kendi süreçlerine uygun ders, duyuru, ödeme, randevu ve bildirim özetlerini görmesi.

- **Anlık Bildirim ve İşlem Merkezi:** OBS, LMS, yemekhane, ring, etkinlik, destek masası ve acil durum bildirimlerinin tek merkezden takip edilmesi.

- **Dijital Kampüs Kartı:** QR/NFC destekli kimlik, yemekhane geçişi, kütüphane işlemleri, etkinlik bileti ve fiziksel geçiş süreçlerinde kullanılabilecek mobil kimlik.

- **Self-Servis Başvurular:** Belge talebi, izin/randevu, yurt, burs, ders itirazı, teknik destek ve etkinlik başvurularının mobil/web üzerinden başlatılması ve durum takibi.

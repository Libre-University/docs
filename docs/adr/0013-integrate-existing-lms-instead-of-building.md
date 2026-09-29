# ADR-0013: MVP'de LMS Sıfırdan Yazılmasın, Mevcut Özgür LMS'e Entegre Olunsun

## Durum

Önerildi.

Karar verenler: Kurucu önerisi; öneri sahibi @Aybavs. Tartışma: [module-lms#7](https://github.com/Libre-University/module-lms/issues/7), [docs#2](https://github.com/Libre-University/docs/issues/2).

## Bağlam

[MVP_SCOPE.md](../../MVP_SCOPE.md) LMS çekirdeğini (ders sayfası, materyal, duyuru, ödev, canlı ders) sıfırdan yazmayı öngörüyordu. Bu alanda olgun özgür yazılımlar vardır: Moodle (GPL-3.0) self-hosted çalışır, LTI 1.3 destekler, BigBlueButton entegrasyonu 4.0'dan beri çekirdektedir, Jitsi eklentisi mevcuttur ve Türkiye'deki üniversitelerin büyük bölümünde zaten kuruludur.

Projenin özgün değeri OBS'dedir: Türkiye'de özgür bir OBS alternatifi yoktur ve YÖKSİS, ÖSYM gibi entegrasyonlar burada gerekir. Sınırlı emeği OBS ile LMS arasında bölmek, ikisini de geciktirir.

## Karar

MVP'de LMS sıfırdan yazılmaz. LibreUniversity, mevcut bir özgür LMS'e entegre olur; ilk ve varsayılan hedef **Moodle**'dır.

### Kapsam

- `adapters` içinde bir `LearningPlatform` portu tanımlanır; ilk uygulama Moodle adapteridir. [ADR-0007](0007-isolate-external-systems-with-adapters.md) ile uyumludur; başka LMS'ler sonradan eklenebilir.
- **OBS → LMS:** Dönem, şube ve kayıt verisinin LMS'e senkronizasyonu (ders ve katılımcı oluşturma, kayıt değişikliklerinin yansıtılması).
- **Kimlik:** LMS, Keycloak üzerinden OIDC/SAML ile aynı SSO'yu kullanır ([ADR-0006](0006-use-open-identity-provider-adapter.md)).
- **LMS → OBS:** Ödev ve sınav sonuçlarının OBS'ye aktarımı; LTI 1.3 Assignment and Grade Services veya Moodle web servisleri.
- **Canlı ders:** LMS tarafında yürütülür (Moodle'da BigBlueButton veya Jitsi). `LiveClassroom` portu ve Jitsi/BigBlueButton adapterleri MVP kapsamından çıkar; yerli LMS yazılırsa geri gelir.
- `module-lms` "LMS entegrasyon modülü" olarak yeniden tanımlanır: senkronizasyon durumu, ders-şube eşleştirmesi ve not aktarım kayıtlarını tutar.

### Veri sahipliği

- Kayıt, ders sonucu ve transkript verisinin sahibi OBS'dir.
- Ders içeriği, materyal, forum, ödev ve ödev teslimlerinin sahibi LMS'dir.
- Hangi alanların hangi yöne aktarılacağı [DATA_MODEL.md](../../DATA_MODEL.md) veri sahipliği tablosunda tanımlanır. Öğrenci ve not verisi iki sistem arasında aktığı için KVKK etkisi vardır; aktarılan alanlar asgaride tutulur.

### Yerli LMS kararı

Kendi LMS'ini yazma kararı, entegrasyonun karşılayamadığı somut ihtiyaçlar ortaya çıktığında ayrı bir ADR ile alınır.

## Sonuçlar

- OBS'ye ayrılan emek artar; MVP'nin en zor ve en özgün parçasına odaklanılır.
- Canlı ders, VOD ve online sınav sorunları MVP'de LMS tarafında çözülmüş olur.
- **Bedel:** Moodle PHP tabanlıdır; ikinci bir yığın işletilir. Türkiye'deki çoğu üniversite Moodle'ı zaten işlettiği için pilot kurumlarda bu bedel büyük ölçüde sıfırdır, ancak sıfırdan kuran bir kurum için ek bileşendir.
- **Bedel:** Tek arayüz vizyonundan MVP'de taviz verilir; öğrenci ders içeriği için LMS'e geçer. Mobil uygulama ilk aşamada LMS'e derin bağlantı verir.
- Senkronizasyon hataları, tekrar deneme ve mutabakat raporu gereksinimleri (NFR-08.03) bu entegrasyon için geçerlidir.
- Etkilenen belgeler: MVP_SCOPE (LMS bölümü), ROADMAP (Faz 3, `module-lms`, `adapters`, `deploy` satırları), UML (canlı ders diyagramı), adapters README. Bu güncellemeler ADR kabul edildikten sonra ayrı PR ile yapılır.

## Değerlendirilen Alternatifler

- **Sıfırdan LMS (mevcut plan):** Tam kontrol ve tek arayüz; ancak yıllar sürecek bir işi OBS ile paralel yürütmek demek.
- **Başka bir özgür LMS (Canvas LMS AGPL, Open edX AGPL, ILIAS GPL):** Lisans olarak uygun; Moodle Türkiye'deki yaygınlığı, Türkçe yerelleştirmesi ve mevcut kurulum tabanı nedeniyle tercih edildi. Port tasarımı diğerlerini dışlamaz.
- **Yalnızca LTI ile bağlanmak, senkronizasyon yapmamak:** Daha az iş; ancak ders ve katılımcı oluşturma OBS'nin sorumluluğunda kalmalı, aksi halde iki sistemde çift veri girişi doğar.

## İlgili Dokümanlar

- [MVP_SCOPE.md](../../MVP_SCOPE.md)
- [MODULES.md](../../MODULES.md) §3
- [FUNCTIONAL_REQUIREMENTS.md](../../FUNCTIONAL_REQUIREMENTS.md) FR-03
- [ADR-0006](0006-use-open-identity-provider-adapter.md)
- [ADR-0007](0007-isolate-external-systems-with-adapters.md)

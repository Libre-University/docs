# LibreUniversity

LibreUniversity; üniversitelerin kapalı kutu, pahalı, denetlenemeyen ve tek tedarikçiye bağımlı dijital sistemlere mahkum olmaması için tasarlanan özgür yazılım tabanlı bir dijital kampüs projesidir.

Amacımız yalnızca bir öğrenci bilgi sistemi yazmak değildir. Üniversitenin web sitesi, OBS, LMS, canlı ders, belge yönetimi, ödeme, yurt, yemekhane, kütüphane, destek masası, kalite, araştırma, güvenlik, raporlama ve mobil self-servis süreçlerini özgür, denetlenebilir ve toplulukla geliştirilebilir bir ekosistem halinde kurmaktır.

## Neden?

Birçok üniversite, ne yaptığını tam göremediği kapalı sistemlere yüksek bedeller öder. Verisini dışarı çıkarmakta zorlanır, kaynak koda erişemez, küçük bir değişiklik için firmaya bağımlı kalır ve yıllar içinde kurumsal hafızasını yazılım tedarikçilerine teslim eder.

LibreUniversity bu döngüyü kırmak ister:

- Üniversitenin verisi üniversitede kalmalı.
- Kaynak kod denetlenebilir olmalı.
- Sistem self-hosted çalışabilmeli.
- Kritik modüller kapalı kaynak SaaS ürünlerine bağlı olmamalı.
- Öğrenciler, akademisyenler, geliştiriciler ve idari personel birlikte katkı verebilmeli.

## Temel İlkeler

- Özgür yazılım ve açık standartlar.
- Kapalı kutu kritik bileşenlere bağımlı olmama.
- Tek tedarikçi kilidine karşı mimari.
- Üniversite içinde kurulabilir, taşınabilir ve denetlenebilir sistem.
- Toplulukla geliştirilen şeffaf karar süreçleri.
- KVKK, güvenlik, erişilebilirlik ve kamu yararı odağı.

## Bu Repo (docs)

Bu repo projenin vizyon, gereksinim, mimari, veri modeli, ADR ve ana yol haritası belgelerinin tek kaynağıdır. Organizasyon genelindeki etiket seti de burada tutulur ([org-labels.yml](org-labels.yml)).

| Faz | Bu repoda yapılacaklar |
| --- | --- |
| Faz 0 | Lisans kararı, ADR-0004/0005/0006/0008/0009/0010'un kabulü, katkıcı karşılama belgeleri, sözlük |
| Faz 1 | API sözleşme ilkeleri, yetki modeli ve audit olay kataloğu belgeleri |
| Faz 2 | Ders kayıt, danışman onayı ve not süreçlerinin ayrıntılı analizleri |
| Faz 3 | LMS ve mobil kullanıcı kılavuzları |
| Faz 4+ | Kurumsal modüller (finans, EBYS, yurt, yemekhane) analizleri |

## Repolar

Proje [`libre-university`](https://github.com/libre-university) organizasyonunda katmanlara göre ayrılmış repolarda geliştirilir. Liste ve faz sorumlulukları için [Yol Haritası](ROADMAP.md) belgesine bakın.

## Mevcut Dokümanlar

- [Mimari İlkeler](ARCHITECTURAL_PRINCIPLES.md)
- [Modüller](MODULES.md)
- [Fonksiyonel Gereksinimler](FUNCTIONAL_REQUIREMENTS.md)
- [Fonksiyonel Olmayan Gereksinimler](NON_FUNCTIONAL_REQUIREMENTS.md)
- [Yol Haritası](ROADMAP.md)
- [MVP Kapsamı](MVP_SCOPE.md)
- [MVP UML Diyagramları](UML.md)
- [MVP Veri Modeli](DATA_MODEL.md)
- [Mimari Karar Kayıtları](docs/adr/)
- [Topluluk](COMMUNITY.md)
- [Katkı Rehberi](CONTRIBUTING.md)
- [Yönetişim](GOVERNANCE.md)
- [Açık Kaynak Politikası](OPEN_SOURCE_POLICY.md)
- [Lisans Önerisi](LICENSE_PROPOSAL.md)
- [Güvenlik Politikası](SECURITY.md)

## Kimler Katkı Verebilir?

- Üniversite öğrencileri.
- Akademisyenler.
- Bilgi işlem ekipleri.
- Yazılım geliştiriciler.
- Tasarımcılar.
- Sistem yöneticileri.
- KVKK, hukuk, kalite ve akreditasyon uzmanları.
- Öğrenci işleri, kütüphane, yurt, yemekhane, mali işler ve idari birim çalışanları.

Kod yazmak şart değil. Süreç bilgisi, dokümantasyon, test, tasarım, çeviri, güvenlik incelemesi ve gerçek üniversite deneyimi de katkıdır.

## Başlangıç Durumu

Proje henüz fikir ve analiz aşamasındadır. İlk hedef; güçlü bir topluluk zemini, net MVP kapsamı, açık mimari kararlar ve geliştirilebilir bir çekirdek oluşturmaktır.

## Lisans

Lisans kararı topluluk tarafından kesinleştirilecektir. Varsayılan öneri, ağ üzerinden hizmet olarak sunulan türevlerin de özgür kalmasını sağlamak için **AGPL-3.0-or-later** lisansıdır.

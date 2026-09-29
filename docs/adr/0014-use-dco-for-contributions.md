# ADR-0014: Katkılar İçin DCO Kullanılsın, CLA İstenmesin

## Durum

Önerildi.

Karar verenler: Kurucu önerisi; öneri sahibi @Aybavs. Tartışma: [docs#13](https://github.com/Libre-University/docs/issues/13), [docs#2](https://github.com/Libre-University/docs/issues/2).

## Bağlam

[ADR-0002](0002-prefer-agpl-3-or-later-license.md) lisansı AGPL-3.0-or-later olarak kesinleştirdi ancak katkıcı sözleşmesi sorusunu açık bıraktı. Bu karar ilk dış katkı birleştirilmeden verilmelidir; geriye dönük uygulanamaz.

Mekanizma yoksa her katkıcı kendi katkısının telif sahibi olarak kalır. "or-later" sayesinde AGPL'nin gelecek sürümlerine geçiş mümkündür; ancak farklı bir lisansa geçmek veya telifi ileride kurulacak bir tüzel kişiye devretmek tüm katkıcıların onayını gerektirir. Üniversiteler ve kamu kurumları kodu alırken katkıcıların bu kodu verme hakkı olduğunu sorabilir.

## Karar

- Katkılar için **Developer Certificate of Origin (DCO) 1.1** kullanılır. Her commit `Signed-off-by: Ad Soyad <e-posta>` satırı taşır (`git commit -s`).
- DCO kontrolü CI'da otomatik yapılır; imzasız commit içeren PR birleştirilemez. Kontrol için hazır GitHub Action veya DCO uygulaması kullanılır (kapalı kaynak bağımlılık yaratmayan seçenek tercih edilir).
- **CLA istenmez.** İmzalatacak bir tüzel kişi yoktur ve CLA katkı eşiğini yükseltir. İleride bir vakıf veya dernek kurulursa CLA ayrı bir ADR ile yeniden değerlendirilir.
- `CONTRIBUTING.md` DCO açıklaması, `git commit -s` kullanımı ve DCO metnine bağlantı içerir.
- **Kamu personeli notu:** Akademisyen ve bilgi işlem çalışanı gibi kamu personelinin görev kapsamında ürettiği kodun hakları kurumuna ait olabilir. `CONTRIBUTING.md` bu katkıcıları uyarır ve işverenlerinden izin aldıklarını doğrulamalarını ister. Hukuki görüş alınana kadar proje bu konuda varsayımda bulunmaz.

## Sonuçlar

- Katkı eşiği düşük kalır; DCO tek satırlık bir alışkanlıktır.
- Her katkının kaynağı ve katkıcının beyanı commit geçmişinde kalır; kurumlara "kaynak temiz" sorusuna yanıt verilebilir.
- Lisans değişikliği veya telif devri gerekirse katkıcı onayı toplanması gerekir; bu kabul edilen bir bedeldir.
- Mevcut commit'ler geriye dönük imzalanmaz; kural bu ADR'nin kabulünden sonraki commit'ler için geçerlidir.

## Değerlendirilen Alternatifler

- **CLA (bireysel ve kurumsal):** Lisans esnekliği sağlar; ancak bugün taraf olacak tüzel kişi yok, katkıcıyı caydırır ve kamu personeli için kurumsal CLA süreci fiilen işlemez.
- **Hiçbir mekanizma:** En düşük eşik; ancak kaynak beyanı olmadığı için kurumlar açısından risk ve gelecekteki tüm seçenekleri kapatır.
- **DCO şimdi, CLA sonra:** Bu ADR'nin seçtiği yol; CLA kapısı tüzel kişi kurulursa ayrı ADR ile açılır.

## İlgili Dokümanlar

- [ADR-0002](0002-prefer-agpl-3-or-later-license.md)
- [LICENSE_PROPOSAL.md](../../LICENSE_PROPOSAL.md)
- [CONTRIBUTING.md](../../CONTRIBUTING.md)
- [GOVERNANCE.md](../../GOVERNANCE.md)
- [DCO 1.1 metni](https://developercertificate.org/)

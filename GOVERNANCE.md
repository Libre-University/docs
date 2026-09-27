# Yönetişim

LibreUniversity, tek bir firma veya kapalı ekip tarafından yönlendirilen bir ürün değil; üniversiteler, öğrenciler, akademisyenler, geliştiriciler ve kamu yararı etrafında birleşen açık bir topluluk projesi olarak yönetilmelidir.

## Temel Yönetişim İlkeleri

- Kararlar şeffaf ve gerekçeli alınır.
- Kritik kararlar belgelenir.
- Topluluk katkısı görünür kılınır.
- Tek tedarikçi, tek kişi veya tek kurum kontrolü oluşmamalıdır.
- Teknik kararlar özgür yazılım, güvenlik, sürdürülebilirlik ve kamu yararı ilkeleriyle uyumlu olmalıdır.

## Roller

- **Katkıcı:** Doküman, kod, test, tasarım, süreç bilgisi veya tartışma katkısı yapan herkes.
- **Modül Sorumlusu:** Belirli bir modülün gereksinim, tasarım ve geliştirme koordinasyonuna yardımcı olan kişi.
- **Maintainer:** Değişiklikleri inceleme, birleştirme, sürüm hazırlama ve kalite standardını koruma yetkisi olan kişi.
- **Güvenlik Sorumlusu:** Güvenlik bildirimlerini takip eden ve koordineli açıklama sürecini yöneten kişi veya ekip.
- **Yönetişim Kurulu:** Büyük mimari, lisans, yol haritası ve topluluk politikası kararlarını koordine eden grup.

## Karar Alma

Küçük değişiklikler ilgili maintainers tarafından incelenip kabul edilebilir.

Büyük değişiklikler için önce tartışma açılmalıdır:

- Yeni çekirdek modül ekleme.
- Mimari yön değiştirme.
- Lisans politikası değişikliği.
- Kritik bağımlılık ekleme.
- Veri modeli veya entegrasyon standardı değiştirme.
- Topluluk kurallarını değiştirme.

Öncelik uzlaşmadadır. Uzlaşma sağlanamazsa maintainers ve yönetişim kurulu gerekçeli karar verir.

## Modül Sahipliği

Modül sorumluluğu sahiplik değil, bakım sorumluluğudur. Hiçbir kişi veya kurum bir modülü kapalı alana çeviremez.

Modül sorumluları:

- Gereksinimleri güncel tutar.
- Katkıları yönlendirir.
- Açık issue listesini düzenler.
- Modülün mimari ilkelere uyumunu gözetir.

## Çıkar Çatışması

Bir katkıcı veya kurum, projeye ticari hizmet sunabilir. Ancak bu durum:

- Kaynak kodu kapatmaya,
- Topluluğu dışlamaya,
- Veriyi kilitlemeye,
- Karar süreçlerini gizlemeye,
- Tek tedarikçi bağımlılığı yaratmaya

yol açamaz.

## Sürüm Politikası

Sürümler açık notlarla yayınlanmalıdır:

- Yeni özellikler.
- Kırıcı değişiklikler.
- Güvenlik düzeltmeleri.
- Migration adımları.
- Bilinen sorunlar.

## Belgelendirme

Her kritik teknik karar için kısa bir karar kaydı tutulmalıdır. İleride `docs/adr/` altında Architecture Decision Record yapısına geçilebilir.

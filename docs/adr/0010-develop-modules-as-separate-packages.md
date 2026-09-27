# ADR-0010: Modüller Ayrı Repolarda, Tek Uygulamaya Derlenen Paketler Olarak Geliştirilsin

## Durum

Önerildi. [ADR-0009](0009-organize-repositories-by-layer.md) kararının "modüller ayrı repoya bölünmez" kuralını değiştirir. Backend dili [ADR-0011](0011-use-go-for-backend.md) ile Go olarak güncellendiğinden modüller derleme zamanında birleştirilir.

## Bağlam

[MODULES.md](../../MODULES.md) 26 iş modülü tanımlar. Bu modüller farklı alan uzmanlığı (öğrenci işleri, kütüphane, hastane, İSG…) gerektirir ve farklı ekiplerce sahiplenilmelidir. Tüm modülleri tek `platform-api` reposunda tutmak, sahiplik, inceleme ve sürüm döngüsünü zorlaştırır.

Öte yandan [ADR-0004](0004-start-with-modular-monolith-for-mvp.md), erken mikroservisleşmenin operasyon yükünden kaçınmak için tek uygulama olarak dağıtımı öngörür.

## Karar

- Her iş modülü `module-<ad>` adlı ayrı bir repoda, bağımsız sürümlenen bir **Go modülü** olarak geliştirilir (ör. `github.com/Libre-University/module-obs`).
- `platform-api` **çekirdek ve dağıtım** uygulamasıdır: kimlik/yetki, akademik çekirdek veri, audit, bildirim, dosya modüllerini içerir.
- Modüller **derleme zamanında** birleştirilir (Caddy web sunucusunun eklenti modeline benzer):
  - Her modül `core.Module` arayüzünü uygular (ad, sürüm, migration'lar, HTTP rotaları, arka plan işleri, izin tanımları) ve `init()` içinde `core.Register` ile kendini kaydeder.
  - `platform-api` varsayılan dağıtımı, MVP modüllerini (`module-obs`, `module-lms`) içe aktararak tek binary üretir.
  - Farklı modül seti isteyen üniversiteler için `libre-build` aracı, seçilen modüllerle özel bir binary derler (ör. `libre-build --with github.com/Libre-University/module-obs@v0.3.0`).
- Dağıtım yine **tek uygulama, tek PostgreSQL veritabanıdır**; mikroservis yoktur. Her modül kendi tablolarının ve migration'larının sahibidir.
- Modüller çekirdeğe yalnızca `platform-api`'nin **genel arayüz paketi** (`github.com/Libre-University/platform-api/core`) üzerinden erişir: yetki kontrolü, audit yazma, bildirim gönderme, dosya saklama, akademik çekirdek sorguları. Çekirdeğin geri kalanı `internal/` altındadır ve derleyici tarafından erişime kapalıdır.
- Modüller birbirinin iç koduna erişemez; modüller arası iletişim çekirdeğin olay (domain event) arayüzü veya modülün genel paketindeki servis arayüzü üzerinden olur.
- `platform-api`, yeni modül reposu açmak için bir **modül şablonu** (`gonew` ile kullanılabilir) ve modülleri çekirdek olmadan test etmeyi sağlayan bir **test paketi** (`core/coretest`) sağlar.
- Modül ekranları MVP boyunca `platform-web` içinde, modül adına göre ayrılmış klasörlerde geliştirilir.
- Modül repoları fazı yaklaştıkça açılır. İlk açılanlar: `module-obs`, `module-lms`.

## Sonuçlar

- Her modülün kendi sahipleri (CODEOWNERS), issue'ları ve sürüm döngüsü olur.
- Üniversiteler yalnızca ihtiyaç duydukları modüllerle derlenmiş bir binary kullanabilir.
- Çekirdek genel arayüzünün sürüm uyumluluğu kritik hale gelir; kırıcı değişiklikler semver ile ve ADR ile yönetilmelidir.
- Modüller arası değişiklikler birden fazla PR gerektirebilir.
- Modül eklemek yeniden derleme gerektirir; çalışma anında modül yükleme yoktur.
- Uçtan uca testler `deploy` reposundaki birleşik geliştirme ortamında çalıştırılır.

## Değerlendirilen Alternatifler

- **Tüm modüller `platform-api` içinde (ADR-0009):** Basit, ancak sahiplik ve ölçeklenme zayıf.
- **Modül başına mikroservis:** Bağımsızlık yüksek, ancak MVP için ağır operasyon ve veri tutarlılığı yükü.

## İlgili Dokümanlar

- [ADR-0004](0004-start-with-modular-monolith-for-mvp.md)
- [ADR-0009](0009-organize-repositories-by-layer.md)
- [ADR-0011](0011-use-go-for-backend.md)
- [MODULES.md](../../MODULES.md)

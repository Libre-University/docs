# ADR-0010: Modüller Ayrı Repolarda, Tek Uygulamaya Kurulan Paketler Olarak Geliştirilsin

## Durum

Önerildi. [ADR-0009](0009-organize-repositories-by-layer.md) kararının "modüller ayrı repoya bölünmez" kuralını değiştirir.

## Bağlam

[MODULES.md](../../MODULES.md) 26 iş modülü tanımlar. Bu modüller farklı alan uzmanlığı (öğrenci işleri, kütüphane, hastane, İSG…) gerektirir ve farklı ekiplerce sahiplenilmelidir. Tüm modülleri tek `platform-api` reposunda tutmak, sahiplik, inceleme ve sürüm döngüsünü zorlaştırır.

Öte yandan [ADR-0004](0004-start-with-modular-monolith-for-mvp.md), erken mikroservisleşmenin operasyon yükünden kaçınmak için tek uygulama olarak dağıtımı öngörür.

## Karar

- Her iş modülü `module-<ad>` adlı ayrı bir repoda, bağımsız sürümlenen bir **Django uygulama paketi** olarak geliştirilir (ör. `libre-university-obs`).
- `platform-api` **çekirdek ve barındırıcı (host)** uygulamadır: kimlik/yetki, akademik çekirdek veri, audit, bildirim, dosya modüllerini içerir ve kurulu modül paketlerini Python entry point'leri (`libre_university.modules`) üzerinden yükler.
- Dağıtım yine **tek uygulama, tek PostgreSQL veritabanıdır**; mikroservis yoktur. Her modül kendi tablolarının ve migration'larının sahibidir.
- Modüller çekirdeğe yalnızca `platform-api`'nin yayımladığı **genel arayüz paketi** (`libre-university-core`) üzerinden erişir: yetki kontrolü, audit yazma, bildirim gönderme, dosya saklama, akademik çekirdek sorguları.
- Modüller birbirinin iç koduna doğrudan erişmez; modüller arası iletişim çekirdeğin olay (domain event) arayüzü veya modülün genel servis API'si üzerinden olur.
- `platform-api`, yeni modül reposu açmak için bir **modül şablonu** (cookiecutter) ve modülleri çekirdek olmadan test etmeyi sağlayan bir **test düzeneği** (pytest eklentisi) sağlar.
- Modül ekranları MVP boyunca `platform-web` içinde, modül adına göre ayrılmış klasörlerde geliştirilir.
- Modül repoları fazı yaklaştıkça açılır. İlk açılanlar: `module-obs`, `module-lms`.

## Sonuçlar

- Her modülün kendi sahipleri (CODEOWNERS), issue'ları ve sürüm döngüsü olur.
- Üniversiteler yalnızca ihtiyaç duydukları modülleri kurabilir.
- Çekirdek genel arayüzünün sürüm uyumluluğu kritik hale gelir; kırıcı değişiklikler semver ile ve ADR ile yönetilmelidir.
- Modüller arası değişiklikler birden fazla PR gerektirebilir.
- Uçtan uca testler `deploy` reposundaki birleşik geliştirme ortamında çalıştırılır.

## Değerlendirilen Alternatifler

- **Tüm modüller `platform-api` içinde (ADR-0009):** Basit, ancak sahiplik ve ölçeklenme zayıf.
- **Modül başına mikroservis:** Bağımsızlık yüksek, ancak MVP için ağır operasyon ve veri tutarlılığı yükü.

## İlgili Dokümanlar

- [ADR-0004](0004-start-with-modular-monolith-for-mvp.md)
- [ADR-0009](0009-organize-repositories-by-layer.md)
- [MODULES.md](../../MODULES.md)

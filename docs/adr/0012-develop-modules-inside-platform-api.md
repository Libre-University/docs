# ADR-0012: Modüller MVP Boyunca `platform-api` İçinde Geliştirilsin

## Durum

Önerildi. Kabul edilirse [ADR-0010](0010-develop-modules-as-separate-packages.md) "Değiştirildi" durumuna geçer.

Karar verenler: Kurucu önerisi; öneri sahibi @Aybavs. Tartışma: [docs#9](https://github.com/Libre-University/docs/issues/9), [docs#2](https://github.com/Libre-University/docs/issues/2).

## Bağlam

[ADR-0009](0009-organize-repositories-by-layer.md) "modül başına repo" seçeneğini modüler monolith kararıyla çeliştiği gerekçesiyle reddetmiş, hemen ardından [ADR-0010](0010-develop-modules-as-separate-packages.md) OBS ve LMS'i ayrı repolarda, derleme zamanında birleşen Go modülleri olarak tanımlamıştı. İki karar birbiriyle çelişiyor.

Asıl sorun modüller arasında değil, modül ile çekirdek arasındaki sınırdadır. Modüller `platform-api/core` genel arayüzünü kullanır ve bu arayüz ilk aylarda sık değişecektir. Modüller ayrı repodayken çekirdekteki her arayüz değişikliği `platform-api` için PR ve sürüm etiketi, ardından her modül reposunda `go.mod` güncellemesi ve ikinci bir PR gerektirir; uçtan uca test için üç repoyu uyumlu sürümlerde bir araya getirmek gerekir. Caddy'nin eklenti modeli bu yapı için iyi bir örnektir, ancak Caddy bu modele çekirdeği yıllarca olgunlaştıktan sonra geçmiştir.

ADR-0010'un vaat ettiği faydalar (modül başına sahiplik, üniversitenin kendi modül setini derlemesi) bugün ayrı repo olmadan da sağlanabilir. Bugün modülleri ayrı ayrı sahiplenecek ekipler yoktur; maliyet şimdi, fayda ileride ödenmektedir.

## Karar

MVP boyunca iş modülleri `platform-api` reposunun içinde geliştirilir. Çalışma zamanı modeli değişmez: tek binary, tek PostgreSQL ([ADR-0004](0004-start-with-modular-monolith-for-mvp.md), [ADR-0011](0011-use-go-for-backend.md)).

### Yerleşim

```
platform-api/
  go.work
  core/                   # go.mod: modüllerin gördüğü genel arayüz (Module, Register, yetki, audit, bildirim, dosya, akademik sorgular)
  core/coretest/          # modülleri çekirdek olmadan test etmek için sahte uygulamalar
  platform/               # go.mod: çekirdek uygulama; dışarıya yalnızca platform.New açık
  platform/internal/...   # identity, academic, audit, notifications, files, modules
  modules/obs/            # go.mod: OBS modülü (bugünkü module-obs)
  modules/obs/internal/
  modules/lms/            # go.mod: LMS modülü (bugünkü module-lms)
  cmd/libre-university/   # platform ile modülleri birleştiren varsayılan main
```

`go.work` ile her modül kendi `go.mod` dosyasına sahip ayrı bir Go modülüdür. Çekirdeğin iç kodu `platform/internal/` altında olduğu için Go'nun `internal` kuralı modüllerin çekirdeğin içine ve birbirinin `internal/` klasörüne erişmesini derleyici düzeyinde engeller.

### Kurallar

- `core.Module` ve `core.Register` mekanizması ADR-0010'daki gibi kalır.
- Modüller yalnızca `core` paketini içe aktarır; `platform` paketini yalnızca `cmd/` kullanır. Bu kural `golangci-lint` `depguard` ile CI'da denetlenir.
- Her modülün tabloları kendi PostgreSQL şemasındadır (`obs.*`, `lms.*`); migration'ları kendi klasöründe ve kendi goose sürüm tablosuyla tutulur.
- sqlc yapılandırmasında her modül yalnızca kendi şemasını görür; başka modülün tablosuna yazılan sorgu kod üretiminde hata verir. Başka modülün verisine `core` arayüzü veya olaylar üzerinden erişilir.
- Modül testleri gerçek çekirdek yerine `core/coretest` ile çalışır.
- Sahiplik dizin bazlı CODEOWNERS ile tanımlanır (`/modules/obs/ @…`); issue'lar `module:*` etiketleriyle ayrılır.
- Farklı modül setleri `cmd/` altında ayrı main paketleri veya build tag ile aynı repodan derlenir; `libre-build` aracının ihtiyacı bu şekilde karşılanır.

### Ayrılma ölçütü

Bir modül şu iki koşul birlikte sağlandığında kendi reposuna taşınır:

1. `core` paketi v1.0 olarak yayımlanmış ve geriye uyumluluk taahhüdü verilmiştir.
2. Modülün, `platform-api` çekirdek bakımcılarından bağımsız en az iki aktif bakımcısı vardır.

Ölçüt modül başına uygulanır. Küçük modüllerin süresiz olarak çekirdek repoda kalması beklenir; Caddy'nin standart modül / topluluk modülü ayrımı örnek alınır. Taşıma işlemi mekaniktir: klasörün `git filter-repo` ile geçmişiyle birlikte yeni repoya alınması, import yollarının güncellenmesi ve `core`'un sürümlenmesi.

### Mevcut modül repoları

`module-obs` ve `module-lms` repolarındaki açık issue'lar `platform-api`'ye `module:obs` / `module:lms` etiketleriyle taşınır; repolar arşivlenir. Yalnızca issue takibi için açık tutulmaz.

## Sonuçlar

- Çekirdek arayüzü olgunlaşana kadar repolar arası sürümleme ve koordinasyon yükü ortadan kalkar; çekirdek ve modül değişiklikleri tek PR'da yapılabilir.
- Uçtan uca test tek repoda çalışır.
- Modül sınırları derleyici (`internal`), `depguard`, ayrı şema ve sqlc kısıtıyla korunur; "aynı repoda olunca sınırlar gevşer" riski araçla kapatılır.
- Modül başına sahiplik ve etiketleme korunur.
- Faz 0'daki `module-obs#1`, `module-lms#1` ve `platform-api#1` iskelet işleri bu yerleşime göre yeniden tanımlanır.
- Yol haritası ve repo tablosu bu karara göre güncellenir (ayrı PR).

## Değerlendirilen Alternatifler

- **ADR-0010 olduğu gibi (modül başına repo):** Sahiplik ayrımı net; ancak bugün ayrı sahiplenecek ekipler yok ve `core` olgunlaşmadan repolar arası sözleşme yükü doğuruyor.
- **Ayrı bir `modules` reposu:** Repo sayısını azaltır ama sorunu çözmez; `core` ile modüller yine farklı repolarda kalır, aynı sürümleme yükü modül başına sahiplik faydası olmadan ödenir.
- **Tek `go.mod` ile tek repo:** En basit başlangıç; ancak modül başına `go.mod` olmadan ileride ayırmak zorlaşır ve modül bağımlılıkları çekirdeğe karışır.
- **Tek repoda geliştirip modülleri otomatik olarak ayrı repolara yansıtmak (Kubernetes `staging/` modeli):** İleride değerlendirilebilir; MVP için gereksiz altyapı.

## İlgili Dokümanlar

- [ADR-0004](0004-start-with-modular-monolith-for-mvp.md)
- [ADR-0009](0009-organize-repositories-by-layer.md)
- [ADR-0010](0010-develop-modules-as-separate-packages.md)
- [ADR-0011](0011-use-go-for-backend.md)
- [ROADMAP.md](../../ROADMAP.md)

# Epsilon Oyun Stüdyosu — Çalışma Düzeni v1.0

**Tarih:** 11 Kasım 2026
**Repo konumu:** `docs/CALISMA-DUZENI.md`
**Bağlı belge:** `docs/rehber/Epsilon_Oyun_Gelistirme_Rehberi_v2_1.md` (bütün ürün ve kalite standartları oradadır; bu belge onu değiştirmez, görev dağılımını ve işleyişi tanımlar)

Bu belge, Epsilon Yayın Grubu'nun kitaptan uyarlama oyun üretiminde üç tarafın nasıl çalıştığını tanımlar. Amaç: Rıza'ya mümkün olduğunca az iş düşmesi, üretimin kesintisiz sürmesi ve yüksek yaratıcı kaliteye ulaşılması.

---

## 1. Roller

### Rıza — Ürün Sahibi
Günlük operasyonda Rıza'ya iş düşmez; iki stüdyo repo üzerinden doğrudan haberleşir. Rıza sadece şunları yapar:

1. **Kitap seçimi** ve kitap içeriklerinin (iç illüstrasyonlar, kapak, metin/PDF) Claude'a iletilmesi — repoya Claude işler.
2. **Hikâye seçimi:** Claude'un sunduğu 3 oyun hikâyesi konseptinden birini seçer; hiçbirini beğenmezse Claude 3 yenisini üretir, seçim yapılana kadar.
3. **İki onay noktası** (aşağıda §5): sanat yönü onayı ve yayın onayı.
4. İstediği an denetim ve müdahale. Müdahale `docs/KARAR-GUNLUGU.md`'ye işlenir ve bağlayıcıdır.

Rıza'ya soru sorulmaz; öneri + etkisi + seçilen varsayılan sunulur. Cevap gelmezse varsayılanla devam edilir (§4).

### ChatGPT — Sanat Stüdyosu (yalnızca görsel)
Sorumluluk alanı, Rehber v2.1 §10.1 tablosundaki **image satırlarının tamamıdır:**

- Sanat kılavuzu ve referans paketi (Rehber §9), kitabın çizim dilinden türetilmiş.
- **Oyundaki bütün görseller:** karakterler, ifadeler/pozlar, ortamlar ve katmanları, nesneler, menü ve TÜM arayüz sanatı (buton, panel, ikon, çerçeve, görev düğümü, ödül, dekor), görsel durumlar (normal/basılı/kilitli/seçili), logo ve mağaza görselleri.
- **Üretim yöntemi kesindir:** hiçbir görsel kodla (CSS/SVG/canvas), hazır temayla veya ikon paketiyle yapılmaz; her sanatsal detay image yeteneğiyle üretilir (Rehber §10). Bu kuralın istisnası yoktur.
- **Görsel tutarlılık denetimi:** her partide kendi çıktılarını kitap referansları ve sanat kılavuzuyla karşılaştırır; Claude'un repoya koyduğu oyun içi ekran görüntülerini kitap kimliğine ve kılavuza sadakat yönünden denetler, bulguları `GPT-TO-CLAUDE.md`'ye yazar.
- Her teslimde manifest satırları (SABLONLAR.md'deki format).

Hikâye ve GDD Claude'dadır; ChatGPT bunları repodan okur, hikâye/mekanik önerilerini `GPT-TO-CLAUDE.md` üzerinden verir.

### Claude — Teknik Stüdyo (hikâye + mekanik + kod)
Sorumluluk alanı, aynı tablodaki **kod satırlarının tamamı artı oyun tasarımıdır:**

- **Hikâye ve oyun tasarımı:** uyarlama özeti, GDD, bölüm/görev kurgusu, karakter motivasyonları ve bütün oyun içi metinler (Rehber §4–6) — hikâye ile mekanik tek elde tasarlanır.
- Oyun mekaniği: temel döngünün uygulanması, kontrol hissi, zorluk eğrisi, yardım sistemi.
- Mimari (Rehber §17: oyun modülü / içerik paketi / ortak deneyim sistemi / ev sahibi ayrımı), kod, kayıt/devam, ebeveyn alanı işlevi, performans (Rehber §18).
- Görsellerin entegrasyonu: yerleşim, 9-slice, atlas, hareket/animasyon, ses bağlama, canlı metin.
- Varlık envanteri ve kullanım matrisinin sahibi; asset'lerin `planlandı → üretildi → teknik kontrol → entegre → oyun içinde doğrulandı` zincirinin yürütülmesi (Rehber §12).
- Kalite kapılarının (K0–K4) yürütülmesi ve kanıtlanması (Rehber §16), görsel sadakat denetimi (Rehber §10.2 adım 7), teslim paketi ve `DEVAM-NOTU` bakımı.
- Repo bakımı: klasör düzeni, sürümleme, ChatGPT çıktılarının `assets/working/`'den `assets/runtime/`'a işlenmesi.

**Sınır kuralı:** ChatGPT kod yazmaz, GDD/hikâye yazmaz, arayüz sanatını koda tarif etmez. Claude görsel üretmez ve eksik görseli ASLA CSS/SVG/canvas, hazır bileşen veya geçici kod çizimiyle ikame etmez; eksik görsel = `CLAUDE-TO-GPT.md`'ye yeni istek + ilgili iş "engelli" işaretlenir (Rehber §10.4). İkisi de diğerinin alanına öneri verebilir; karar alan tarafındır.

---

## 2. Tek doğru kaynak: GitHub reposu

Repo **private önerilir** — kitap içerikleri telifli olduğu için. ChatGPT'nin erişimi public link değil GitHub bağlantısı üzerinden olduğundan private repo düzeni bozmaz. **İki stüdyo da repoya doğrudan yazar:** ChatGPT ürettiği partileri, belgelerini ve notlarını kendisi commit'ler; Claude git ile doğrudan çalışır. Bütün iletişim repo dosyaları üzerinden yürür — sohbet geçmişi kaynak değildir: **repoda olmayan şey yok sayılır.** Her oturum `docs/DEVAM-NOTU.md`'den başlar.

### Yazma alanları (çakışma önleme — Rehber §26)

Her dosyanın tek sahibi vardır; diğer taraf o dosyayı okur ama değiştirmez:

- **ChatGPT yazar:** `assets/working/**`, sanat kılavuzu dosyaları, `docs/istekler/GPT-TO-CLAUDE.md`; `CLAUDE-TO-GPT.md`'de yalnızca isteklerin durum ve "Sonuç" satırları.
- **Claude yazar:** `src/**`, `content/**`, `assets/runtime/**`, `docs/gdd/**`, `docs/DEVAM-NOTU.md`, `docs/OYUN-KATALOGU.md`, `docs/istekler/CLAUDE-TO-GPT.md`; `GPT-TO-CLAUDE.md`'de yalnızca notların cevap satırları.
- **KARAR-GUNLUGU.md:** ikisi de sadece sona kayıt ekler (append-only); numara çakışırsa Claude düzeltir.
- **Rıza her yere yazabilir;** yazdığı her şey bağlayıcıdır.

Commit mesajı öneki zorunludur: `[gpt] ...`, `[claude] ...`, `[riza] ...` (örn. `[gpt] P003: ana karakter poz seti v001`). Rutin işler doğrudan ana dala gider; büyük veya deneysel değişiklik ayrı dalda açılır, birleştirmeyi Claude yapar.

Her durumda repoya konmayacaklar: gerçek çocuk/kişi verisi, hesap bilgisi, API anahtarı. Kitap içerikleri Rıza'dan Claude'a gelir; Claude üretim için gerekenleri `assets/source/`'a işler ve ChatGPT kitaba oradan erişir. Repo public tutulacaksa tam metin yerine yalnızca üretim için gereken referans sayfalar konur.

## 3. Günlük döngü

1. **Claude turu:** `DEVAM-NOTU` ve `GPT-TO-CLAUDE.md` okunur → `assets/working/`'e düşen yeni partiler teknik kontrolden geçirilip entegre edilir → sıradaki iş yapılır (kod, mekanik, denetim) → yeni görsel/içerik ihtiyaçları `docs/istekler/CLAUDE-TO-GPT.md`'ye şartnameli istek olarak yazılır → `DEVAM-NOTU` ve manifest güncellenir, commit atılır.
2. **ChatGPT turu:** `DEVAM-NOTU` ve `CLAUDE-TO-GPT.md` okunur → açık istekler üretilir → her parti `assets/working/PNNN-aciklama/` klasörüne manifest satırlarıyla birlikte doğrudan push'lanır → isteklerin durum/sonuç satırları güncellenir → Claude'a brief, soru ve öneriler `GPT-TO-CLAUDE.md`'ye işlenir.
3. **Rıza (isteğe bağlı):** `DEVAM-NOTU` ve `KARAR-GUNLUGU`'ne göz atar; müdahalesi varsa yazar, iki stüdyo bir sonraki turda uygular.

Turların sırası sabit değildir; her stüdyo repoyu her açtığında diğerinin son commit'lerinden devam eder.

İstek dosyalarındaki her kayıt `AÇIK / ÜRETİLDİ / KABUL / RET(nedeni)` durumlarından birini taşır. RET edilen iş aynı istek numarasıyla, ret nedeni yazılarak yeniden üretilir.

## 4. Özerklik ve karar kuralları (Rıza'yı az meşgul etme)

- **Varsayılan davranış: yap ve kaydet.** Kapsam içindeki her üretim, düzeltme ve entegrasyon için izin istenmez (Rehber §27). Önemli her karar `KARAR-GUNLUGU`'ne gerekçesiyle yazılır; Rıza async okur, itiraz ederse geri alınır.
- **Rıza'ya giden kararlar yalnızca şunlardır:** kitap seçimi; sanat yönü onayı (§5/O1); kapsamın esaslı değişmesi; harcama gerektiren her şey (hesap, lisans, mağaza ücreti); yayına basma (§5/O2).
- **İki stüdyo anlaşamazsa:** konu `KARAR-GUNLUGU`'ne iki seçenek + etkileriyle yazılır, Claude geçici kararı verir ve iş durmaz; Rıza isterse değiştirir.
- **Belirsizlikte:** çocuk deneyimi > görsel gösteriş > üretim hızı sıralaması uygulanır.

## 5. Rıza'nın iki onay noktası

- **O1 — Sanat yönü + kapsam onayı** (Rehber kapıları K0+K1 birleşik): uyarlama özeti, GDD özeti, sanat kılavuzu ve 3–4 temsilî ekran referansı tek mesajda sunulur. Rıza "onay" der veya düzeltme ister. Bu onaydan sonra seri üretim tamamen özerk yürür.
- **O2 — Yayın onayı** (K4): tamamlanmış oyun, denetim kaydı ve mağaza paketi sunulur. Yayın ancak Rıza'nın onayıyla olur.

K2 (ilk kalite bölümü) ve K3 (tam içerik) kapıları Claude'un iç kontrol noktalarıdır; Rıza'ya yalnızca kısa ilerleme mesajı + oynanabilir link gider, onay beklenmez.

## 6. Teknoloji kararı (başlangıç, KARAR-GUNLUGU #001)


- **HTML5 web tabanlı oyun modülü** (tek kod tabanı), oyun katmanında **Phaser 3**; App Store ve Google Play paketlemesi **Capacitor** ile.
- Gerekçe: image-ağırlıklı 2D oyunlara uygun, tek kod tabanından iki mağaza + web demo, çatı uygulamaya modül olarak taşınabilir (Rehber §17 ile uyumlu).
- Her oyun `src/` içinde bağımsız modül olarak, içerik `content/` altında sürümlü veri olarak tutulur; ileride çatı uygulama bu modülleri yükler.

## 7. Gece denetimi (otomatik)

Her gece 00:00'da (Europe/Istanbul) Claude'un zamanlanmış denetim görevi çalışır ve kimseden talimat beklemeden şunları kontrol eder:

- Repo bütünlüğü: klasör yapısı, adlandırma kuralları, yazma alanı ihlalleri, commit önekleri.
- Manifest ↔ dosya tutarlılığı: dosyası olmayan kayıt, kaydı olmayan dosya, durum zincirinde takılı kalan varlıklar.
- İstek sağlığı: 2 günden uzun süredir AÇIK bekleyen istekler, cevapsız notlar.
- Teknik sağlık: build/test sonucu, DEVAM-NOTU güncelliği.

Rapor `docs/denetim/GECE-RAPORU-<tarih>.md` olarak commit'lenir. ChatGPT'yi ilgilendiren bulgular `CLAUDE-TO-GPT.md`'ye istek/not olarak düşülür; ChatGPT her oturum başında son gece raporunu okur ve kendi alanındaki bulguları kapatır. Kritik bulgu (çalışmayan build, kayıp dosya, kural ihlali) Rıza'ya bildirilir; gerisi için Rıza rahatsız edilmez.

## 8. Kalite ilkeleri (özet — tam hâli Rehber'de)

- "Tamamlandı" yalnızca Rehber §23 ölçütleri karşılanınca denir; dosyasız/çalışmayan hiçbir şey tamamlandı sayılmaz.
- Her görevde amaç → anlamlı eylem → anlaşılır sonuç → tepki → ilerleme döngüsü aranır (Rehber §6); aynı sorunun resim değiştirmiş hâli çeşitlilik sayılmaz.
- Görsel sadakat: ChatGPT'nin referans ekranıyla çalışan oyunun ekran görüntüsü aynı boyutta karşılaştırılır; sapmalar düzeltilmeden bölüm kapanmaz.
- Reklam yok, çocuğa satın alma yönlendirmesi yok, cezalandırıcı seri baskısı yok (Rehber §8).

## 9. Yeni oyun açılış sırası (özet)

1. Rıza kitabı seçer ve içeriklerini Claude'a iletir; Claude kaynakları `assets/source/`'a işler, `OYUN-KATALOGU.md`'ye kayıt açar.
2. Claude **3 oyun hikâyesi konsepti** sunar — eğitici ve eğlenceli olmak kaydıyla; her biri için ana duygu, çocuğun rolü, temel oyun döngüsü, bölüm yapısı fikri ve öğrenme hedefleri. Rıza birini seçer; beğenmezse Claude 3 yeni konsept üretir, seçim yapılana kadar.
3. Claude seçilen hikâyeyi **en ince ayrıntısına kadar projelendirir:** tam GDD (hikâye, bölüm/görev kurgusu, bütün ekranların ve arayüzün tanımı, oyun elementleri, bütün oyun içi metinler), kapsam sözleşmesi, varlık envanteri ve kullanım matrisi — `docs/gdd/` altına. İlk görsel istekleri `CLAUDE-TO-GPT.md`'ye şartnameli olarak yazılır.
4. ChatGPT: GDD ve kitap görsellerinden (`assets/source/`) sanat kılavuzu + temsilî ekran referansları.
5. **O1 onayı.**
6. ChatGPT ilk kalite bölümünün asset'lerini üretir; Claude paralelde mimariyi ve ortak deneyim sistemini kurar.
7. K2: ilk kalite bölümü çalışır hâlde; görsel/oyun/teknik denetim.
8. Kalan kapsam partiler hâlinde: istek → üretim → entegrasyon → doğrulama.
9. K3 → K4 → **O2 onayı** → yayın; katalog ve devam notu güncellenir.

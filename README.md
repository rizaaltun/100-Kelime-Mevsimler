# Epsilon Oyun Stüdyosu

Epsilon Yayın Grubu'nun çocuk kitaplarından uyarlanan eğitici mobil oyunlarının üretim deposu. Hedef: her kitap için eğlenceli, görsel olarak güçlü, karakter odaklı, tamamlanmış ve yeniden oynanabilir bir oyun; uzun vadede 100 oyunluk katalogla çatı uygulama.

## Nasıl çalışıyoruz

Üretim iki yapay zekâ stüdyosu ve bir ürün sahibiyle yürür:

| Taraf | Rol |
| --- | --- |
| **Rıza** | Ürün sahibi: kitap seçimi ve kaynak yükleme, O1 (sanat yönü) ve O2 (yayın) onayları, istediği an müdahale |
| **ChatGPT — Sanat Stüdyosu** | Sanat kılavuzu ve oyundaki bütün görseller (menü/arayüz dahil, tamamı image üretimi — kodla tasarım yasak) + görsellerin kitapla tutarlılık denetimi; çıktılarını repoya kendisi push'lar |
| **Claude — Teknik Stüdyo** | Hikâye ve GDD, oyun mekaniği, kod, mimari, entegrasyon, denetim, bu reponun bakımı |

İki stüdyo birbirleriyle yalnızca bu repo üzerinden haberleşir (`docs/istekler/`); günlük operasyonda Rıza'ya iş düşmez.

İşleyişin tamamı: [`docs/CALISMA-DUZENI.md`](docs/CALISMA-DUZENI.md). Ürün ve kalite standartları: [`docs/rehber/Epsilon_Oyun_Gelistirme_Rehberi_v2_1.md`](docs/rehber/). **Bu repo tek doğru kaynaktır; repoda olmayan iş yok sayılır.** Her oturum [`docs/DEVAM-NOTU.md`](docs/DEVAM-NOTU.md) ile başlar.

## Klasör yapısı

```
docs/
  rehber/                  Rehber v2.1 ve bağlı standart belgeleri
  CALISMA-DUZENI.md        Roller, işleyiş, onay noktaları
  DEVAM-NOTU.md            Güncel durum — her oturumun başlangıç noktası
  KARAR-GUNLUGU.md         Numaralı kararlar ve gerekçeleri
  OYUN-KATALOGU.md         Oyun kayıtları (kimlik, yaş, beceri, durum)
  SABLONLAR.md             Kayıt ve brief şablonları
  gdd/                     Oyun tasarım belgeleri (oyun başına bir dosya)
  istekler/
    CLAUDE-TO-GPT.md       Claude'un şartnameli görsel/içerik istekleri
    GPT-TO-CLAUDE.md       ChatGPT'nin Claude'a brief ve notları
assets/
  source/                  Kitap referansları (yalnız üretim için gereken sayfalar)
  working/                 ChatGPT teslim partileri — kabul bekleyen
  runtime/                 Oyuna alınmış, doğrulanmış varlıklar
    characters/  environments/  objects/  ui/  effects/  audio/
content/                   Sürümlü görev, bölüm, metin ve içerik verileri
src/                       Oyun modülleri ve ortak deneyim sistemi (HTML5 / Phaser 3)
```

## Dosya akışı

1. Claude isteği `docs/istekler/CLAUDE-TO-GPT.md`'ye yazar ve commit'ler.
2. ChatGPT isteği repodan okur, partiyi üretir ve `assets/working/PNNN-aciklama/` altına manifest satırlarıyla birlikte kendisi push'lar; isteğin durumunu günceller.
3. Claude teknik kontrolü yapar, kabul edilen varlığı `assets/runtime/`'a işler, manifesti ve isteğin durumunu günceller; ret varsa nedenini aynı istek numarasına yazar.

Yazma alanları ayrıktır (kim hangi dosyaya yazar: `docs/CALISMA-DUZENI.md` §2); commit mesajları `[gpt]`, `[claude]`, `[riza]` önekini taşır.

## Adlandırma

Varlık dosyaları: `oyunid_aile_ad_durum_v001.png` (örn. `oyun01_ui_btn_primary_pressed_v002.png`). "son", "final", "yeni" gibi adlar kullanılmaz; aynı ada farklı içerik yüklenmez. Parti klasörleri: `P001-aciklama` biçiminde numaralanır.

## Not

Kitap içerikleri telifli olduğu için repo private tutulur (ChatGPT erişimi GitHub bağlantısı üzerindendir, public link gerekmez). Gerçek kişi/çocuk verisi, hesap bilgisi ve anahtarlar hiçbir durumda repoya konmaz.

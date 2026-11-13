# Çalışma Kayıt Şablonları v1.0

Repo konumu: `docs/SABLONLAR.md`. Bu dosyadaki formatlar bağlayıcıdır; iki stüdyo da kayıtları bu biçimde tutar. Şablonlar boş iskelettir — doldurulmamış şablon, yapılmış iş değildir.

---

## 1. DEVAM-NOTU.md

Her anlamlı oturum sonunda Claude günceller. Her oturum bunu okuyarak başlar.

```markdown
# DEVAM NOTU — güncelleme: <tarih> (<güncelleyen>)

## Aktif oyun
- Oyun: <oyunid — ad> | Kitap: <kitap> | Hedef yaş: <aralık>
- Aşama / kalite kapısı: <K0–K4 + kısa durum>
- Standart sürümleri: Rehber v2.1, Çalışma Düzeni v1.0, sanat kılavuzu v<NN>

## Son tamamlananlar
- <somut çıktı + dosya yolu>

## Sıradaki somut işler
1. <iş — sahibi: Claude / ChatGPT / Rıza>

## Açık istekler
- CLAUDE-TO-GPT: <açık istek numaraları> | GPT-TO-CLAUDE: <varsa>

## Engeller ve açık sorunlar
- <engel — neyi bekliyor — hangi işler etkileniyor>

## Rıza'dan beklenen (varsa)
- <tek cümle + varsayılan: cevap gelmezse ne yapılacağı>
```

## 2. KARAR-GUNLUGU.md

Numaralı, silinmez; karar değişirse yeni kayıt eskisine atıf yapar.

```markdown
## #NNN — <kısa başlık> (<tarih>, karar veren: Rıza / Claude / ChatGPT)
- Karar: <tek cümle>
- Gerekçe: <1–2 cümle>
- Etki: <hangi oyun/dosya/standart etkileniyor>
- Durum: geçerli | #MMM ile değişti
```

## 3. CLAUDE-TO-GPT.md — görsel/içerik istek kaydı

Her istek tek kayıt. ChatGPT şartnameye birebir uyar; yoruma açık alan bırakılmışsa yaratıcı karar ChatGPT'nindir.

```markdown
## İSTEK-NNN — <kısa ad>   [AÇIK | ÜRETİLDİ | KABUL | RET]
- Varlık kimlikleri: <oyunid_aile_ad_durum> (tek istekte ilişkili aile toplanabilir)
- Kullanım yeri: <ekran/görev + ne işe yarayacağı>
- Referans: <sanat kılavuzu sürümü + karakter/ekran referans dosyası>
- İstenen: <poz/eylem/içerik tarifi — yaratıcı alan ChatGPT'de>
- Teknik: boyut/oran <px veya oran>, alfa <evet/hayır>, katman ihtiyacı <varsa>,
  9-slice <varsa kenar payları>, durum varyantları <normal/basılı/...>
- Kabul ölçütü: <neye bakılacak>
- Sonuç: <parti adı + dosyalar> | RET nedeni: <varsa, somut>
```

## 4. GPT-TO-CLAUDE.md — brief/not kaydı

```markdown
## NOT-NNN — <kısa ad> (<tarih>)   [AÇIK | CEVAPLANDI]
- Tür: mekanik önerisi | teknik soru | içerik değişikliği | uyarı
- İçerik: <ChatGPT'nin metni>
- Claude cevabı/kararı: <ne yapıldı; karar gerekiyorsa KARAR-GUNLUGU #NNN>
```

## 5. Manifest — varlık envanteri satırı

ChatGPT her teslim partisiyle bu satırları verir; Claude kabulden sonra durum alanını yürütür. Dosya: `assets/runtime/MANIFEST.md` (parti hâlindeyken `assets/working/<parti>/manifest.md`).

```markdown
| asset_id | aile | kullanım | dosya | boyut | alfa | referans | sürüm | durum |
| oyun01_char_main_celebrate | karakter | görev sonucu ekranı | ...v001.png | 1024x1024 | var | kılavuz v02 | v001 | üretildi |
```

Durum zinciri: `planlandı → üretildi → teknik kontrol → entegre → doğrulandı` (+ `engelli`, `ret`). Kullanım matrisi aynı dosyanın ikinci tablosudur: hangi ekran/görev hangi asset_id'yi kullanıyor.

## 6. OYUN-KATALOGU.md — oyun kaydı

```markdown
## <oyunid> — <oyun adı>
- Kitap / yayınevi: <...> | Hedef yaş: <...> | Ön beceriler: <...>
- Hikâye ve temel döngü: <2–3 cümle>
- Birincil / ikincil beceri: <ortak sözlükten>
- Sanat yönü: <kılavuz sürümü> | Teknoloji: HTML5/Phaser3/Capacitor
- Durum: <aşama/kapı> | Sürüm: <...> | Açık kararlar: <...>
```

## 7. Teslim partisi kuralları (özet)

- Parti klasörü: `assets/working/PNNN-aciklama/` — içinde dosyalar + `manifest.md`.
- Dosya adı: `oyunid_aile_ad_durum_vNNN.png` — "son", "final", "yeni" yasak.
- Ayrı kullanılacak her öğe gerçek alfa kanallı PNG; tam sahne arka planları katman ihtiyacına göre ayrılmış.
- Parti, isteğin BÜTÜN kalemlerini kapsar; eksik kalem varsa manifestte `engelli` olarak görünür.

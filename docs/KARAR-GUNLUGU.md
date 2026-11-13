# Karar Günlüğü

Numaralı, silinmez; karar değişirse yeni kayıt eskisine atıf yapar. Format: `docs/SABLONLAR.md` §2. İki stüdyo da yalnızca sona kayıt ekler (append-only); numara çakışırsa Claude düzeltir.

---

## #001 — Teknoloji seçimi (2026-11-12, karar veren: Rıza)
- Karar: HTML5 web tabanlı oyun modülü, oyun katmanında Phaser 3; App Store ve Google Play paketlemesi Capacitor ile.
- Gerekçe: Image-ağırlıklı 2D oyunlara uygun; tek kod tabanından iki mağaza + web demo; ileride çatı uygulamaya modül olarak taşınabilir (Rehber §17 ile uyumlu).
- Etki: Bütün oyunlar; `src/` yapısı (oyun başına bağımsız modül) ve `content/` (sürümlü veri).
- Durum: geçerli

## #002 — Rol dağılımı: iki stüdyo modeli (2026-11-12, karar veren: Rıza)
- Karar: Hikâye, GDD, oyun mekaniği ve kod Claude'da (Teknik Stüdyo); ChatGPT yalnızca görsel üretir (Sanat Stüdyosu) — bütün görseller image yeteneğiyle, kodla (CSS/SVG/canvas) tasarım yasak.
- Gerekçe: Hikâye ile mekanik tek elde tasarlanır; görsel kalite ve kitap sadakati tek sorumluda toplanır (CALISMA-DUZENI §1).
- Etki: Bütün üretim süreci; yazma alanları CALISMA-DUZENI §2'deki gibi ayrıktır.
- Durum: geçerli

## #003 — Oyun başına bir repo (2026-11-12, karar veren: Rıza)
- Karar: Her oyun kendi GitHub reposunda geliştirilir; bu repo `100-Kelime-Mevsimler` oyununa aittir.
- Gerekçe: Kaynak ve varlık hacmi oyun başına büyüktür; erişim ve arşivleme oyun bazında yönetilir.
- Etki: Repo yapısı; OYUN-KATALOGU bu repoda yalnız bu oyunun kaydını tutar, çatı katalog ileride ayrıca kurulur.
- Durum: geçerli

## #004 — İlk kitap: 100 Kelime Mevsimler (2026-11-12, karar veren: Rıza)
- Karar: İlk oyun, "100 Kelime Mevsimler" (dil öğrenme boardbook) kitabından uyarlanır; oyun kimliği `oyun01`.
- Gerekçe: Rıza'nın kitap seçimi (CALISMA-DUZENI §1, görev 1).
- Etki: `docs/OYUN-KATALOGU.md` kaydı açıldı; kitap içerikleri gelince `assets/source/` doldurulacak, ardından 3 hikâye konsepti sunulacak.
- Durum: geçerli

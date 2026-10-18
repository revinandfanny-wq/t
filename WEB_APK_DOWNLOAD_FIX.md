# WEB -> APK (Telegram) DOWNLOAD FIX

## Kenapa versi sebelumnya tidak masuk Galeri?
Karena kamu membuat:
`Dika Tools WEB -> APK dari Telegram/WebView`.

Dalam model ini folder `android/` dari ZIP tidak otomatis ikut menjadi APK. Jadi `MediaStore` Java tidak pernah dipanggil.

## Yang sudah diperbaiki di versi ini
1. TikTok dipanggil melalui `/api/tiktok` sehingga API key RapidAPI tidak ditanam di HTML.
2. Tombol download tidak lagi memakai variabel `event` yang bisa menyebabkan `ReferenceError`.
3. File download melewati `/api/download` dengan `Content-Disposition: attachment`.
4. Proxy download sekarang melakukan streaming, bukan membaca seluruh video ke RAM.
5. WebView diberi kesempatan menyerahkan file ke Download Manager.
6. Riwayat Unduhan Dika Tools tetap disimpan.

## SANGAT PENTING
Website murni **tidak mempunyai izin untuk memaksa file masuk ke Galeri Android**.

Agar APK hasil "WEB -> APK Telegram" benar-benar menyimpan file, builder/WebView yang kamu pakai HARUS mendukung:
- Android Download Manager / WebView DownloadListener, atau
- pilihan "Allow downloads / Download files".

Kalau builder Telegram tidak punya dukungan download, tidak ada perubahan HTML/JavaScript yang dapat memaksa WebView menyimpan file ke Galeri.

## Cara cek
Setelah deploy WEB:
1. Buka link WEB biasa di Chrome Android.
2. Convert TikTok.
3. Tekan Download Video.
4. Jika Chrome menyimpan file, backend Dika Tools sudah benar.
5. Jika Chrome berhasil tetapi APK tidak, masalahnya 100% pada builder WEB -> APK Telegram yang tidak meneruskan download.

## TikTok No Watermark
Server membutuhkan:
`RAPIDAPI_KEY`

Masukkan key hanya di environment server/deployment, BUKAN di index.html.

Endpoint:
`/api/tiktok?url=...`

## Spotify
Tetap mengikuti SPOTIFY_SETUP.md.
Full playback membutuhkan akun Spotify yang memenuhi persyaratan Spotify + OAuth/PKCE.


### Fix terbaru
Versi ini menormalkan response RapidAPI TikTok secara rekursif dan mencoba `/index` lalu `/vid/index` jika endpoint utama tidak mengembalikan URL media. Frontend hanya memakai response normalisasi `video`, `music`, `title`.

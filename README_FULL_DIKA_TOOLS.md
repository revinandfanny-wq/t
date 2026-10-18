# Dika Tools — Full Build (Semua Permintaan)

Versi ini mempertahankan struktur/fungsi lama dan merangkum perubahan yang diminta.

## 1. Login & Dashboard
- Akun Developer bawaan: **username `Dika` / password `dev12`**.
- Developer dikunci sebagai akun sistem dan tidak dibuat ulang dari form.
- Dashboard menjadi pusat semua tool.
- Tool dibuka sebagai halaman luas/full-screen bila relevan.

## 2. Spotify — pencarian + player langsung
- Dashboard → Spotify membuka halaman Spotify full.
- Cari lagu/artis/album.
- Tombol **Putar** tidak dimaksudkan untuk sekadar membuka `open.spotify.com`.
- Full playback memakai Spotify Web Playback SDK setelah user login Spotify dan memenuhi syarat Spotify.
- Mini-player tetap ada ketika berpindah halaman.
- Play/pause/next/previous + Media Session.
- OAuth menggunakan Authorization Code with PKCE; Client Secret tidak ditaruh di HTML.
- Di halaman Spotify sekarang tersedia kolom **Tempel Spotify Client ID** sehingga tidak perlu mengedit kode untuk memasukkan Client ID.
- Redirect URI yang harus didaftarkan ditampilkan langsung di halaman Spotify.
- Preview tetap menjadi fallback jika full playback belum terhubung.

### Setup Spotify paling singkat
1. Pastikan akun Spotify yang dipakai memenuhi syarat Premium untuk Web Playback.
2. Buat app di Spotify Developer Dashboard.
3. Salin **Client ID**.
4. Buka Dika Tools → Spotify.
5. Tempel Client ID → **Simpan ID**.
6. Di Spotify Developer Dashboard, tambahkan **Redirect URI yang tampil di Dika Tools**.
7. Tekan **Login Spotify**.
8. Setelah berhasil, cari lagu → **Putar**.

**Jangan masukkan Client Secret ke HTML atau kirim Client Secret ke orang lain.**

## 3. Elysian AI
- Dashboard → Elysian AI membuka halaman chat yang luas.
- Jawaban tampil bertahap seperti sedang mengetik, bukan langsung muncul seluruhnya.
- Chat tetap berada di halaman AI dan dapat dibersihkan.

## 4. Unduhan
- Menu titik tiga → **Unduhan** membuka halaman Unduhan penuh.
- Riwayat download TikTok ditampilkan.
- Video yang berhasil di-cache dapat ditonton langsung di halaman tersebut.
- MP3 memiliki audio player.
- Ada Unduh Lagi, Hapus, dan Hapus Semua.
- Riwayat disimpan di localStorage dan media cache di IndexedDB.

## 5. TikTok → Galeri Android
APK harus memakai wrapper Android di folder `android/`.
- Android 10+ memakai MediaStore.
- Video → `Movies/Dika Tools/TikTok`.
- MP3 → `Music/Dika Tools`.
- Download native tidak memakai Base64 untuk file besar.
- Ada Toast sukses/gagal.
- Android <= 9 memakai permission storage + media scanner.

**Penting:** jika builder hanya mengambil `index.html` dan mengabaikan folder `android/`, penyimpanan langsung ke Galeri tidak akan aktif. Gunakan wrapper Android yang disertakan.

## 6. Support Developer / QRIS
- Menu titik tiga → **Support Developer**.
- QRIS sudah disertakan sebagai `qris-support.jpg`.
- User dapat melihat QRIS dan mengirim bukti transfer/gambar.
- Endpoint `/api/support.js` mengirim bukti ke email developer yang dikonfigurasi.
- Untuk email otomatis, set `RESEND_API_KEY` dan opsional `RESEND_FROM` pada environment server.
- Alamat penerima pada versi ini: `dikssswany@gmail.com`.

## 7. Environment server
Untuk deploy:
- `RAPIDAPI_KEY` → API TikTok RapidAPI. Key hanya di environment server, tidak di index.html.
- `RESEND_API_KEY` → pengiriman bukti Support Developer.
- `RESEND_FROM` → optional, alamat sender yang sudah diverifikasi pada provider.

Jangan menaruh secret server di `index.html`.

## 8. Batasan penting
- Spotify full playback bergantung pada aturan Spotify, login user, dan Premium.
- WebView/PWA tidak dapat menjamin playback setelah Android melakukan **Force Stop** pada aplikasi. Background/minimize/lock-screen bergantung pada Web Playback/Media Session dan wrapper.
- Penyimpanan Galeri native hanya aktif bila APK benar-benar dibangun memakai Android wrapper yang disertakan.

## Struktur utama
- `index.html` — UI + dashboard + Spotify + AI + download UI.
- `api/spotify.js` — pencarian Spotify.
- `api/tiktok.js` — API TikTok.
- `api/download.js` — proxy download.
- `api/support.js` — bukti Support Developer.
- `qris-support.jpg` — QRIS developer.
- `android/` — wrapper native Android untuk MediaStore.


## WEB → APK Telegram
Untuk builder yang hanya membungkus URL web, native MediaStore Java tidak ikut. Versi ini memakai endpoint download HTTP dengan Content-Disposition agar WebView/Download Manager dapat menangani file. Jika builder tidak memiliki DownloadListener/Download Manager, penyimpanan ke Galeri tidak dapat dipaksakan dari HTML saja.

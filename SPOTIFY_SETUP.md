# Dika Tools — Spotify Full Player

Fitur Spotify di versi ini sudah disiapkan untuk **Spotify Web Playback SDK**:
- Cari lagu dari halaman Spotify full-screen.
- Tekan **Putar** untuk lagu penuh langsung di Dika Tools setelah login Spotify.
- Mini player tetap tampil saat berpindah halaman.
- Play/pause/next/previous dan Media Session.
- Preview tetap tersedia bila pengguna belum login dan API menyediakan preview.

## Wajib untuk lagu penuh
Spotify mensyaratkan akun **Spotify Premium** untuk Web Playback SDK.

1. Buat aplikasi di Spotify Developer Dashboard.
2. Ambil **Client ID**.
3. Tambahkan Redirect URI yang sama persis dengan alamat aplikasi Dika Tools, misalnya:
   `https://domain-kamu.com/`
4. Buka `index.html` dan ganti:
   `GANTI_DENGAN_SPOTIFY_CLIENT_ID`
   dengan Client ID kamu.

Jangan masukkan Client Secret ke `index.html`.

## Batasan Android/PWA
Player web dapat terus berjalan ketika halaman/minimize masih hidup dan browser/WebView mengizinkan background media. Jika proses APK benar-benar dihentikan oleh Android (force-stop/swipe-kill tergantung perangkat), HTML/PWA tidak dapat menjamin musik tetap berjalan. Untuk perilaku seperti aplikasi musik native saat proses dimatikan, perlu foreground media service native Android.

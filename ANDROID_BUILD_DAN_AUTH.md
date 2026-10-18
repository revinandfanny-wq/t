# DIKSS TOOLS — Android wrapper, Google Login, Vercel

## Yang perlu diketahui
- Ini adalah proyek web asli dengan wrapper Android native (WebView), bukan proyek Flutter murni.
- Firebase Web API key memang boleh ada di frontend web; ia bukan password rahasia. Lindungi data dengan Firebase Security Rules dan backend, bukan menyembunyikan API key.
- Google login untuk situs harus memakai domain Vercel yang terdaftar pada Firebase Authentication > Settings > Authorized domains.
- Role Owner tidak boleh dipercaya dari localStorage/browser. Sebelum dipakai publik, pindahkan penetapan role ke backend tepercaya (misalnya Firebase Admin SDK/Firestore Rules). Akun selain rexees9@gmail.com harus tetap member. Jangan berikan hak owner hanya berdasarkan input dari client.
- Status akun dan trial adalah field terpisah di record lokal: status active, trial.enabled false, startedAt/expiresAt null. Data localStorage tidak persisten lintas perangkat dan bukan database aman.

## Android
1. Buka folder `android/` dengan Android Studio.
2. Di `android/app/src/main/java/com/dikatools/app/MainActivity.java`, ganti `WEB_APP_URL` dengan URL deployment Vercel sebenarnya.
3. Build > Build APK(s). APK belum dibangun atau diuji dari lingkungan ini.
4. Android WebView tidak selalu mendukung Firebase Google popup dengan baik. Jika tombol Google gagal di APK, integrasikan native Google Sign-In / Firebase Auth Android atau gunakan alur browser eksternal yang benar; jangan mengandalkan popup WebView.

## Vercel
- Proyek web statis: root directory adalah folder proyek yang berisi `index.html`; tidak memerlukan build command untuk halaman statis.
- API di folder `api/` perlu disesuaikan dengan runtime serverless Vercel; `index.js` Node server biasa tidak otomatis berjalan sebagai server persisten di Vercel.
- Tambahkan environment variables hanya untuk rahasia server seperti GROQ_API_KEY, RESEND_API_KEY, dan kredensial API terkait. Jangan masukkan rahasia server ke HTML.
- Untuk akun/role/trial lintas perangkat gunakan Firestore dengan Security Rules ketat atau database persisten lain. Banner lintas perangkat gunakan Firebase Storage atau object storage.
- Notifikasi browser meminta izin dari pengguna; notifikasi push saat aplikasi ditutup memerlukan service worker dan layanan push terkonfigurasi. Izin Android 13+ memerlukan POST_NOTIFICATIONS pada aplikasi native.

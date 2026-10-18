# Sistem Notifikasi Dikss Tools

## Yang aktif di versi ini
- Tombol meminta izin notifikasi browser (harus HTTPS dan dipicu klik pengguna).
- Preferensi lokal: izinkan notifikasi, suara, pengumuman Developer, dan promo.
- Pengumuman dapat menampilkan notifikasi browser pada perangkat yang membuatnya jika izin sudah diberikan.
- Service Worker menerima event `push` dan membuka halaman saat notifikasi diketuk.

## Batasan penting
Form pengumuman masih menyimpan data di `localStorage` browser/perangkat itu saja. Jadi ia **belum mengirim pengumuman ke semua akun**. Untuk push broadcast sungguhan, perlu backend/database bersama, penyimpanan subscription endpoint, VAPID keys, dan endpoint server yang mengirim Web Push. Jangan menaruh private VAPID key di `index.html`.

## Deploy
1. Upload seluruh isi ZIP ke proyek Vercel dan deploy ulang.
2. Buka situs melalui HTTPS.
3. Login, buka menu Notifikasi, lalu tekan **Aktifkan notifikasi perangkat** dan izinkan prompt browser.
4. Uji tombol tes. Jika pernah memilih Block, ubah izin situs dari pengaturan browser Android.

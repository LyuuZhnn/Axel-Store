# Axel Store

Website toko online statis dengan HTML5, CSS3, Vanilla JavaScript, localStorage, JSON, dan WhatsApp. Proyek ini dibuat terpisah dalam folder `axel-store/` dan ditujukan untuk GitHub Pages.

## Fitur

- Beranda dan sidebar pembeli yang berubah menjadi drawer pada layar kecil.
- Katalog dengan pencarian, filter kategori, dan pengurutan.
- Detail produk, wishlist, keranjang, validasi stok, checkout bertahap, riwayat pesanan lokal, dan tautan WhatsApp.
- Profil pelanggan lokal opsional; pembeli tetap dapat berbelanja sebagai tamu.
- Panel admin terpisah di `admin/index.html`, dengan sidebar kiri desktop dan drawer mobile.
- CRUD produk/kategori, status pesanan lokal, pengaturan toko/banner, backup dan import JSON.
- Identitas developer di footer sesuai teks yang diminta.

## Struktur

- `index.html`, `shop.html`, `product.html`, `cart.html`, `checkout.html`, `orders.html`, `wishlist.html`, `about.html`, `account.html`: halaman pembeli.
- `admin/index.html`: login/panel admin frontend.
- `css/`: stylesheet tema, komponen, responsif, admin.
- `js/`: `storage.js`, `products.js`, `cart.js`, `wishlist.js`, `app.js`, dan `admin.js` untuk logika toko.
- `assets/`: lokasi aset lokal.

## Menjalankan secara lokal

Bisa dibuka langsung dengan `index.html`, tetapi sebagian fitur browser seperti clipboard/API modern dapat berbeda berdasarkan browser. Untuk pengalaman yang lebih konsisten gunakan hosting statis atau editor preview statis. Tidak membutuhkan Express, PHP, atau backend.

## Mengatur WhatsApp toko

1. Buka `admin/index.html` pada origin website yang sama.
2. Pada kunjungan pertama, buat pengunci lokal minimum 8 karakter.
3. Masuk dan buka **Pengaturan Toko**.
4. Isi nomor WhatsApp dengan kode negara, misalnya awali Indonesia dengan `62`, tanpa tanda `+` atau spasi lebih disarankan.
5. Simpan. Uji tautan dari checkout sebelum membagikan website.

Pengunci tersebut hanya menyimpan hash sederhana pada browser dan sesi di `sessionStorage`; ini **bukan autentikasi aman**. Siapa pun yang memahami frontend atau memodifikasi browser dapat melewatinya. Jangan menyimpan rahasia atau menganggap admin terlindungi dari akses tidak sah. Untuk operasional produksi diperlukan backend/auth provider.

## Produk dan kategori

Tambahkan produk melalui Admin → Produk. Nama, harga, dan stok wajib valid. Gunakan URL gambar publik HTTPS atau tempatkan aset yang sah digunakan di folder `assets/`. File gambar yang hanya berada di perangkat admin tidak otomatis tersedia untuk pengunjung lain. Kategori dapat dikelola melalui menu Kategori.

Katalog awal sengaja kosong. Kategori bawaan disediakan sebagai struktur navigasi, bukan data transaksi. Tidak ada rating, ulasan, penjualan, pendapatan, ataupun diskon palsu.

## Data lokal dan privasi

Produk, kategori, keranjang, wishlist, pengaturan, profil, pesanan, dan pengunci disimpan pada browser/origin ini menggunakan `localStorage`. Data tidak otomatis tersinkronisasi antara browser/perangkat. Data pelanggan yang disimpan oleh browser pelanggan tidak otomatis terlihat oleh admin pada perangkat lain. Jangan menganggap riwayat pesanan lokal sebagai sistem order terpusat. Menghapus data situs/browser dapat menghapus data lokal. Ekspor pesanan memuat informasi pribadi; lindungi file tersebut.

Checkout menyimpan ringkasan pesanan lokal lalu menawarkan tautan WhatsApp. Membuka WhatsApp **tidak** membuktikan pesanan diterima penjual ataupun pembayaran berhasil. Nomor WA dan biaya kirim harus dikonfigurasi oleh pengelola; biaya kirim default adalah Rp0 sampai kamu mengaturnya.

## GitHub Pages

1. Buat repository baru bernama `Axel-Store` di https://github.com/ . Jangan menambahkan README/license otomatis apabila akan push folder lokal ini.
2. Ekstrak ZIP, buka terminal di folder `axel-store/` (pastikan `index.html` terlihat melalui `ls`).
3. Jalankan:

```bash
git init
git branch -M main
git add .
git commit -m "Initial commit Axel Store"
git remote add origin https://github.com/USERNAME/Axel-Store.git
git push -u origin main
```

Ganti `USERNAME` dengan username GitHub sebenarnya dan gunakan URL repo yang benar. Bila Git meminta identitas commit:

```bash
git config --global user.name "Nama GitHub Kamu"
git config --global user.email "Email GitHub Kamu"
```

Periksa remote yang ada sebelum mengubahnya:

```bash
git remote -v
# hanya jika belum ada:
git remote add origin https://github.com/USERNAME/Axel-Store.git
# jika sudah ada tetapi salah:
git remote set-url origin https://github.com/USERNAME/Axel-Store.git
```

4. Buka repository → **Settings → Pages**. Pada Source pilih **Deploy from a branch**, branch `main`, folder `/(root)`, lalu Save.
5. Setelah deployment selesai, GitHub akan menunjukkan URL. Pola project site biasanya `https://USERNAME.github.io/Axel-Store/`, tetapi URL itu belum aktif sampai repo dan deployment benar-benar ada.

Path halaman memakai link relatif agar dapat bekerja pada subpath project site. Jangan memindahkan `index.html` ke subfolder tanpa mengubah jalur aset/link.

## Memperbarui website

Di dalam folder repository:

```bash
git add .
git commit -m "Update Axel Store"
git push
```

Jika tidak ada perubahan, commit baru memang tidak dibuat. Jangan menggunakan `git push --force` sebagai langkah pertama ketika push ditolak; periksa URL remote dan riwayat repository dulu.

## Batasan dan pengujian

Website ini statis. Login admin frontend/localStorage bukan perlindungan produksi; tidak ada backend, pembayaran online, inventori terpusat, sinkronisasi pesanan, atau autentikasi server. Fitur WhatsApp hanya membuka draft pesan untuk dikirim pengguna. Uji kembali browser, ukuran layar, konfigurasi nomor WhatsApp, dan publikasi GitHub Pages sebelum dipakai secara nyata.

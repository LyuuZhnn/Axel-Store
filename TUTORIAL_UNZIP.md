# Tutorial Axel Store: ZIP, Unzip, Termux, GitHub, dan Pages

## 1. Ekstrak ZIP

### Android
1. Unduh `axel-store.zip` dari ChatGPT.
2. Buka aplikasi pengelola file dan masuk ke Downloads/Unduhan.
3. Pilih ZIP → Ekstrak.
4. Pastikan folder hasil ekstraksi hanya satu tingkat, lalu buka `axel-store/` sampai terlihat `index.html`, `admin/`, `css/`, `js/`, dan `assets/`.

### Termux
Pastikan ZIP berada di folder Download dan nama filenya persis:

```bash
termux-setup-storage
pkg install git unzip -y
mkdir -p ~/axel-store
unzip -o ~/storage/downloads/axel-store.zip -d ~/axel-store
cd ~/axel-store
find . -maxdepth 3 -name index.html
```

Arsip ini biasanya berisi folder `axel-store/`, jadi file utama bisa terletak di `~/axel-store/axel-store/index.html`. Jika begitu, masuk dulu ke folder itu dan lakukan Git di sana:

```bash
cd ~/axel-store/axel-store
ls -la
```

Jangan `git init` di folder induk yang tidak berisi `index.html`. Jika memilih ekstraksi lewat aplikasi file, buka terminal langsung dari folder proyek hasil ekstrak atau pindahkan folder proyek ke lokasi yang diketahui.

## 2. Buat repository

1. Buka https://github.com/ dan login.
2. Pilih New repository.
3. Isi nama `Axel-Store`.
4. Pilih Public atau Private sesuai kebutuhan.
5. Untuk push proyek yang sudah punya file, jangan centang README/license/.gitignore otomatis agar tidak menciptakan riwayat awal yang bentrok.
6. Buat repository lalu salin URL HTTPS-nya. URL contoh: `https://github.com/USERNAME/Axel-Store.git`.

## 3. Push dari Termux

Jalankan dari folder yang berisi `index.html` dan folder `css`, `js`, `admin`:

```bash
pkg install git -y
git init
git branch -M main
git add .
git commit -m "Initial commit Axel Store"
git remote add origin https://github.com/USERNAME/Axel-Store.git
git push -u origin main
```

Ganti `USERNAME`, dan pastikan URL repo tepat. Jika Git meminta identitas commit:

```bash
git config --global user.name "Nama GitHub Kamu"
git config --global user.email "Email GitHub Kamu"
```

Jika remote `origin` sudah ada, jangan menambahnya lagi dulu:

```bash
git remote -v
```

Bila URL salah:

```bash
git remote set-url origin https://github.com/USERNAME/Axel-Store.git
git remote -v
```

Jika muncul `nothing to commit`, berarti tidak ada perubahan baru untuk commit. Jika push ditolak karena riwayat berbeda, baca pesan error dan periksa apakah repository sudah memiliki commit dari GitHub sebelum memilih solusi. Jangan langsung force push.

## 4. Aktifkan GitHub Pages

1. Buka repo `Axel-Store` di GitHub.
2. Masuk ke Settings → Pages.
3. Pada Build and deployment, pilih Deploy from a branch.
4. Pilih branch `main` dan folder `/(root)`, lalu Save.
5. Tunggu sampai status deployment selesai dan buka URL yang diberikan GitHub.

URL project site biasanya `https://USERNAME.github.io/Axel-Store/`. Ganti username dan gunakan alamat aktual yang ditampilkan GitHub. Jangan menganggap website online sebelum deployment berhasil.

## 5. Update berikutnya

```bash
cd /path/ke/axel-store
git add .
git commit -m "Update Axel Store"
git push
```

Ganti path dengan folder repository yang benar. Jalankan hanya setelah file diubah.

## Catatan penting

Website memakai `localStorage`, sehingga data produk/pesanan tidak otomatis sinkron antara browser atau perangkat. Login admin frontend tidak aman untuk produksi. WhatsApp hanya menyiapkan draft pesan; penjual harus benar-benar menerima dan mengonfirmasi pesanan.

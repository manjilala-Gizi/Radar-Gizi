# RADAR Gizi: Panduan Pemasangan

*Rekap Analisis Determinan dan Area Rawan Gizi*  
Aplikasi dikembangkan oleh: **Ainun Thahirah H., Aminah Razaq dan Andi Marhamatul Ginayah** | Mahasiswa Prodi Gizi dan Dietetika Poltekkes Kemenkes Makassar.  
Dibimbing oleh **Manjilala, S.Gz, M.Gizi dan Dr. Nadimin, SKM, M.Kes**

Aplikasi pendamping e-PPGBM untuk analisis kuadran determinan masalah gizi dan penentuan desa prioritas intervensi.
Semua data diproses di perangkat pengguna dan tidak dikirim ke server mana pun.

## Isi folder `radar-gizi-pwa`

| File | Fungsi |
|---|---|
| `index.html` | Aplikasi utama, sudah memuat peta batas desa se-Sulawesi Selatan |
| `manifest.webmanifest` | Identitas aplikasi (nama, ikon, warna) agar bisa dipasang |
| `sw.js` | Service worker: menyimpan aplikasi agar tetap jalan tanpa internet |
| `lib/xlsx.full.min.js` | Pembaca file Excel (SheetJS 0.18.5, lisensi Apache-2.0) |
| `icons/` | Ikon aplikasi |
| `Template_RADAR_Gizi.xlsx` | Template kosong untuk petugas. Di aplikasi, tombol **Unduh template** juga bisa membuat template yang sudah berisi kode dan nama wilayah |

PWA wajib disajikan lewat **HTTPS**. Jika `index.html` dibuka langsung dari folder di komputer, aplikasi tetap berjalan, tetapi tidak bisa dipasang dan tidak bekerja offline.

---

## A. Menaruh aplikasi di internet (pilih salah satu)

### Opsi 1: GitHub Pages (disarankan: gratis, alamat tetap)
1. Buat akun di github.com, lalu klik **New repository**. Beri nama misalnya `radar-gizi`, pilih **Public**, lalu klik **Create repository**.
2. Klik **uploading an existing file**. Seret **semua isi** folder `radar-gizi-pwa` (bukan foldernya) ke halaman tersebut, termasuk folder `icons` dan `lib`, lalu klik **Commit changes**.
3. Buka **Settings → Pages**. Di bagian *Build and deployment*, pilih **Deploy from a branch**, branch **main**, folder **/(root)**, lalu klik **Save**.
4. Tunggu 1–3 menit. Alamat aplikasi akan tampil di halaman yang sama, misalnya
   `https://namaakun.github.io/radar-gizi/`

### Opsi 2: Netlify Drop (paling cepat, tanpa akun di awal)
1. Buka app.netlify.com/drop.
2. Seret folder `radar-gizi-pwa` ke halaman itu.
3. Aplikasi langsung mendapat alamat `https://….netlify.app`. Buat akun agar alamatnya tidak kedaluwarsa dan bisa diganti namanya.

### Opsi 3: Server institusi
Salin isi folder ke server web kampus yang sudah memakai HTTPS. Tidak perlu pengaturan khusus.

---

## B. Menampilkan aplikasi di Google Sites institusi

> **Penting:** Google Sites tidak mengizinkan aplikasi yang disematkan menyimpan data secara permanen. Data yang diunggah di dalam kotak sematan akan hilang saat browser ditutup. Karena itu, jadikan Google Sites sebagai **pintu masuk**: pasang tombol **"Buka RADAR Gizi"** (Sisipkan → Tombol) yang mengarah ke alamat aplikasi. Petugas bekerja di tab penuh atau di aplikasi yang sudah dipasang, karena di sana data tersimpan.

### Cara yang disarankan: sematkan lewat URL (sebagai pratinjau)
1. Buka halaman Google Sites, lalu klik **Sisipkan → Sematkan**.
2. Pilih tab **Menurut URL**, lalu tempel alamat aplikasi dari langkah A.
3. Pilih **Seluruh halaman**, lalu klik **Sisipkan**.
4. Perbesar kotak sematan sampai seluruh lebar halaman, dengan tinggi minimal setara satu layar penuh.
5. Di atas atau di bawah kotak, tambahkan:
   - tombol **"Buka aplikasi penuh"** yang mengarah ke alamat aplikasi. Di dalam Google Sites, tombol *Pasang aplikasi* tidak muncul, jadi pengguna perlu membuka alamat aslinya untuk memasang;
   - tautan **unduh template** dari Google Drive sebagai cadangan (unggah `Template_RADAR_Gizi.xlsx` ke Drive, lalu atur aksesnya ke *Siapa saja yang memiliki link*). Aplikasi sudah punya tombol unduh template, tetapi sebagian pengaturan Google Sites memblokir unduhan dari dalam kotak sematan.

### Cara cadangan: tempel kode (tanpa hosting)
Gunakan file `radar-gizi-google-sites.html` (terpisah dari folder PWA).
1. Klik **Sisipkan → Sematkan**, lalu pilih tab **Sematkan kode**.
2. Buka file tersebut dengan Notepad, salin seluruh isinya, lalu tempel.

Catatan: ukuran file ini sekitar 3,5 MB karena memuat peta se-Sulsel. Jika Google Sites menolak atau terasa lambat, gunakan cara URL di atas.

---

## C. Memasang di HP atau laptop
- **Android (Chrome):** buka alamat aplikasi, lalu ketuk **Pasang sebagai aplikasi** di panel kiri, atau menu ⋮ → **Instal aplikasi / Tambahkan ke layar utama**.
- **iPhone (Safari):** ketuk tombol **Bagikan → Tambahkan ke Layar Utama**.
- **Laptop (Chrome/Edge):** klik ikon pasang di ujung kanan kolom alamat.

Setelah dibuka sekali saat online, aplikasi tetap bisa dipakai tanpa internet.

---

## D. Memperbarui aplikasi
1. Ganti file yang berubah, misalnya `index.html`.
2. Buka `sw.js` dan naikkan angka versi pada baris `const CACHE = "radar-gizi-v1.8.0";`, misalnya menjadi `v1.8.1`.
3. Unggah ulang kedua file tersebut. Pengguna mendapat versi baru saat membuka aplikasi berikutnya, kadang setelah dibuka dua kali.

---

## E. Penyimpanan data dan tren
- Setiap file template yang diunggah dianggap **satu periode** sesuai isian *Bulan data* dan *Tahun data* di sheet Identitas. Jika diunggah lagi untuk bulan yang sama, data lama diganti.
- Beberapa file bisa dipilih sekaligus. Mulai dua periode, grafik **tren** dan daftar **perpindahan kuadran** muncul otomatis.
- Data **tersimpan otomatis di browser perangkat tersebut**. Saat aplikasi dibuka lagi di perangkat dan browser yang sama, data langsung muncul. Data tidak dikirim ke server mana pun.
- Data tersimpan bisa hilang jika riwayat atau data situs browser dihapus, atau jika aplikasi dibuka dalam mode penyamaran. Karena itu, biasakan menekan **Simpan cadangan** untuk mengunduh file `.json` ke komputer. File ini juga dipakai untuk memindahkan data ke laptop lain lewat tombol **Buka cadangan**.
- Di panel Data tertulis **Terakhir disimpan** (tanggal dan jam) serta **alamat aplikasi** tempat data itu tersimpan. Data hanya muncul lagi bila aplikasi dibuka dari alamat dan browser yang sama.
- Setiap selesai mengunggah file, aplikasi menawarkan **Simpan cadangan sekarang**. Satu klik langsung mengunduh file cadangan.
- Aplikasi menyimpan **salinan kedua** di browser (IndexedDB). Bila penyimpanan utama terhapus oleh bersih-bersih ringan, data dipulihkan otomatis dari salinan ini. Salinan ini tetap ikut hilang bila seluruh data situs dihapus, jadi file cadangan tetap pegangan utama.
- Pada komputer yang dipakai bersama, gunakan **Hapus semua data di perangkat ini** setelah selesai.

## F. Gambar dan laporan PDF
Grafik kuadran, peta, dan grafik tren masing-masing punya tombol **Unduh JPG** dan **Salin gambar**. Gambar dibuat berlatar putih, lengkap dengan judul, legenda, dan sumber. *Salin gambar* langsung bisa ditempel (Ctrl+V) di Word atau PowerPoint. Jika tombol ini tidak berfungsi, misalnya di dalam Google Sites, gunakan *Unduh JPG* atau buka aplikasi di tab penuh.

Tombol **Buat laporan PDF** di atas hasil analisis menyusun laporan A4: ringkasan kuadran, grafik, peta, tabel prioritas, capaian seluruh indikator, tren, kasus belum tertangani, arah tindak lanjut, catatan (opsional), dan kolom tanda tangan (Petugas Gizi dan Kepala Puskesmas; untuk Dinkes otomatis Pengelola Program Gizi dan Kepala Bidang Kesmas). Klik **Cetak / Simpan PDF**, lalu pilih **Simpan sebagai PDF** di jendela cetak. Laporan sebaiknya dibuat dari tab penuh atau aplikasi terpasang, bukan dari dalam Google Sites.

---

## G. Template per wilayah dan indikator
- Tombol **Unduh template (.xlsx)** membuka pilihan wilayah: puskesmas/kecamatan (centang desa wilayah kerja), kabupaten/kota (baris per desa atau per kecamatan), provinsi (24 kabupaten/kota), atau template kosong. Kode dan nama wilayah, kabupaten, kecamatan, bulan, dan tahun langsung terisi. Template dibuat di perangkat, jadi tetap bisa diunduh tanpa internet.
- Aplikasi menghitung 47 indikator dari dua sumber, masing-masing diberi label: **Gizi (Dinkes)** dan **Konvergensi Stunting** (31 indikator layanan intervensi stunting). Indikator yang ada di kedua sumber diberi kedua label.
- Kolom indikator Konvergensi Stunting di template bersifat opsional. Bila dikosongkan, indikatornya tidak muncul di aplikasi.
- Indikator balita 24-59 bulan dihitung otomatis dari kolom balita 0-59 bulan dikurangi kolom baduta 0-23 bulan. Makanan bergizi seimbang pada ibu hamil diukur dengan MDD-W (minimal 5 dari 10 kelompok pangan). Kolom pekarangan diisi Ada/Tidak.
- File template versi lama tetap bisa diunggah; indikator Konvergensi Stunting saja yang tidak muncul.

---

## H. Data per puskesmas, kecamatan, kabupaten/kota, dan provinsi
- **Satu puskesmas:** isi template dengan desa wilayah kerja puskesmas. Kolom `puskesmas` boleh kosong karena otomatis diambil dari sheet Identitas. Peta otomatis fokus ke desa-desa tersebut.
- **Dinas Kesehatan kabupaten/kota:** unggah semua file puskesmas untuk bulan yang sama sekaligus. File dengan bulan dan tahun yang sama otomatis **digabung**. Pilih **Unit analisis: Per puskesmas / Per kecamatan / Per desa**.
- **Dinas Kesehatan provinsi:** unggah rekap per desa dari kabupaten/kota, lalu pilih **Per kabupaten/kota** (peta 24 kabupaten/kota) atau **Per kecamatan**.
- Angka absolut dijumlahkan per unit, lalu persentase dan kuadran dihitung dari angka gabungan tersebut.
- **Data hanya per kecamatan/kabupaten:** isi `kode_wilayah` dengan kode 6 digit (kecamatan, misalnya 73.06.02) atau 4 digit (kabupaten/kota, misalnya 73.06), lihat sheet *Kode_Kec_Kab_Sulsel*. Aplikasi mengenali tingkat data dari panjang kode.
- **Kode desa** tetap kunci utama. Desa tanpa kode lengkap tidak ikut dihitung per kecamatan/kabupaten, dan aplikasi menampilkan peringatan.

---

## I. Sumber data dan catatan
- **Batas desa:** Batas Desa Maret 2020 (BIG/Kemendagri), Sulawesi Selatan, 3.044 desa/kelurahan. Bentuk poligon disederhanakan untuk tampilan. Danau Towuti, Matano, dan Tempe digambar biru muda. Wilayah yang diklaim lebih dari satu desa digabungkan ke desa yang tercatat pertama, semata-mata untuk keperluan tampilan peta.
- **Indikator dan target referensi:** RPJMN 2026, Laporan Tahunan Surveilans Gizi Dinkes Sulsel 2025, dan 31 indikator layanan intervensi stunting dalam aksi konvergensi daerah. Semua target bisa diubah di aplikasi.
- **Kerahasiaan:** template hanya berisi data agregat per desa, tanpa nama, NIK, atau alamat individu.

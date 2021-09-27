# 1 Dashboard

## 1.1 Import Fix Asset

Program khusus untuk menambahkan fix asset dengan import data type **csv** 

1. Klik Import.  lalu **Download Format** file csv nya . Masukkan data ke file csv.

   ![](img/fa-import.png)

2. Masukkan File yang sudah disiapkan , lalu klik preview

3. Jika Tidak ada yang error , scroll paling bawah klik **import**

4. Setelah itu periksa kembali data apakah sudah sesuai. Lalu Klik **Posting**

5. Data Automatis diproses program untuk di import ke Database **fix_asset dan fa_stok**

## 1.2 Tutup Tahun

Digunakan ketika penjurnalan keuangan tahun yang akan ditutup sudah selesai. Masukkan pin lalu klik **Tutup Tahun**.

## 1.3 Update Data

Digunakan untuk memperbarui data rekap jurnal perbulan. Agar Laporan Jurnal LR dan Neraca data yang ditampilkan dapat diperbarui. Data yang diolah adalah **glj_item** di rekap perbulan , data yang sudah direkap diupdate ke **master_gl** dan **glj_rekap**. Untuk Saldo Awal  diambil dari data **master_gl**

## 1.4 Import Buku Bank

Digunakan untuk import Transaksi Buku Bank yang belum diinput Admin. Daftar Akun yang di input Admin : 

1. Akuntan  & Konsultan : Diinput finance lewat login admin
2. Hutang Dagang : Diinput Admin ketika Pembayaran Tagihan
3. Kas Kecil: Diinput Admin ketika TopUp Petty Cash
4. Piutang Dagang : Diinput admin ketika Pembayaran Invoice
5. Pendapatan Lain2 : Diinput admin di Input Transaksi Bank
6. Uang Muka Penjualan : Diinput Admin di Input Transaksi Bank

Catatan Saat Import Buku Bank :

1. Khusus Akun Koreksi , diubah ke **Piutang Dagang** ketika Import Buku Bank.
2. Khusus Akun Tranfer Antar Bank, yang diinput hanya dari sisi penerima atau kredit.



Cara penggunaanya: 

1. Klik Import.  lalu **Download Format** file csv nya . Masukkan data ke file csv.

   ![](img/fa-import.png)

2. Masukkan File yang sudah disiapkan , lalu klik preview

3. Jika Tidak ada yang error , scroll paling bawah klik **import**. Proses yang terjadi Data tersimpan di **tmp_bank**

4. Setelah itu periksa kembali data apakah sudah sesuai. Lalu Klik **Posting**

5. Data Automatis diproses program untuk di import ke Database **bk_bank , glj, glj_item**. 



# 2 Data Master

## 2.1 Faktur

Lokasi : **Data Master :arrow_right:  Faktur**

Database yag digunakan  : **faktur dan invoice(mengetahui penggunaan faktur terakhir)**

![](img/faktur.png)

Berisi Data Faktur yang digunakan Untuk Tagihan Invoice Client. Cek Sisa Faktur setiap akan melakukan Invoice-an. 

1. Kode = 1

   Kode Faktur yang sedang digunakan. 

2. Kode = 2

   Kode Faktur ketika Kode faktur yang sedang digunakan habis maka akan berpindah ke kode 2.

## 2.2 GL System

Lokasi : **Data Master :arrow_right:  GL System**

Database yang digunakan : **gl_system**

Berisi Data GL System yang digunakan untuk lock Transaksi Admin seperti tutub bulan dan tutup tahun.

## 2.3 Master Cabang

Lokasi : **Data Master :arrow_right: Master Cabang**

Database yang digunakan : **master_cab**

Berisi daftar cabang yang ada di Datautama, digunakan sebagai berikut :

1. Mengelola Kode Cabang
2. Nama Pimpinan yang digunakan untuk Cetak Invoice dan Purchase Order
3. Nama Admin yang digunakan untuk Purchase Order
4. Seri adalah Urutan dari Cabang. Jika sekarang terdapat 5 cabang maka no seri Selanjutnya **06**
5. Detail , untuk mengisi detail Informasi Backoffice seperti Rekening Bank dan email digunakan pada cetak Invoice
6. Alamat, digunakan untuk data Alamat di Purchase Order
7. Kunci, merupakan kode [SHA1](https://md5decrypt.net/) yang digunakan untuk keamanan saat ingin membuka laporan teknisi.

## 2.4 Master Client

Lokasi : **Data Master :arrow_right: Master Cabang**

Database yang digunakan : **client**

Berisi Data Client semua Cabang, finance hanya dapat melihat dan mengedit data tersebut. Disarankan untk melihat data saja.

## 2.5 Master GL Account

Lokasi : **Data Master :arrow_right: Master GL Account**

Database yang digunakan : **master_gl**

Berisi daftar akun GL yang digunakan untuk Jurnal Keuangan. Untuk Keterangan Master Gl:

1. Kode Account : Kode Kunci sesuaikan dengan Format Sekarang.
2. Nama Account : Diisi sesuai nama akun
3. Tampil : Jika ingin menampilkan Kode tersebut di Transaksi Bank 
4. Jenis Account : Pilih Jenis Account (Asset, Liability, Incomce, Cost)
5. Kode Kategori : Pilih Kode Kategori sesuaikan dengan Akun GL 
6. Kode Cabang : Pilih Cabang mana yang akan digunakan
7. Saldo Awal  : Tentukan Saldo Awal, Tahun Berjalan. Saldo ini akan mempengaruhi Jurnal Keuangan
8. Kunci Status Bulanan : Digunakan untuk menyembunyikan Akun dari Transaksi Backoffice

## 2.6 Master G-Link

Lokasi : **Data Master :arrow_right: Master G-Link **

Database yang digunakan : **master_glink**

Berisi daftar Link Transaksi Jurnal Backoofice. Finance dapat menambahkan , mengedit dan menghapus Data (Disarankan untuk tidak menghapus dan mengedit data)

## 2.7 Master Kategori Account

Lokasi : **Data Master :arrow_right: Master Kategori Account **

Database yang digunakan: **master_ktg**

Berisi Jenis Kategori Account yang digunakan untuk Master GL Account. Finance dapat menambahkan , mengedit dan menghapus Data

## 2.8 Master Supplier

Lokasi  : **Data Master  :arrow_right: Master Supplier  **

Database yang digunakan : **supplierdu**

Finance Bertanggung Jawab Mengelola Data Supplier untuk semua cabang. Cara Pengisian Supplier:

1. Kode Supplier: Penentuan Kode Supplier  3 huruf pertama ditambah 2 angka. Misal **CV AGHNIA JAYA** maka kode nya AGH01, 01 adalah urutan kode , jika AGH01 sudah ada maka diganti menjadi AGH02
2. Status : Jika salah satu cabang masih menggunakan Supplier ini maka Status diisi Aktif
3. Jika Supplierr ber PPN maka pilih Ya pada **PKP**. dan Isi Data Pajak Supplier



# 3 Data Inventory & Inventaris

Berisi Data Master yang berhubungan dengan Inventory dan Inventaris

## 3.1 Master Barang

Lokasi : **Data Inventory & Inventaris :arrow_right: Master Barang**

Database yang digunakan : **i_barang, i_satuan**

Ketentuan input Barang :

1. Kode Barang : Maksimal Input 16 karakter. Kode barang harus unik dan menyerupai nama barang. Diperbolehkan menggunakan Karkater **huruf, angka , simbol (-)** saja.
2. Nama Barang : Maksimal Input 30 karakter
3. Satuan : Untuk Barang menggunakan **pcs** sedangkan kabel menggunakan satuan **box**.
4. Kode Merk : pilih merk , jika merk tidak tersedia input merk terlebih dahulu di Master Merk

## 3.2 Master Gudang

Lokasi : **Data Inventory & Inventaris :arrow_right: Master Gudang**

## 3.3 Master Jenis Barang

Lokasi : **Data Inventory & Inventaris :arrow_right: Master Jenis Barang**

## 3.4 Master Merk

Lokasi : **Data Inventory & Inventaris :arrow_right: Master Merk**

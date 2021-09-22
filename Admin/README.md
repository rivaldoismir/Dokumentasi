# 1 Data Client

**Admin** bertanggung jawab mengelola data client baik menambahkan client baru maupun mengedit data client. Data Client berguna untuk pembuatan [**Invoice**](#2-invoice)

**Database yang digunakan :** ***client** , **client_pkt***

## 1.1 Create Client

Untuk menambahkan **Data Client** bisa masuk ke **Data Master** :arrow_right: **Client** :computer_mouse: **Add Data** . Data yang perlu dipersiapkan * : 

1. Kode Client : diisi dengan Huruf Besar dan angka, dapat diisi 3 - 6 Karakter

2. Status : diisi aktif jika client masih aktif

3. Nama Client : diisi dengan nama client, untuk penggunaan simbol hanya diperbolehkan menggunakan [  **+ , . - ( )** ]

4. Keterangan : 
   1. **Client Bulanan** (Untuk client yang ditagih secara bulanan)
   2. Client Onetime (Untuk client yang ditagih secara onetime)
   3. Client Titipan (Client Titipan berguna untuk Ticketting Helpdesk)
   4. BTS (Digunakan untuk Ticketting Helpdesk)
   
5. **Alamat Lengkap** : diisi alamat client

6. Data PIC Client (Nama) : diisi nama PIC Client

7. Data PIC Client (No. Telepon) : diisi no telpon PIC client 

8. Data Admin (Marketting in charge) : diisi nama marketting

9. Data Admin (Tanggal MOU) : diisi tanggal MOU untuk client baru maka Tanggal MOU dan Tanggal Berlangganan sama

10. Data Admin (Waktu Kontrak) : diisi waktu kontrak dalam hitungan bulan

11. Data Lainnya (Alamat Pengiriman) : diisi jika alamat pengiriman pada invoice berbeda dengan [alamat lengkap](#11-create-client). untuk format penuliasannya **NamaClient#Alamat Pengiriman**. Contohnya 

    > Alamat Pengiriman : Kantor Dinas Perhubungan Semarang#Jl. Mekar Sari No. 20

## 1.2 Edit Client

Untuk mengedit **Data Client** bisa masuk ke **Data Master** :arrow_right: **Client** :pencil:**Edit Client**  . Data tambahan yang di edit yaitu :

1.  No. Urut Invoice Auto : diisi angka lebih dari 0, sesuaikan dengan urutan Invoice Auto yang akan dicetak (angka boleh sama).

2. Data Detail Layanan : Diinput untuk client dengan keterangan **Client Bulanan** . 

   ![](https://github.com/rivaldoismir/Dokumentasi/blob/main/Admin/img/Client-Layanan.png) 

   1. Kategori Penjualan diisi sesuai ketentuan berikut ini :
      1.	BANDWIDTH : UNTUK TAGIHAN BANDWIDTH BULANAN
      2.	INSREG : HANYA UNTUK INSTALASI KLIEN BULANAN
      3.	LAIN2 :
         1.	ANNUAL FEE (UNTUK KLIEN DU SMRG)
         2.	JASA ONE TIME (PENARIKAN KABEL, SETTING AKSES POINT, SETTING RADIO, SETTING CCTV)
      4.	COLOCATION : COLOCATION SERVER / ANTENA (ADA KLIEN YANG MENITIPKAN PERANGKATNYA DI LAHAN DU)
      5.	DOMAIN/HOSTING : BIAYA DOMAIN (TAHUNAN), HOSTING (BULANAN)
      6.	IP : SEWA IP ADDRESS
      7.	INFRASTRUKTUR :
         1.	PEMBELIAN PERANGKAT SEKALIGUS DENGAN JASANYA YANG SIFATNYA ONE TIME, MISALNYA : ADA PEMBANGUNAN JARINGAN LOKAL LAN DI SEBUAH HOTEL, DATAUTAMA MENJUAL PERANGKAT SEKALIGUS JASA PENARIKAN KABELNYA.
         2.	SEWA INFRASTRUKTUR (UNTUK KLIEN DU SMG-MSM)
      8.	PERANGKAT : JIKA HANYA MENJUAL PERANGKATNYA SAJA, TANPA JASA SETTING DLL.
   2. Deskripsi : input keterangan
   3. Tambahan Periode : Pilih **YA** , jika Deskripsi ada keterangan Periode Tanggal
   4. Nominal Tagihan : diisi tagihan sebelum PPN

   

# 2 Invoice

**Admin** bertanggung jawab membuat Invoice Bulanan maupun Onetime. 

Database yang digunakan invoice auto dan invoice baru : **invoice, invoice_item, glj, glj_item, saldo_client**

Database yang digunakan Pembayaran Invoice : **tmp_bayar_invoice (temporary) , glj, glj_item, saldo_client, bk_bank, bayar_invoice, bayar_invoice_item**

## 2.1 Invoice Auto

Lokasi dari Invoice Auto : **Transaksi :arrow_right:  Penjualan :arrow_right:  Invoice Auto** 

Invoice Auto merupakan fitur baru dari Backoffice untuk mempercepat pembuatan invoice bulanan secara automatis, pembuatannya mulai H-4 sampai H+3 di bulan berjalan Invoice dan  dengan syarat Client :

1. Client memiliki 1 Invoice sebelumnya. Digunakan untuk mengambil data kode faktur 
2. Termasuk Client Bulanan
3. Client Valid : Sisa Kontrak dan Layanan ada

## 2.2 Invoice Baru

Lokasi dari Invoice Baru : **Transaksi** :arrow_right: **Penjualan** :arrow_right: **Invoice Baru** :fast_forward: **pilih Client**  

Invoice Baru bisa digunakan untuk Penjualan Onetime maupun Bulanan jika tidak dapat menggunakan Invoice Auto

**Jurnal Yang terbentuk dari Invoice Auto dan Invoice Baru** :

Jenis Jurnal yang dipakai  **INV**

| AKUN           |      DEBET |     KREDIT |
| -------------- | ---------: | ---------: |
| PIUTANG DAGANG | 11.010.000 |            |
| PENJUALAN *    |            | 10.000.000 |
| HUTANG PPN     |            |  1.000.000 |
| METERAI        |            |     10.000 |

## 2.3 Pembayaran Invoice

Lokasi dari Pembayaran Invoice : **Transaksi** :arrow_right: **Penjualan** :arrow_right: **Pembayaran Invoice** :fast_forward: **pilih Client**  

Digunakan untuk melunasi invoice client ketika client sudah membayar invoice tersebut. Jika client hanya membayar sebagian maka pilih **Bayar Sebagian** dan isi nominal serta potongan jika ada.

**Berikut Jurnal Jenis -  Jenis Pembayaran Invoice :**

Jenis Jurnal yang dipakai  **BIN**

### 2.3.1 Pembayaran Full

| AKUN           |      DEBET |     KREDIT |
| -------------- | ---------: | ---------: |
| BANK           | 11.010.000 |            |
| PIUTANG DAGANG |            | 11.010.000 |

### 2.3.2 Pembayaran dengan Potongan Meterai

| AKUN           |      DEBET |     KREDIT |
| -------------- | ---------: | ---------: |
| BANK           | 11.000.000 |            |
| BIAYA LAIN2    |     10.000 |            |
| PIUTANG DAGANG |            | 11.010.000 |

### 2.3.3 Pembayaran dengan PPh 23

Jika PPh 23 tidak sesuai dapat menggunakan Custom Nominal PPh dan tetap ceklist PPh 23

| AKUN             |      DEBET |     KREDIT |
| ---------------- | ---------: | ---------: |
| BANK             | 10.810.000 |            |
| UM. PPh Pasal 23 |    200.000 |            |
| PIUTANG DAGANG   |            | 11.010.000 |

### 2.3.4 Pembayaran dengan biaya lain-lain maupun biaya tranfer

| AKUN           |      DEBET |     KREDIT |
| -------------- | ---------: | ---------: |
| BANK           | 11.005.000 |            |
| BIAYA LAIN2    |      5.000 |            |
| PIUTANG DAGANG |            | 11.010.000 |

### 2.3.5 Pembayaran dengan Diskon Penjualan

| AKUN             |      DEBET |     KREDIT |
| ---------------- | ---------: | ---------: |
| BANK             | 10.010.000 |            |
| DISKON PENJUALAN |  1.000.000 |            |
| PIUTANG DAGANG   |            | 11.010.000 |

### 2.3.6 Pembayaran dengan PPh 4 Ayat 2

| AKUN           |      DEBET |     KREDIT |
| -------------- | ---------: | ---------: |
| BANK           | 10.010.000 |            |
| UM. PPh Final  |  1.000.000 |            |
| PIUTANG DAGANG |            | 11.010.000 |

### 2.3.7 Pembayaran dengan PPh 22

| AKUN             |      DEBET |     KREDIT |
| ---------------- | ---------: | ---------: |
| BANK             | 10.860.000 |            |
| UM. PPh Pasal 22 |    150.000 |            |
| PIUTANG DAGANG   |            | 11.010.000 |

## 2.4 Laporan

Lokasi : **Laporan** :arrow_right: **Penjualan**  

Laporan yang terbuat dari transaksi invoice maupun pembayaran invoice : 

### 2.4.1 Laporan Invoice

Untuk mencetak laporan 1 Invoice menggunakan **Laporan Invoice**, sedangkan untuk **Laporan Invoice Periode** dapat mencetak laporan lebih dari satu dengan syarat per invoice 1 halaman.

Data diambil dari database **invoice dan invoice_item** 

### 2.4.2 Laporan Pembayaran Invoice

Berisi Daftar Pembayaran Invoice beserta informasi Bank

Ambil dari database **bayar_invoice , bayar_invoice_item , bk_bank**

### 2.4.3 Laporan Piutang Dagang

Berisi Piutang Dagang per Client yang diambil dari **saldo_client**.  Untuk Saldo Awal mulai 2021 diambil dari database **client** 

Data Laporan diambil dari database **saldo_client , bk_bank , client**

### 2.4.4 Laporan Piutang Periode

Berisi Detail Layanan Invoice dan Pembayaran Invocie yang diambil dari database **saldo_client**. Bisa filter berdasarkan periode tanggal invoice.

### 2.4.5 Saldo Piutang Dagang

Berisi informasi Saldo Akhir Client yang dapat ditentukan tanggal saldo akhirnya. Informasi juga dapat diexport ke Excel.

Data Laporan diambil dari database **saldo_client dan client**

### 2.4.6 Laporan Invoice Monthly

Berisi informasi Invoice Bulan yang difilter per Bulan yang dapat dicetak PDF maupun export excel

Data diambil dari database **invoice** dan **client** 



# 3 PETTY CASH

Ketentuan Input Petty Cash :

- Jika ada pembelian Perangkat yang merupakan Jenis Inventaris misal beli **Mikrotik powerline PL 7411** di tokped seharga 660.000 ongkir 10.000 maka saat pembuatan petty cash itu dipisah yang mikrotik dengan kode Inventaris Perangkat 660.000 , Sedangkan ongkir masukkan ke Kode Ekspedisi
- Jika ada Pembayaran Biaya Tenaga Ahli atau yang berhubungan dengan pajak misal sebesar 12.000.000, dipotongkan untuk PPh 21 sebesar 2.5% hingga 3% atau 300.000. Yang diinput di **Input Petty Cash**  sebesar 11.700.000 dengan kode Biaya Tenaga Ahli. Sedangkan 300.000 diinput di **Hutang Pajak** untuk debet (**Biaya Tenaga Ahli**) dan kreditnya (**Hutang PPh 21**) 

## 3.1 Input Petty Cash

Lokasi : **Petty Cash :arrow_right: Input** 

Digunakan admin untuk input petty cash data tersebut masuk ke Database (sebelum rekap transaksi) **tmp_pcash**. Setelah semua data dicek selanjutnya direkap transaksi untuk menjadikan sebuah laporan. 

Data tersebut masuk ke Database : **saldo_pcash, pcash, pcash_item, glj, glj_item**

Jenis Jurnal yang dipakai  **PET** , untuk pusat menggunakan **PET-PST**

Jurnal yang terbuat dari Petty Cash tersebut

| AKUN                |   DEBET |  KREDIT |
| ------------------- | ------: | ------: |
| Administrasi Kantor | 100.000 |         |
| Bahan Bakar         |  15.000 |         |
| KAS KECIL           |         | 115.000 |

## 3.2 TopUp Petty Cash

Lokasi : **Petty Cash :arrow_right:  Top-up** 

Top Up Saldo Petty Cash sesuaikan TopUp bank. Pastikan Saldo Petty Cash Sesuai dengan Saldo Real. History TopUp yang ditampilkan 40 item.

Database yang digunakan  : **bk_bank, saldo_pcash, glj, glj_item**  

Jenis Jurnal yang dipakai  **TOP** , untuk pusat menggunakan **TOP-PST**

Jurnal yang terbuat dari Petty Cash tersebut

| AKUN       |   DEBET |  KREDIT |
| ---------- | ------: | ------: |
| Petty Cash | 100.000 |         |
| Bank       |         | 100.000 |

## 3.3 Hutang Pajak

Seperti yang dijelaskan pada contoh kasus diatas pada **3 Petty Cash** . Input Hutang Dagang Pajak Petty Cash digunakan untuk potongan PPh. 

Database yang digunakan : **glj, glj_item**

Jenis jurnal yang digunakan : **PPH-PC**

## 3.4 Laporan Petty Cash

Lokasi : **Laporan :arrow_right: Petty Cash**

Laporan yang terbentuk pada transakasi Petty Cash  :

### 3.4.1 Mutasi Petty Cash 

Yang ditampilkan mutasi Petty Cash debet dan kredit

Data diambil dari Database : **saldo_pcash**

### 3.4.2 Petty Cash

Menampilkan Item dari Petty Cash yang dapat di Export Excel untuk laporan bulanan.

Database yang digunakan : **pcash_item**

### 3.4.3 Cetak Petty Cash

Menampilkan Laporan Rekap Petty Cash. Selain itu khusus Petty Cash terakhir jika Petty Cash tersebut ada revisi maka dapat 



# 4 Pembeliaan




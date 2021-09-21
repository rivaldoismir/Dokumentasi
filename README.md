# 1 Data Client

**Admin** bertanggung jawab mengelola data client baik menambahkan client baru maupun mengedit data client. Data Client berguna untuk pembuatan **Invoice**

**Database yang digunakan :** ***client** , **client_pkt***

## 1.1 Create Client

Untuk menambahkan **Data Client** bisa masuk ke **Data Master :arrow_right: Client :computer_mouse: Add Data **. Data yang perlu dipersiapkan * : 

1. Kode Client : diisi dengan Huruf Besar dan angka, dapat diisi 3 - 6 Karakter

2. Status : diisi aktif jika client masih aktif

3. Nama Client : diisi dengan nama client, untuk penggunaan simbol hanya diperbolehkan menggunakan [  **+ , . - ( )** ]

4. Keterangan : 
   1. Client Bulanan (Untuk client yang ditagih secara bulanan)
   2. Client Onetime (Untuk client yang ditagih secara onetime)
   3. Client Titipan (Client Titipan berguna untuk Ticketting Helpdesk)
   4. BTS (Digunakan untuk menambahkan)
   
5. Alamat Lengkap : diisi alamat client

6. Data PIC Client (Nama) : diisi nama PIC Client

7. Data PIC Client (No. Telepon) : diisi no telpon PIC client 

8. Data Admin (Marketting in charge) : diisi nama marketting

9. Data Admin (Tanggal MOU) : diisi tanggal MOU

10. Data Admin (Waktu Kontrak) : diisi waktu kontrak dalam hitungan bulan

11. Data Lainnya (Alamat Pengiriman) : diisi jika alamat pengiriman pada invoice beda dengan alamat lengkap. untuk formatnya **Nama/Kantor Penerima#Alamat Pengiriman**. 

    

## 1.2 Edit Client

Untuk mengedit **Data Client** bisa masuk ke **Data Master :arrow_right: Client :pencil:Edit Client  **. Data tambahan yang di edit yaitu :

1.  No. Urut Invoice Auto : diisi angak lebih dari 0, sesuaikan dengan urutan Invoice Auto yang akan dicetak boleh, angka boleh sama.

2. Data Detail Layanan : Diinput untuk client dengan keterangan **Client Bulanan** . 

   ![](D:\Master_Kerja\Dokumentasi\img\Client-Layanan.png)

   1. Kategori Penjualan diisi sesuai ketentuan berikut ini :
      1.	BANDWIDTH : UNTUK TAGIHAN BANDWIDTH BULANAN
      2.	INSREG : HANYA UNTUK INSTALASI KLIEN BULANAN
      3.	LAIN2 : 
      A.	ANNUAL FEE (UNTUK KLIEN DU SMRG)
      B.	JASA ONE TIME (PENARIKAN KABEL, SETTING AKSES POINT, SETTING RADIO, SETTING CCTV)
      4.	COLOCATION : COLOCATION SERVER / ANTENA (ADA KLIEN YANG MENITIPKAN PERANGKATNYA DI LAHAN DU)
      5.	DOMAIN/HOSTING : BIAYA DOMAIN (TAHUNAN), HOSTING (BULANAN)
      6.	IP : SEWA IP ADDRESS
      7.	INFRASTRUKTUR :
      A.	 PEMBELIAN PERANGKAT SEKALIGUS DENGAN JASANYA YANG SIFATNYA ONE TIME, MISALNYA : ADA PEMBANGUNAN JARINGAN LOKAL LAN DI SEBUAH HOTEL, DATAUTAMA MENJUAL PERANGKAT SEKALIGUS JASA PENARIKAN KABELNYA.
      B.	SEWA INFRASTRUKTUR (UNTUK KLIEN DU SMG-MSM)
      8.	PERANGKAT : JIKA HANYA MENJUAL PERANGKATNYA SAJA, TANPA JASA SETTING DLL.
   2. Deskripsi : input keterangan
   3. Tambahan Periode : Pilih **YA** , jika Deskripsi ada keterangan Periode Tanggal
   4. Nominal Tagihan : diisi tagihan sebelum PPN

   

# 2 Invoice

**Admin** bertanggung jawab membuat Invoice Bulanan maupun Onetime. 

**Database yang digunakan invoice auto dan invoice baru :** ***invoice, invoice_item, glj, glj_item, saldo_client* **

**Database yang digunakan Pembayaran Invoice :** ***tmp_bayar_invoice (temporary) , glj, glj_item, saldo_client, bk_bank, bayar_invoice, bayar_invoice_item* **

## 2.1 Invoice Auto

Lokasi dari Invoice Auto : **Transaksi :arrow_right:  Penjualan :arrow_right:  Invoice Auto** 

Invoice Auto merupakan fitur baru dari Backoffice untuk mempercepat pembuatan invoice bulanan secara automatis, pembuatannya mulai H-4 sampai H+3 di bulan berjalan Invoice dan  dengan syarat Client :

1. Client memiliki 1 Invoice sebelumnya. Digunakan untuk mengambil data kode faktur 
2. Termasuk Client Bulanan
3. Client Valid : Sisa Kontrak dan Layanan ada

## 2.2 Invoice Baru

Lokasi dari Invoice Baru : **Transaksi :arrow_right: Penjualan :arrow_right: Invoice Baru :fast_forward: pilih Client  **

Invoice Baru bisa digunakan untuk Penjualan Onetime maupun Bulanan jika tidak dapat menggunakan Invoice Auto

**Jurnal Yang terbentuk dari Invoice Auto dan Invoice Baru** :

| AKUN           |      DEBET |     KREDIT |
| -------------- | ---------: | ---------: |
| PIUTANG DAGANG | 11.010.000 |            |
| PENJUALAN *    |            | 10.000.000 |
| HUTANG PPN     |            |  1.000.000 |
| METERAI        |            |     10.000 |

## 2.3 Pembayaran Invoice

Lokasi dari Pembayaran Invoice : **Transaksi :arrow_right: Penjualan :arrow_right: Pembayaran Invoice :fast_forward: pilih Client ** 

Digunakan untuk melunasi invoice client ketika client sudah membayar invoice tersebut. Jika client hanya membayar sebagian maka pilih **Bayar Sebagian** dan isi nominal serta potongan jika ada.

**Berikut Jurnal Jenis -  Jenis Pembayaran Invoice :**

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

Laporan yang terbuat dari transaksi invoice maupun pembayaran invoice

Lokasi : **Laporan :arrow_right: Penjualan  ** 

### 2.4.1 Laporan Invoice

Untuk mencetak laporan satuan menggunakan Laporan Invoice, sedangkan untuk Laporan Invoice Periode dapat mencetak laporan lebih dari satu dengan syarat per invoice 1 halaman.

Ambil dari database **invoice dan invoice_item** 

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

Data diambil dari database **invoice dan client **




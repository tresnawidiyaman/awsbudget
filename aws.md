# Budgeting AWS
Resource utama: https://aws.amazon.com/pricing/.
Catatan: Harga yang tertera adalah untuk regian asia pasifik singapore(ap-southeast-1). Harga diregion lain akan berbeda, mungkin bisa lebih murah atau lebih mahal.

# Tujuan
Di bab ini, siswa diharapkan sadar terhadap penggunaan setiap layanan, akan berimbas pada pengeluaran rutin AWS. Dan siswa diharapkan mampu menghitung biaya pengeluaran rutin ketika merancang solusi cloud. Hitungan biaya yang timbul dalam suatu solusi cloud merupakan salah satu pertimbangan apakah sebuah rencana solusi bisa diterima semua pihak.

# Mengakses menu billing
Menu ini memungkinkan kita memantau berapa budget yang sudah terpakai di bulan berjalan. Menu dapat diakses dari menu kanan atas. Nama Accunt>My Billng Dashboard. Atau pada tautan https://console.aws.amazon.com/billing/home?region=ap-southeast-1#/. 

Menu ini dapat dilihat untuk user root atau user IAM lainnya yang sudah mendapat akses billing. Billing bulanan akan dihitung pertanggal 1 tiap bulannya. Setelah itu sistem akan mengirimkan tagihan pemakaian ke alamat root account untuk segera dibayarkan sebelum jatuh tempo. Pembayaran bisa menggunakan auto debet (CC) atau penagihan manual. Keterlambatan pembayaran tagihan dari masa tenggang pembayaran bisa mengakibatkan akun aws diblok, layanan server non aktie. Sehingga mengundang resiko kehilangan data di server. Berikut tampilan biling dashboard:
(gambar)

# Kalkulator billing
AWS menyedikan simulasi berapa harga yang harus dibayar untuk satu bulan jika menggunakan layanannya.
Kalkulator dapat diakses pada tautan berikut: https://calculator.s3.amazonaws.com/index.html

# Type Pembayaran
## Pay-As-You-Go / On Demang Picing
Metode ini merupakan tipe pembayaran paling populer karena paling mudah dengan biling perjam. Biasanya metod ini dianjurkan untun mesin/service yang masih dalam mode riset sehingga membutuhkan perubahan masa pakai maupun tipe mesin sesering mungkin.

## Reserved Instances
Metod ini merupakan metod pembayaran langganan. Satuan billing dihitung dalam pembulatan perbulan. Metod ini dianjurkan untuk mesin/service yang sudah ditemukan spek stabil jangka panjangnya. Sehingga kecil kemungkinan ada perubahan spek lagi. Dalam penerapannya, metod ini menghasilkan harga per service lebih murah untuk pemakaian dalam jangka panjang, misal kontrak setahun. Selisih dengan method pay-as-you-go bisa mencapai 75% lebih murah.

# Point - point yang menjadi itungan billing

* EC2
* Storage, SSD, HDD, Snapshot, Backup
* RDS
* Elastic IP
* ELB
* S3
* Route53
* Network

# EC2
Tautan: https://aws.amazon.com/ec2/pricing/on-demand/
Harga EC2 yang kita bayar hanya menghitung jumlah core dan ram yang digunakan. Oleh sebab itu untuk mempermudah pengguna, AWS telah menyediakan templet tipe server sesuai kebutuhan user. Harga yang tertera biasanya merupakan tarif perjam untuk pembayaran pay-as-you-go. Sedangkan untuk hitungan perbulan dihitung sebagai 1bulan = 720jam. Harga ini juga akan berbeda untuk tiap region, jenis generasi processor dan type peruntukan.

Type yang akan kita gunakan lebih sering adalah tipe
* T2.(xxx)
* T3.(xxx)
Kami menyarankan menggunakan tipe t3, sebagai templet tipe server yang menggunakan generasi processor lebih baru.

Berikut terlampir harga type EC2 untuk region AP-2 (Singapore) dengan OS Ubuntu Linux. (Gambar)

# Storage
Tautan: https://aws.amazon.com/ebs/pricing/
Storage yang digunakan adalah EBS, Elastic Block Storage.

EBS menyediakan beberapa tipe penyimpanan, diantaranya:
* General SSD (GP2). Ini merupakan tipe penyimpanan yang akan kita pakai secara bawaan.
* EBS Snapshots, Ini adalah tipe penyimpanan yang biasa kita gunakan untuk backup snapshot.

Untuk harga adalah sebagai berikut:
* GP2: $0.12 per GB-month of provisioned storage
* EBS Snapshots: $0.05 per GB-month of data stored

# RDS
Tautan: https://aws.amazon.com/rds/pricing/
Untuk database keluarga MySQL dan Postgresql, harga yang dibayar berasal dari jumlah Core dan Ram yang digunakan. Namun komposisi core dan RAM sudah menjadi kesatuan template. Setelah itu harga RDS ditambah dengan penggunaan storage untuk data, backup dan snapshot. Ini karena untuk mode RDS terdapat mekanisme auto backup snapshot dalam tenggat waktu tertentu.

## Harga Resource Compute

Berikut tipe RDS Mariadb yang biasa dipakai beserta harganya untuk on-demand/pay-as-you-go:
https://aws.amazon.com/rds/mariadb/pricing/?pg=pr&loc=4
(Gambar)

## Harga Storage
* General Purpose (SSD) Storage 	$0.138 per GB-month

## Data Transport
Ini adalah harga yang dibayar untuk bandwith. Harganya memang tidak terlalu mahal. Namun sebagai pos pengeluaran rutin, wajib kita ketahui.

### Data Transfer IN To Amazon RDS From Internet
* All data transfer in 	$0.00 per GB

### Data Transfer OUT From Amazon RDS To Internet
* Up to 1 GB / Month 	$0.00 per GB
* Next 9.999 TB / Month 	$0.12 per GB

# Elastic IP
Elastic IP adalah alamat IP yang kita sewa sehingga IP ini secara teknis hanya untuk kita dan tidak bisa digunakan orang lain. Sehingga jika tidak digunakana kan dikenakan biaya rutin sebagai berikut:

* $0.005 per additional IP address associated with a running instance per hour on a pro rata basis
* $0.005 per Elastic IP address not associated with a running instance per hour on a pro rata basis

# S3
Tautan: https://aws.amazon.com/s3/pricing/
S3 adalah layanan penyimpanan object. bentuk penyimpanan berupa bucket.
Berikut harga layanan ini:
## S3 Standard - General purpose storage for any type of data, typically used for frequently accessed data	
* First 50 TB / Month	$0.025 per GB
* Next 450 TB / Month	$0.024 per GB

# Route53
Adalah layanan pengelola DNS. Berikut tarifnya.

## Hosted Zones and Records
* $0.50 per hosted zone / month for the first 25 hosted zones
* $0.10 per hosted zone / month for additional hosted zones

# ELB
Tautan: https://aws.amazon.com/elasticloadbalancing/pricing/

Harga ELB diitung dari banyaknya ELB yang dibuat, tipe ELB dan Banwith yang dihabiskan. Berikut harga perkiraan ELB:

* $0.028 per Classic Load Balancer-hour (or partial hour)
* $0.008 per GB of data processed by a Classic Load Balancer

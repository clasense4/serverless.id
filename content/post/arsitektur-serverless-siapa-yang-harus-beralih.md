+++
title = "Arsitektur Serverless? Siapa yang harus beralih?"
author = "fajriabdillah"
share = true
tags = ["serverless"]
draft = false
menu = ""
image = "images/default.jpg"
slug = "arsitektur-serverless-siapa-yang-harus-beralih"
date = "2017-06-23T02:20:24+07:00"
comments = true
+++

>>> Pastikan anda sudah memahami apa itu serverless, dan [kenapa harus beralih](/post/arsitektur-serverless-kenapa-harus-beralih/).

<!--more-->

![ Who-wants-change-Who-wants-to-change.jpg ](/images/arsitektur-serverless-siapa-yang-harus-beralih/Who-wants-change-Who-wants-to-change.jpg "Who want to change?")

### Startup yang mengejar MVP

Startup secara mudah bisa Kita artikan perusahaan yang sedang merintis, dengan jumlah pegawai yang masih sedikit. Sedikit ini relatif, ada yang bilang satu orang bisa membangun startup seperti [Apex Ping](https://www.indiehackers.com/businesses/apex-ping) (FYI, TJ Holowaychuk juga membuat salah satu framework serverless yaitu [Apex](http://apex.run/)), atau dua orang seperti [Indie Hackers](https://www.indiehackers.com/blog/acquired-by-stripe), atau yang cukup banyak dengan 15 orang seperti [Less anoyying CRM](https://www.indiehackers.com/businesses/less-annoying-crm).

MVP yang dimaksud adalah [Minimun Viable Product](https://en.wikipedia.org/wiki/Minimum_viable_product), bukan MVP dalam Ragnarok Online, bukan juga MVP seekor monyet dalam film Most Valuable Primate. Produk yang akan dibuat, sudah bisa memuaskan pengguna, memudahkan hidup pengguna dan bisa menyelesaikan masalah dengan adanya produk ini.

Arsitektur serverless akan sangat memangkas waktu yang dibutuhkan untuk membuat sebuah produk, jika produk yang ditawarkan adalah sebuah aplikasi berbasis web, dengan kombinasi :

- [S3 untuk hosting](http://docs.aws.amazon.com/AmazonS3/latest/dev/WebsiteHosting.html)
- [AWS Api gateway sebagai REST API](http://docs.aws.amazon.com/apigateway/latest/developerguide/create-api-using-restapi.html)
- [AWS Lambda sebagai handler Api Gateway](http://docs.aws.amazon.com/lambda/latest/dg/with-on-demand-https-example.html)
- [AWS DynamoDB sebagai data layer](http://docs.aws.amazon.com/lambda/latest/dg/with-ddb.html)
- [AWS Route 53 untuk manajemen DNS](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/Welcome.html)

Bisnis Anda sudah bisa dimulai, **Anda bisa fokus pada produk dan pengguna, bukan infrastruktur**.

>>> Mahmoud Matouk memberikan tutorial gratis di Udemy dengan judul "**[Serverless Architecture on AWS](https://www.udemy.com/serverless-architecture-on-aws/)**" yang membahas 4 stack tersebut.

### Startup yang kekurangan / tidak ada tim Devops

[Devops](https://en.wikipedia.org/wiki/DevOps) secara mudah bisa Kita artikan seseorang yang bertanggung jawab atas berjalannya sebuah produk digital. Jika produk yang ditawarkan adalah aplikasi berbasis web, minimal akan berurusan dengan :

- **Web Server** seperti Nginx, Apache Web Server, Lighttpd
- **Web Framework** seperti Laravel, Django, Ruby on Rails, Sails / Meteor
- **Platform Application** seperti PHP-FPM, gunicorn, PM2
- **RDBMS** seperti MySQL, PostgreSQL
- **NoSQL** seperti Redis, MongoDB, Elasticsearch, Cassandra
- Permintaan server atau instance seperti pada provider AWS, GCP, Azure

Lebih dalam pada peran pentingnya tim Devops adalah **mereka harus memastikan produk yang dikembangkan tidak ada masalah**, khususnya saat terjadi traffic yang tinggi, jika terjadi service down seperti "I/O server aplikasi tinggi" sehingga tidak bisa diakses, sudah pasti tim Devops yang akan berada di garis depan. Lalu ketika weekend, dan terjadi "Server Database Down", sudah pasti tim Devops yang menangani.

Arsitektur serverless akan memudahkan tim Devops. Dengan tidak perlunya memikirkan Web Server yang tidak pernah down (AWS Api Gateway + AWS Lambda sebagai layer Web Server), tim Devops bisa **fokus pada pekerjaan lain**.

Kita ambil contoh produk NoSQL [Aerospike](http://www.aerospike.com/). Produk ini tidak tersedia sebagai layanan "Managed" di AWS, dan kita sendiri yang harus melakukan manajemen. Tim Devops bisa fokus pada proses Scaling Up & Scaling Horizontal dengan menambahkan node yang akan membuat aerospike melakukan "[Automatic Rebalance](http://www.aerospike.com/docs/architecture/data-distribution.html)".

Kita ambil contoh lain, yaitu Duolingo menggunakan DynamoDB dan menyimpan [31 Miliar item](https://www.youtube.com/watch?v=fhnAvn2YxZA), Duolingo hanya membutuhkan 2 orang tim Devops untuk menghandle [110 Juta Pengguna](https://www.techinasia.com/how-duolingo-got-110-million-users) (2 orang Devops disebutkan dalam video).

### Perusahaan yang memiliki server fisik

Banyak perusahaan IT yang memulai bisnis dengan memiliki server, baik itu di data center maupun membuat ruang server khusus di perusahaan mereka. Ada beberapa hal yang perlu diperhatikan jika memiliki server fisik, diantaranya :

- Ketersediaan Part seperti HDD, Processor, Ram, dan Power Supply
- Akses Internet inbound / outbound
- Suhu Ruangan
- Kestabilan Listrik
- Tim Server yang selalu standby di data center
- Biaya yang tidak murah

Perusahaan banyak beranggapan dengan memiliki / mengelola server sendiri, bisnis akan tetap berjalan. Betul, cara ini dilakukan oleh Stackoverflow, [Arsitektur](https://nickcraver.com/blog/2016/02/17/stack-overflow-the-architecture-2016-edition/) dan [Hardware](https://nickcraver.com/blog/2016/03/29/stack-overflow-the-hardware-2016-edition/).

Anda bisa mengikuti langkah yang diambil stackoverflow jika :

- Memiliki Tim Devops yang sangat berpengalaman
- Sudah **menguasai 100% produk** yang sedang dibuat
- Sudah mengerti ketika harus melakukan scaling
- Sudah mengerti ketika terjadi masalah pada server
- Sudah melakukan tuning server sampai maksimal

### Lalu, mengapa masih menawarkan arsitektur serverless?

##### Processor dari tahun ke tahun semakin baik dan semakin murah

![ processor-by-year.png ](/images/arsitektur-serverless-siapa-yang-harus-beralih/processor-by-year.png "Processor dari 2006 hingga 2013")

Dengan melihat tabel diatas yang bersumber dari [techspot](http://www.techspot.com/article/1039-ten-years-intel-cpu-compared/), processor dari tahun ke tahun itu semakin baik dan semakin murah. Dengan memiliki $316 pada tahun 2006 kita bisa memiliki high end processor. Namun dengan harga yang tidak berbeda jauh, dengan memiliki $339 pada tahun 2013 kita bisa memiliki high end processor terbaik di tahun tersebut.

Kita bandingkan dengan processor Server, antara [Intel Xeon E5-2690 Generasi Pertama dengan Generasi Keempat](https://ark.intel.com/compare/91770,64596). Hasil benchmark menunjukkan, [generasi pertama](https://ark.intel.com/products/64596/Intel-Xeon-Processor-E5-2690-20M-Cache-2_90-GHz-8_00-GTs-Intel-QPI) mendapatkan score **503|681**, dan [generasi keempat](https://ark.intel.com/products/91770/Intel-Xeon-Processor-E5-2690-v4-35M-Cache-2_60-GHz) mendapatkan score **943|1300**.

##### Effort yang tidak sedikit jika ingin melakukan upgrade server

Merujuk pada point nomor 1, dengan melihat processor yang semakin murah tiap tahun, pastinya perusahaan juga ingin melakukan upgrade pada server yang mereka miliki. Dengan biaya yang semakin murah, akan didapatkan "compute power" yang lebih baik. Namun proses upgrade server itu tidak mudah, ada beberapa hal yang harus anda pertimbangkan, diantaranya :

- Anda harus memikirkan tentang socket processor, beruntung jika socket masih sama, jika socketnya berbeda?
- Processor lama yang Anda miliki, mau dipakai untuk apa?
- Jika Processor lama yang Anda miliki ingin dijual saja, berapa banyak jatuhnya?
- Jika Socket processor cocok, apakah dengan motherboard yang lama, sistem bisa berjalan dengan maksimal?
- Jika Socket processor tidak cocok, berikut juga komponen lainnya tidak cocok, Anda lebih baik **membeli Server baru**
- Server lama yang Anda miliki, mau dipakai untuk apa?
- Jika Server lama yang Anda miliki ingin dijual saja, berapa banyak jatuhnya?
- Jika server lama yang Anda miliki tetap ingin digunakan, Anda harus **membayar biaya maintenance ke Data Center**

##### Tidak bisa melakukan proses Autoscaling

Saya rasa point ini cukup jelas. Kalaupun ada sebuah kasus, ambil contoh ecommerce yang melakukan flash sale, effort untuk melewati event ini sangat besar sekali. Sudah adakah provider di Indonesia yang menyediakan sewa server fisik per jam?

>>> Anda tidak perlu memikirkan hal-hal diatas dengan arsitektur serverless.

### Kesimpulan

>>> Arsitektur Serverless akan mempermudah hidup Kita dan membuat Kita lebih efisien terhadap waktu dengan tidak perlu memikirkan tentang infrastruktur atau server.

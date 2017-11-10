+++
author = "ridwanbejo"
comments = true
date = "2017-11-10T03:00:00+07:00"
draft = false
image = ""
menu = ""
share = true
slug = "contoh-skema-aplikasi-serverless-2-laporan-warga"
tags = ["azure", "serverless","aws", "nosql"]
title = "Contoh Skema Aplikasi Serverless #2 - Laporan Warga"

+++

#### Pendahuluan

Laporan warga adalah sebuah aplikasi yang dapat membantu warga perkotaan atau pedesaan untuk melaporkan berbagai keluhan seputar infrastruktur yang ada di daerahnya. Seperti jalan rusak, lampu lalu lintas mati, solokan belum dikeruk, dan permasalahan infrastruktur lainnya.

Warga cukup memotret infrastruktur yang rusak dan melaporkannya melalui aplikasi yang bernama "Citizen Report". Nantinya warga bisa memotret foto kerusakan infrastruktur dan memberikan catatan serta memilih kategori infrastruktur apa.

Setelah sampai di *server*, pemerintah setempat dapat melihat berbagai laporan yang masuk melalui *dashboard* yang dibangun diatas Elasticsearch dan Kibana. Laporan yang masuk akan ditampilkan dalam berbagai grafik dan visualisasi lainnya agar mempermudah pemerintah setempat untuk mengambil keputusan dalam menentukan prioritas infrastruktur mana yang harus diperbaiki dahulu. Dan bila keluhan sudah ditangani, maka pemerintah setempat akan memberikan notifikasi langsung kepada pelapor.

Saat ini aplikasi "Citizen Report" tersebut belum dilengkapi sistem *machine learning* yang dapat menentukan prediksi kerusakan terbesar di masa yang akan datang dengan melihat jumlah laporan dan ketersediaan anggaran.

Lalu bagaimanakah bila kita ingin mengimplementasikannya diatas arsitektur *serverless*?

#### Contoh arsitektur diatas Amazon Web Service

Bila kita ingin membangunnya diatas Amazon Web Service, beberapa layanan yang diperlukan antara lain adalah sebagai berikut:

* S3
* API Gateway
* Lambda
* DynamoDB
* Cloudwatch
* Simple Queue Service
* Simple Notification Service
* Elasticsearch on AWS

S3 dapat digunakan untuk menyimpan *static file* seperti *file* Javascript, CSS, dan *template* yang dibangun dengan menggunakan *library* Javascript. Misalnya *clientside* dari aplikasi kita dibangun dengan menggunakan Angular.js, React.js, atau Vue.js.

Karena aplikasi tersebut membutuhkan *service* yang diambil melalaui AJAX. Maka kita harus menyimpannya diatas Lambda. Dengan menggunakan Lambda, kamu dapat membuat beberapa *service* dengan bahasa pemrograman seperti Node.js, Python, dan Java. Dalam implementasinya pun, usahakan 1 CRUD diimplmentasikan ke dalam 1 Lambda. Jangan sampai 1 Lambda memiliki terlalu banyak *service*.

Kita mulai dari bagian *backend* dahulu. Kita akan membuat tiga buah Lambda untuk menangani data *user*, *report category*, dan *report*. Ketiganya menggunakan DynamoDB untuk menyimpan data. Kemudian terhubung juga ke API Gateway yang nantinya akan digunakan oleh aplikasi *mobile* dalam menerima dan mengirim *request*.

Bila ada laporan yang masuk, data tekstual akan disimpan ke DynamoDB, sedangkan data berupa gambar atau video akan disimpan ke S3 dengan melalui perantara SQS, sehingga *file* yang dikirim akan diproses dilain waktu tanpa harus menunggu semua *file* diproses saat itu juga. Begitu *file* masuk ke S3, maka Lambda yang bertugas melakukan *image processing* akan berjalan dan menyimpan kembali hasil pemrosesannya ke S3. Lambda tersebut diberikan *event trigger* ketika S3 menerima *file*.

Lanjut ke bagian Admin Panel, diasumsikan kita membuat admin panel ini dengan bantuan *clientside* Javascript seperti Angular.js, React.js, atau Vue.js. Dengan *web template* berbasis Twitter Bootstrap. Semua *static file* tersebut disimpan ke S3 dan *bucket*-nya diekspos ke publik dengan menggunakan *amazon resource name* yang dihasilkan.

Kemudian Admin Panel tersebut menggunakan ketiga *service* yang telah dibangun dengan Lamdba. Dan bila ada laporan yang masuk maka proses pemberitahuan kepada pelapor akan dikirimkan lewat Simple Notification Service baik itu SMS maupun *push notification* yang dibantu dengan Lambda. Bila *user* berhasil terverifikasi pun akan ada notifikasinya melalui Simple Notification Service.

Karena ada juga pihak pemerintah yang ingin melihat perkembangan masalah infrastruktur di daerahnya. AWS Cloudwatch bertugas untuk menjalankan Lambda yang akan digunakan melakukan ETL dari DynamoDB ke AWS Elasticsearch. AWS Elasticsearch ini sudah lengkap dimana kita dapat menggunakan Elasticsearch, Logstash, dan Kibana tanpa instalasi (*zero installation*).

Secara periodik dengan rentang per jam, Cloudwatch akan menjalan Lambda dan mengekstrak data - data dari DynamoDB ke AWS Elasticsearch. Dan jajaran pemerintah tingkat atas yang terkait dapat melihat infografiknya melalui Kibana yang sudah memuat berbagai laporan warga dan *insight* yang telah dibuat oleh tim *Business Intelligence*.

![ img-1.png ](/images/contoh-skema-aplikasi-serverless-2-laporan-warga/img-1.png "serverless architecture example on aws") 

#### Contoh arsitektur diatas Azure

Hampir mirip dengan versi AWS, hanya ada beberapa perbedaan dalam layanan Azure yang dipilih. Di Azure kita dapat menggunakan:

* Azure App Service, untuk meng-*hosting* aplikasi *web* seperti aplikasi berbasis *client-side* Javascript yang dibangun menggunakan Angular.js, React.js atau Vue.js
* Azure Function, untuk membuat *service* yang dibangun diatas FaaS di Azure.
* Azure Blob Storage, untuk menyimpan gambar hasil laporan warga
* Azure CosmosDB, untuk menyimpan skema *database* yang digunakan untuk menampung data dari hasil laporan warga
* Azure Blob Storage Queue, merupakan sistem antrian yang dapat mengatur jumlah *file* yang masuk ke Azure Blob Storage
* Azure Notification Hub, layanan Azure yang dapat memberikan notifikasi ke sebuah *mobile device* mulai dari *push notification*, SMS, dan *email*.
* Web Scheduler, layanan Azure yang dapat mengatur penjadwalan untuk *script* yang akan kita jadwalkan.

![ img-2.png ](/images/contoh-skema-aplikasi-serverless-2-laporan-warga/img-2.png "serverless architecture example on azure") 

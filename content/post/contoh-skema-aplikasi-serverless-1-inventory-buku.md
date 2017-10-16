+++
author = "ridwanbejo"
comments = true
date = "2017-10-16T02:15:00+07:00"
draft = false
image = ""
menu = ""
share = true
slug = "contoh-skema-aplikasi-serverless-1-inventory-buku"
tags = ["azure", "serverless","aws", "nosql]
title = "Contoh Skema Aplikasi Serverless #1 - Inventory Buku"

+++

####Pendahuluan

Inventori Buku, ceritanya, adalah sebuah aplikasi yang digunakan untuk mengelola buku yang ada di suatu gudang. Kita dapat mencatat stok buku dan berbagai macam judul buku yang masuk dan keluar di gudang milik kita. Sederhananya, ada beberapa orang admin yang dapat mengelola sirkulasi buku yang ada di gudang.

Kemudian kita pun dapat mencatat kategori buku yang akan disimpan di lemari. Pertama kita pisahkan *layer* *frontend* dan *backend*. Dimana *layer* *frontend* dapat dibangun dengan menggunakan *tools* seperti Angular.js, React.js, ataupun Vue.js. 

Ingat disini kita akan membuat sebuah panel berbasis *web*. Kemudian kita juga membutuhkan *storage* untuk menyimpan *cover* dari buku yang akan disimpan. Tak lupa kita juga memerlukan *database* yang akan menyimpan informasi dari buku yang akan disimpan mulai dari judul, pengarang, penerbit, tebal halaman, ukuran buku, sampai stok yang tersedia.

Pengelola buku pun dapat dibuat oleh akun **superadmin** dengan menyesuaikan pada karyawan yang dibutuhkan untuk mengelola buku di gudang yang kita miliki. Anggap saja gudang yang dimiliki meliputi lima gudang yang berbeda di Kota Bandung.

Lalu bagaimanakah bila kita ingin mengimplementasikannya diatas arsitektur *serverless*?

####Contoh arsitektur diatas Amazon Web Service

Bila kita ingin membangunnya diatas Amazon Web Service, beberapa layanan yang diperlukan antara lain adalah sebagai berikut:

* S3
* API Gateway
* Lambda
* DynamoDB

S3 dapat digunakan untuk menyimpan *static file* seperti *file* Javascript, CSS, dan *template* yang dibangun dengan menggunakan *library* Javascript. Misalnya *clientside* dari aplikasi kita dibangun dengan menggunakan Angular.js, React.js, atau Vue.js.

Karena aplikasi tersebut membutuhkan *service* yang diambil melalaui AJAX. Maka kita harus menyimpannya diatas Lambda. Dengan menggunakan Lambda, kamu dapat membuat beberapa *service* dengan bahasa pemrograman seperti Node.js, Python, dan Java. Dalam implementasinya pun, usahakan 1 CRUD diimplmentasikan ke dalam 1 Lambda. Jangan sampai 1 Lambda memiliki terlalu banyak *service*.

Katakanlah kita ingin membuat *service* untuk *user management*, mengelola kategori buku, dan mengelola buku itu sendiri. Kita buat kodenya dalam bahasa pemrograman yang diperlukan, pastikan kodenya siap di-*deploy* setelah melalui serangkaian pengujian dan *deploy*-lah kode kamu dengan menggunakan *tools* seperti Zappa atau Serverless Framework.

Untuk *data store*-nya, kita gunakan DynamoDB, karena dengan DynamoDB kamu cukup membuat tabel saja tanpa harus membangun infrastruktur *database* sendiri. Dan untuk menyimpan gambar dari *cover* buku, gunakan juga S3 untuk menyimpan gambar - gambar tersebut yang di-*upload* dengan ditangani oleh AWS Lambda.

Namun AWS Lambda tidak dapat digunakan langsung oleh aplikasi *web* kita yang dibangun diatas Angular.js, kamu harus mentranslasikannya URL ke *service* dengan menggunakan API Gateway. Layanan ini merupakan *web server* yang sangat mudah digunakan sekaligus tidak ribet dikonfigurasi, kamu hanya perlu menentukan URL induk apa yang akan ditangani, dan pilihlah Lambda mana yang akan menangani.

![ img-1.png ](/images/contoh-skema-aplikasi-serverless-1-inventory-buku/img-1.png "serverless architecture example on aws") 

####Contoh arsitektur diatas Azure

Hampir mirip dengan versi AWS, hanya ada beberapa perbedaan dalam layanan Azure yang dipilih. Di Azure kita dapat menggunakan:

* Azure Apps, untuk *hosting* aplikasi *web* kita yang ditulis menggunakan Angular.js, React.js, atau Vue.js beserta *static file*-nya
* Azure Function, untuk membuat *service* yang dibangun diatas FaaS di Azure.
* Azure Blob Storage, untuk menyimpan *cover* buku dan *file* lainnya
* Azure CosmosDB, untuk menyimpan segala data mulai dari data kategori buku, stok buku, data buku, sampai data user

![ img-2.png ](/images/contoh-skema-aplikasi-serverless-1-inventory-buku/img-2.png "serverless architecture example on azure") 
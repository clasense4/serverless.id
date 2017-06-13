+++
title = "Arsitektur Serverless? Kenapa harus beralih?"
author = "Fajri Abdillah"
share = true
tags = ["serverless"]
draft = false
menu = ""
image = "images/default.jpg"
slug = "arsitektur-serverless-kenapa-harus-beralih"
date = "2017-06-13T02:24:24+07:00"
comments = true
+++

>>> Serverless? Tidak ada server? Mana mungkin.

![ impossibru.jpg ](/images/arsitektur-serverless-kenapa-harus-beralih/impossibru.jpg "IMPOSSIBRU")

<!--more-->

Betul, istilah ini memang sangat awam bagi para Developer. Lalu apa sebetulnya serverless itu sendiri? Sudah sangat banyak yang membahas mengenai serverless ini, beberapa diantaranya :

- [Serverless Architectures](https://martinfowler.com/articles/serverless.html) *(Paling jelas, disertai dengan beberapa perbandingan)*
- [What *is* Serverless Architecture?](https://medium.com/@PaulDJohnston/what-is-serverless-architecture-43b9ea4babca)
- [Answering All Your Questions on Serverless Javascript](https://medium.com/the-node-js-collection/serverless-javascript-5d2528ac46b5)
- [What’s This Serverless Thing Anyway?](https://read.acloud.guru/whats-this-serverless-thing-anyway-b101cb72c7e6)

### Beri saya alasan untuk beralih

Umumnya untuk membuat sebuah sistem, mayoritas menggunakan pola seperti ini :

1. **Web Server + Aplikasi Server dan Database Server dalam satu server**.

    Ini langkah yang sederhana, dan efisien terhadap biaya. Kita bisa memulai dari satu server untuk melihat traffic yang terjadi didalam sistem yang dibangun, selama semua muat dalam satu server, kenapa tidak?

    "Provision Tools" seperti [Ansible](https://www.ansible.com/how-ansible-works), [Chef](https://www.chef.io/automate/) dan [Puppet](https://puppet.com/product/capabilities/automated-provisioning) dapat menangani deployment seperti ini. Cukup ketik satu baris perintah di command line kita, tunggu, dan sistem siap digunakan. Limitasi pada sistem seperti ini adalah ketika traffic meningkat, imbasnya yaitu pada CPU, Memory dan Storage yang sudah terkunci pada server kita.

    Jika server yang digunakan adalah server fisik, limitasinya pada jumlah slot CPU, slot Memory, dan slot Storage. Jika server yang digunakan berbasis cloud, cukup dengan sekian klik, server kita semakin kuat untuk menerima traffic. Harus diingat, deployment seperti ini pasti ada downtime ketika melakukan upgrade. Lalu muncul pertanyaan

    >>> Kalau trafficnya cuma rame waktu weekend, gimana ya?

    ![ cpu_utilization.png ](/images/arsitektur-serverless-kenapa-harus-beralih/cpu_utilization.png "CPU Utilization di salah satu startup")

2. **Web Server + Aplikasi Server dan Database Server dalam server yang berbeda dan banyak**.

    Ini langkah yang sangat baik. Ketika traffic meningkat, dan yang membutuhkan penanganan lebih lanjut hanya pada sisi Web Server, Web Server bisa kita upgrade atau tambah node, begitu juga jika server Database membutuhkan penanganan, bisa dilakukan scaling dengan menambahkan node untuk replikasi / sharding.

    Deployment jenis ini juga bisa ditangani oleh "Provision Tools" sama seperti diatas. Cukup ketik satu baris perintah di command line kita, tungggu, dan sistem siap digunakan. Atau jika menggunakan service cloud seperti **[AWS Elastic Beanstalk](https://aws.amazon.com/elasticbeanstalk/)** atau **[AWS Opswork](https://aws.amazon.com/opsworks/)**, kita sudah sangat dimudahkan.

    Apakah dengan deployment seperti ini bisa menjawab pertanyaan diatas? Saya pikir ini bisa. Lalu ketika tim melihat halaman monitoring, tampak jelas grafik yang sangat menanjak, dan seketika turun dengan curam. Dan di bagian report **http request 500**, naik sangat tajam. Lalu muncul lagi pertanyaan

    >>> Berapa banyak pengunjung yang dibuat kecewa dengan error 500 ini?

    "Kita tambah 1 instance, ketika rata - rata CPU sudah **mencapai 85% selama 5 menit**. Dan kurangi 1 instance ketika rata - rata CPU **sudah 25% selama 5 menit**". Betul, cara ini bisa melakukan antisipasi awal ketika traffic sudah mulai tinggi. Lalu muncul lagi pertanyaan

    >>> 85%? Berarti ada 15% yang kurang dimanfaatkan? Kenapa ngga nunggu 100%?

    "Kalau nunggu 100%, takutnya telat, provisioning itu butuh waktu Pak, jadi kita ambil antisipasi di angka 85%, atau kurang dari angka tersebut kalau ingin aman. Kecuali Bapak tidak mempermasalahkan dengan melihat health status mencapai **warning** atau **severe**". Dan inilah bentuk ketidak-pastian dalam industri yang kita jalani. Harus siap ketika traffic tinggi, dan tidak boleh mahal ketika traffic sedang rendah.

    ![ env_by_health.png ](/images/arsitektur-serverless-kenapa-harus-beralih/env_by_health.png "")

    >>> Harga EC2 dengan tipe **[m4.large](https://aws.amazon.com/ec2/pricing/on-demand/)** per jam di region tokyo / **ap-northeast-1** yaitu **$0.129**. Dengan asumsi seperti diatas berarti ada 15% ($0.01935) yang percuma, dikalikan berapa jam pemakaian dan dikalikan berapa instance, apabila menggunakan instance yang lebih tinggi, berapa biaya yang terbuang?

### Selamat Datang di Dunia Serverless

Dengan merujuk pertanyaan sebelumnya, maka pertanyaan nomor 1 sudah otomatis diselesaikan oleh serverless. Dengan otomatis serverless akan melakukan scaling sejumlah traffic. Berita baiknya, jika menggunakan framework zappa, Kita bisa memanfaatkan fungsi **[async](https://github.com/Miserlou/Zappa#asynchronous-task-execution)**. Mengenai async & zappa akan dibahas dalam post lainnya.

Lalu mengenai metode pembayaran untuk arsitektur serverless khususnya [aws lambda](https://aws.amazon.com/lambda/pricing/), yaitu ketika fungsi dijalankan, kita bayar. Kita tidak membayar fungsi yang tidak dijalankan. Jadi kita bisa lebih efisien dalam sisi biaya, dan tidak dipusingkan mengenai manajemen server. Dan ini otomatis menjawab pertanyaan nomor 2.

Service lainnya seperti [auth0](https://auth0.com/) yang memberikan fitur identitas tanpa harus memanage server. Login menggunakan akun social dipermudah dengan service ini, dan bisa juga dikombinasikan dengan aws lambda, [google firebase](https://firebase.google.com/), dll.

Jika kita ingin membuat aplikasi streaming, kita bisa memanfaatkan [aws kinesis firehose](https://aws.amazon.com/kinesis/firehose/) untuk mengirim data ke [S3](https://aws.amazon.com/s3/), atau [aws kinesis stream](https://aws.amazon.com/kinesis/streams/) untuk mengirim data ke RDBMS seperti [AWS RDS](https://aws.amazon.com/rds/) / [Aurora](https://aws.amazon.com/rds/aurora/) dan NoSQL seperti [AWS DynamoDB](https://aws.amazon.com/dynamodb/), [Redis](https://aws.amazon.com/elasticache/).

### Kesimpulan

>>> Serverless adalah tentang tidak diperlukannya manage server, semua tentang pemanfaatan service

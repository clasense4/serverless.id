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

Betul, teknologi serverless, dibelakangnya memang masih ada server, tapi hanya memiliki waktu sekian detik / mili detik, istilah ini memang sangat awam bagi para Developer.

Lalu apa sebetulnya serverless itu sendiri? Sudah sangat banyak yang membahas mengenai serverless ini, beberapa diantaranya :

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

    Apakah dengan deployment seperti ini bisa menjawab pertanyaan diatas? Saya pikir ini bisa. Lalu mengapa masih menawarkan serverless?

    Kita tengok sebuah cerita di suatu tim. Pada suatu waktu tim melihat halaman monitoring, tampak jelas grafik yang sangat menanjak, dan seketika turun dengan curam. Dan di bagian report **http request 500**, naik sangat tajam. Lalu muncul pertanyaan

    >>> Server Aplikasi kita ngga kuat, berapa banyak pengunjung yang dibuat kecewa dengan error ini?

    Lalu dilakukan meeting dan muncullah sebuah formula, "Kita tambah 1 instance, ketika rata - rata CPU sudah **mencapai 85% selama 5 menit**. Dan kurangi 1 instance ketika rata - rata CPU **sudah 25% selama 5 menit**". Dengan cara ini, kita bisa melakukan antisipasi awal ketika traffic sudah mulai tinggi. Lalu muncul lagi pertanyaan

    >>> Berapa waktu yang dibutuhkan untuk menambah instance baru?

    ![ autoscaling_aws.png ](/images/arsitektur-serverless-kenapa-harus-beralih/autoscaling_aws.png "")

### Selamat Datang di Dunia Serverless

Dengan merujuk pertanyaan sebelumnya, maka pertanyaan pada point nomor 1 sudah diselesaikan oleh serverless. Dengan otomatis serverless akan melakukan scaling sejumlah traffic. Berita baiknya, jika menggunakan framework zappa, Kita bisa memanfaatkan fungsi **[async](https://github.com/Miserlou/Zappa#asynchronous-task-execution)**. Mengenai async & zappa akan dibahas dalam post yang berbeda.

Lalu mengenai perbandingan antara arsitektur serverless dan arsitektur berbasis server seperti elasticbeanstalk, perbedaan yang sangat jelas yaitu saat proses [autoscaling](http://docs.aws.amazon.com/autoscaling/latest/userguide/GettingStartedTutorial.html) terjadi. Provisioning instance baru, itu **[dibutuhkan proses](https://stackoverflow.com/questions/14115502/elastic-beanstalk-auto-scaling-how-long-to-bring-up-a-new-instance)**, seperti install dependency (contoh : Nginx + PHP-FPM), register ke Elastic Load Balancer, Health Check, sehingga instance bisa menerima traffic.

Pada arsitektur serverless, tidak ada lagi proses install dependency dan lainnya seperti pada elastic beanstalk. Karena kode kita sudah dibungkus menjadi sebuah fungsi, proses menambah instance dalam arsitektur serverless tersebut berjalan sangat cepat dan otomatis.

Dalam dunia serverless, Kita bisa fokus pada bisnis dan kepuasan user. Tidak perlu banyak effort dalam scaling, semua sudah di handle oleh provider.

Dalam dunia serverless, Kita berbicara mengenai pemanfaatan service. Service seperti [auth0](https://auth0.com/) yang memberikan fitur identitas tanpa harus memanage server. Login menggunakan akun social dipermudah dengan service ini.

Jika kita ingin membuat aplikasi data streaming, kita bisa memanfaatkan service seperti [aws kinesis firehose](https://aws.amazon.com/kinesis/firehose/) untuk mengirim data ke [S3](https://aws.amazon.com/s3/), atau [aws kinesis stream](https://aws.amazon.com/kinesis/streams/) untuk mengirim data ke RDBMS seperti [AWS RDS](https://aws.amazon.com/rds/) / [Aurora](https://aws.amazon.com/rds/aurora/) dan NoSQL seperti [AWS DynamoDB](https://aws.amazon.com/dynamodb/), [Redis](https://aws.amazon.com/elasticache/). Mengenai teknologi streaming akan dibahas dalam post yang berbeda.

### Kesimpulan

>>> Serverless adalah tentang tidak diperlukannya manage server, semua tentang pemanfaatan service, Kita tidak lagi dipusingkan oleh limitasi server, sehingga proses bisnis berjalan dengan baik berapapun traffic yang datang.

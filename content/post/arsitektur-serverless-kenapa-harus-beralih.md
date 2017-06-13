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

Betul, istilah ini memang sangat awam bagi para Developer. Umumnya untuk membuat sebuah sistem, mayoritas menggunakan pola seperti ini :

1. **Web Server + Aplikasi Server dan Database Server dalam satu server**.

    Ini langkah yang sederhana, dan efisien terhadap biaya. Kita bisa memulai dari satu server untuk melihat traffic yang terjadi didalam sistem yang dibangun, selama semua muat dalam satu server, kenapa tidak?

    "Provision Tools" seperti Ansible, Chef dan Puppet dapat menangani deployment seperti ini. Cukup ketik satu baris perintah di command line kita, tunggu, dan sistem siap digunakan. Limitasi pada sistem seperti ini adalah ketika traffic meningkat, imbasnya yaitu pada CPU, Memory dan Storage yang sudah terkunci pada server kita.

    Jika server yang digunakan adalah server fisik, limitasinya pada jumlah slot CPU, slot Memory, dan slot Storage. Jika server yang digunakan berbasis cloud, cukup dengan sekian klik, server kita semakin kuat untuk menerima traffic. Harus diingat, deployment seperti ini pasti ada downtime ketika melakukan upgrade. Lalu muncul pertanyaan

    >>> Kalau trafficnya cuma rame waktu weekend, gimana ya?

    ![ cpu_utilization.png ](/images/arsitektur-serverless-kenapa-harus-beralih/cpu_utilization.png "CPU Utilization di salah satu startup")

2. **Web Server + Aplikasi Server dan Database Server dalam server yang berbeda dan banyak**.

    Ini langkah yang sangat baik. Ketika traffic meningkat, dan yang membutuhkan penanganan lebih lanjut hanya pada sisi Web Server, Web Server bisa kita upgrade, begitu juga jika server Database membutuhkan penanganan, bisa dilakukan scaling atau menambahkan node untuk replikasi / sharding.

    Deployment jenis ini juga bisa ditangani oleh "Provision Tools" sama seperti diatas. Cukup ketik satu baris perintah di command line kita, tungggu, dan sistem siap digunakan. Atau jika menggunakan service cloud seperti **AWS Elastic Beanstalk** atau **AWS Opswork**, kita sudah sangat dimudahkan.

    Apakah dengan deployment seperti ini bisa menjawab pertanyaan diatas? Saya pikir ini bisa. Lalu ketika tim melihat halaman monitoring, tampak jelas grafik yang sangat menanjak, dan seketika turun dengan curam. Dan di bagian report **http request 500**, naik sangat tajam. Lalu muncul lagi pertanyaan

    >>> Berapa banyak pengunjung yang dibuat kecewa dengan error 500 ini?

    "Kita tambah 1 instance, ketika rata - rata CPU sudah **mencapai 85%**. Dan kurangi 1 instance ketika rata - rata CPU **sudah 25%**". Betul, cara ini bisa melakukan antisipasi awal ketika traffic sudah mulai tinggi. Lalu muncul lagi pertanyaan

    >>> 85%? Berarti ada 15% yang kurang dimanfaatkan? Kenapa ngga nunggu 100%?

    "Kalau nunggu 100%, takutnya telat, provisioning itu butuh waktu Pak, jadi kita ambil antisipasi di angka 85%, atau kurang dari angka tersebut kalau ingin aman. Kecuali Bapak tidak mempermasalahkan dengan melihat health status mencapai **warning** atau **severe**". Dan inilah bentuk ketidak-pastian dalam industri yang kita jalani. Harus siap ketika traffic tinggi, dan tidak boleh mahal ketika traffic sedang rendah.

    ![ env_by_health.png ](/images/arsitektur-serverless-kenapa-harus-beralih/env_by_health.png "")

    >>> Harga EC2 dengan tipe **m4.large** per jam di region tokyo / **ap-northeast-1** yaitu **$0.129**. Dengan asumsi seperti berarti ada 15% ($0.01935) yang percuma, dikalikan berapa jam pemakaian dan dikalikan berapa instance, apabila menggunakan instance yang lebih tinggi, berapa biaya yang terbuang?

### Selamat Datang di Dunia Serverless

Dengan merujuk pertanyaan sebelumnya, maka pertanyaan nomor 1 sudah otomatis diselesaikan oleh serverless. Dengan otomatis serverless akan melakukan scaling sejumlah traffic. Berita baiknya, jika menggunakan framework zappa, Kita bisa memanfaatkan fungsi **async**. Mengenai async & zappa akan dibahas dalam post lainnya.

Lalu mengenai metode pembayaran untuk arsitektur serverless khususnya aws lambda, yaitu ketika fungsi dijalankan, kita bayar. Kita tidak membayar fungsi yang tidak dijalankan. Jadi kita bisa lebih efisien dalam sisi biaya, dan tidak dipusingkan mengenai manajemen server.

Service lainnya seperti auth0 yang memberikan fitur identitas tanpa harus memanage server. Login menggunakan akun social dipermudah dengan service ini, dan bisa juga dikombinasikan dengan aws lambda, google firebase, dll.

Jika kita ingin membuat aplikasi streaming, kita bisa memanfaatkan aws kinesis firehose untuk mengirim data ke S3, atau aws kinesis stream untuk mengirim data ke RDBMS seperti AWS RDS / Aurora dan NoSQL seperti AWS DynamoDB, Redis.

### Kesimpulan

>>> Serverless adalah tentang tidak diperlukannya maintenance server, semua tentang pemanfaatan service

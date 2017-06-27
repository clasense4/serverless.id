+++
title = "Arsitektur Serverless? Siapa yang sudah sukses?"
author = "fajriabdillah"
share = true
tags = ["serverless"]
draft = false
menu = ""
image = "images/default.jpg"
slug = "arsitektur-serverless-siapa-yang-sudah-sukses"
date = "2017-06-27T20:15:00+07:00"
comments = true
+++

>>> Pastikan anda sudah memahami [kenapa harus beralih](/post/arsitektur-serverless-kenapa-harus-beralih/) dan [siapa yang harus beralih](/post/arsitektur-serverless-siapa-yang-harus-beralih).

<!--more-->

### Membangun Website Sensus Australia yang lebih baik dengan Arsitektur Serverless

Pada tanggal 9 Agustus tahun 2016, penduduk Australia melakukan sensus. 16 juta penduduk Australia — 65% dari total populasi, atau lebih dari 6 juta rumah tangga — diharapkan untuk menyelesaikan sensus penduduk dengan cara daring. Proyek ini menggunakan dana lebih dari **$9,000,000** dan menggunakan dana lebih dari **$400,000** untuk melakukan "Load Testing". Klaim dari pemerintah, server telah di load hingga 150% dari kapasitas, namun dari sekian banyak uang tersebut, website "crash", dan banyak orang komplain seperti diberitakan oleh [news.com.au](http://www.news.com.au/national/frustration-as-abs-census-website-unable-to-be-reached/news-story/298363b96a4feab132698075cec306b2) dan [lifehacker.com.au](https://www.lifehacker.com.au/2016/08/the-australian-census-website-is-down/).

Austin Wilshire dan Bernd Hartzer menerima perhatian dunia ketika mereka membuat sebuah website alternatif "Australian Bureau of Statistics" dengan biaya kurang dari **$500**. Mereka mengerjakan website ini dalam hackaton dan selesai **kurang dari 24 Jam**. Yang menarik, Austin Wilshire belum pernah menyentuh AWS sama sekali, apalagi teknologi serverless.

Lalu darimana mereka bisa mengklaim lebih baik dari website aslinya? Mereka melakukannya dengan opensource load testing tool [Goad](https://goad.io/). Goad menggunakan AWS Lambda untuk melakukan Load Testing, dan sanggup mencapai angka 100,000 request/detik.

Bahkan Werner Vogel, CTO Amazon men-tweet tentang kesuksesan 2 anak muda ini.

<center><blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">cool: QUT Students built an Australian Census system for $500 that does not <a href="https://twitter.com/hashtag/CensusFail?src=hash">#CensusFail</a> <a href="https://t.co/ieaxP4Ix1s">https://t.co/ieaxP4Ix1s</a> <a href="https://twitter.com/hashtag/AWS?src=hash">#AWS</a> <a href="https://t.co/gZiUzPKEvf">pic.twitter.com/gZiUzPKEvf</a></p>&mdash; Werner Vogels (@Werner) <a href="https://twitter.com/Werner/status/765599106387542016">August 16, 2016</a></blockquote></center>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

>>> Kunjungi artikel lengkapnya ["Building A Better Australian Census Website with Serverless Architecture"](https://serverless.com/blog/building-a-better-australian-census-site/)

### 30,000 "Pageview" dengan biaya $0.21 dan serverless

[Fantasy Movie League](https://fantasymovieleague.com/) adalah game fantasy untuk orang-orang yang tidak suka dengan olahraga. Perkiraan pengguna yang sudah registrasi pada saat artikel aslinya dibuat yaitu 24,000.

Aplikasi yang dibuat adalah ["Lineup Calculator"](http://analyzer.fmlnerd.com/lineups/). Dengan biaya yang murah, dan tidak perlu manage server, arsitektur serverless adalah cerita yang sangat menarik.

>>> Kunjungi artikel lengkapnya ["30K Page Views for $0.21: A Serverless Story"](https://fmlnerd.com/2016/08/16/30k-page-views-for-0-21-a-serverless-story/)

### Perjalanan OpsGenie menuju arsitektur serverless

[OpsGenie](https://www.opsgenie.com/) adalah sebuah start-up yang dimulai pada tahun 2011 dengan tiga orang senior full stak developers yang sangat berpengalaman dalam membangun aplikasi Java Enterprise, produk on-premise yang memiliki spesialisasi dalam integrasi, data enrichment dan manajemen dari generasi pertama aplikasi monitoring infrastruktur. Mereka melihat ada kesempatan, dan memutuskan menggunakan pengalaman mereka untuk membangun layanan internet untuk "Alert/Incident Management".

OpsGenie mulai memindahkan banyak service mereka dari Java ke serverless, dan membuat artikel berseri mengenai perjalanan mereka dari **[Aplikasi Monolitik Java ke Arsitektur Serverless AWS](https://engineering.opsgenie.com/migrating-a-monolithic-java-application-to-aws-serverless-architecture-1180ca87b0b0)**.

>>> Kunjungi artikel lengkapnya ["OpsGenie is on a journey to reap the benefits of serverless architecture"](https://read.acloud.guru/opsgenie-journey-to-serverless-architecture-785540261ec3)

### Cloudsploit tidak lagi memanage EC2 Server

[CloudSploit](https://cloudsploit.com/) adalah "Security and Configuration Scanner" yang bisa mendeteksi ratusan ancaman dalam akun AWS.

Menariknya, Cloudsploit **belum menggunakan framework**, karena mereka ingin aplikasi web yang bisa di deploy dimanapun, bahkan jika di masa depan mereka harus meninggalkan AWS API Gateway dan AWS Lambda. Maka mereka pun **membuat sebuah nodejs framework sendiri**. Alasan lainnya adalah pada saat mereka memulai proses menuju arsitektur serverless, belum ada framework yang stable, serverless framework saat itu belum memasuki versi 1.0.

Lalu ke bagian yang lebih penting, yaitu Billing. Sebelumnya mereka full menggunakan server EC2, baik digunakan atau tidak, **mereka membayar untuk 24 Jam / 7 Hari Seminggu** dan saat ini mereka membayar ketika service mereka digunakan. Mereka percaya arsitektur serverless ini sangat membantu khususnya pada proses scaling yang **"tidak terbatas"**. Dan siapa yang merasa nyaman ketika pemberitahuan **"the server is out of disk space"** pada pukul 3AM tidak lagi muncul?

>>> Kunjungi artikel lengkapnya [We Made the Whole Company “Serverless”](https://blog.cloudsploit.com/we-made-the-whole-company-serverless-5a91c27cd8c4)

### Postflight mengurangi biaya hosting hingga $10,000 per bulan

Adam Pash adalah Lead Engineer di Postflight, dan mendapatkan tugas khusus, yaitu "Menulis ulang Readability Parser API". Readability API versi gratis membuat perusahaan harus membayar sekitar **$10,000** tiap bulan. Javascript adalah pilihan bahasa pemrograman yang akan digunakan, karena banyak Engineer di Postflight yang pernah memiliki pengalaman web.

Pilihan mereka adalah menggunakan [Serverless Framework](http://serverless.com/). Pada bulan Oktober kemarin, Postflight merilis "Mercury Web Parser", dan hasilnya mencengangkan. **Biaya operasional mereka seketika turun**, dan hari ini, Mercury Web Parser membutuhkan biaya sekitar **$400** untuk beroperasi. Dengan detail biaya :

#### API Gateway:
- Biaya Request: $137 ($3.50 per 1 juta API calls)
- Cache: $14
- Data Transfer Out: $42 ($0.09/GB)

#### Lambda
- Biaya Request: $3
- Biaya Compute: $174 (rata-rata 2.37 detik/invocation dengan alokasi memory sebesar 256MB)

#### Total Biaya: $370

>>> Kunjungi artikel lengkapnya [Serving 39 Million Requests for $370/Month, or: How We Reduced Our Hosting Costs by Two Orders of Magnitude](https://trackchanges.postlight.com/serving-39-million-requests-for-370-month-or-how-we-reduced-our-hosting-costs-by-two-orders-of-edc30a9a88cd)

---

### Kesimpulan

>>> Dengan 5 kisah sukses tersebut, sudah siapkah anda dipermudah oleh arsitektur serverless?

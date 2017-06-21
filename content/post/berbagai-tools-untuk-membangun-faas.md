+++
title = "Mengenal Berbagai Tools untuk Membangun Aplikasi Berarsitektur Serverless"
author = "ridwanbejo"
share = true
tags = ["serverless", "amazon web service", "microsoft azure", "google cloud platform", "openwhisk", "iron io"]
draft = false
menu = ""
image = "images/default.jpg"
slug = "mengenal-berbagai-tools-untuk-membangun-aplikasi-berarsitektur-serverless"
date = "2017-06-17T02:24:24+07:00"
comments = true
+++

## Pendahuluan

*Serverless* memang masih belum lazim di khalayak IT Indonesia. Namun perlahan tapi pasti, rekan - rekan IT yang sudah mulai banyak menggunakan *virtual private server*, *platform as a service*, dan layanan *cloud* lainnya mungkin akan mulai melirik sesuatu yang dinamakan dengan *serverless architecture* ini.

Memang *vendor* besar yang baru menyediakan masih didominasi oleh Amazon Web Service, Microsoft Azure, dan Google Cloud Platform. Namun walaupun baru tiga yang secara resmi membuka layanan ini, berbagai *tools* untuk membangun aplikasi *serverless* ini sudah bermunculan.

## Berbagai Framework Arsitektur untuk Serverless

Berikut adalah berbagai *tools* untuk memulai pembuatan aplikasi *serverless* dengan bahasa pemrograman yang kamu sukai:

### Azure Function Tool

Azure Function Tool adalah peralatan untuk *local development* dalam membuat, menguji, menjalankan, *debugging*, dan *deploy* kode kita ke Azure Function Service.

* Github url: https://github.com/Azure/azure-functions-cli
* Github Stars: 65
* Bahasa Pemrograman: Node.js, C#, F#
* Sistem Operasi: Windows
* FaaS Service: Azure Function

### Turtle

Turtle adalah *toolkit* untuk membangun aplikasi *serverless* yang bersifat *event driven*. Kamu dapat membuat sebuah *function* Node.js yang akan di-*deploy* ke berbagai layanan FaaS.

* Github url: https://github.com/iopipe/turtle/
* Github Stars: 145
* Bahasa Pemrograman: Node.js
* Sistem Operasi: Windows, OSX, Linux, BSD
* FaaS Service: AWS Lambda, Azure Function, Google Cloud Function

### Lambada

Lambada dapat membantu kamu membuat REST API berbasis *serverless* dengan menggunakan bahasa Java. Lambada menggunakan JAX-RS API dan dapat men-*deploy* aplikasi kamu secara mudah ke AWS Lambda dan API Gateway

* Github url: https://github.com/lambadaframework/lambadaframework
* Github Stars: 193
* Bahasa Pemrograman: Node.js
* Sistem Operasi: Windows, OSX, Linux, BSD
* FaaS Service: AWS Lambda

### Shep

Shep adalah *toolkit* untuk membangun aplikasi *serverless* yang dapat di-*deploy* di AWS API Gateway dan AWS Lambda. Kamu dapat menggunakan Node.js untuk membuat aplikasi *serverless* menggunakan Sheep.

* Github url: https://github.com/bustle/shep
* Github Stars: 200
* Bahasa Pemrograman: Node.js
* Sistem Operasi: Windows, OSX, Linux, BSD
* FaaS Service: AWS Lambda

### Sparta

Sparta adalah *toolkit* untuk membangun aplikasi *serverless* yang dapat di-*deploy* di AWS API Gateway dan AWS Lambda. Kamu dapat menggunakan Go untuk membuat aplikasi *serverless* menggunakan Sparta.

Selain itu kamu juga dapat mengintegrasikan S3 dan SNS sebagai *event source*, dan dapat juga membantu kamu men-*deploy* *static website* di S3.

* Github url: https://github.com/mweagle/Sparta
* Github Stars: 332
* Bahasa Pemrograman: Go
* Sistem Operasi: Windows, OSX, Linux, BSD
* FaaS Service: AWS Lambda

### Python Lambda

Python Lambda adalah *toolkit* untuk membangun aplikasi *serverless* yang dapat di-*deploy* di AWS Lambda menggunakan bahasa pemrograman Python.

* Github url: https://github.com/nficano/python-lambda
* Github Stars: 414
* Bahasa Pemrograman: Python
* Sistem Operasi: Windows, OSX, Linux, BSD
* FaaS Service: AWS Lambda

### Deep

Deep adalah *toolkit* untuk membangun aplikasi *serverless* yang dapat di-*deploy* di berbagai Faas Service. Kamu dapat menggunakan Node.js untuk membuat aplikasi *serverless* menggunakan Deep.

* Github url: https://github.com/MitocGroup/deep-framework
* Github Stars: 448
* Bahasa Pemrograman: Node.js
* Sistem Operasi: Windows, OSX, Linux, BSD
* FaaS Service: AWS Lambda, Azure Function, Google Cloud Function

### Lambdoku

Lambdoku adalah *toolkit* untuk membangun aplikasi *serverless* yang memberikan pengalaman seperti menggunakan Heroku Toolbet sat menggunakan AWS Lambda.

* Github url: https://github.com/kubek2k/lambdoku
* Github Stars: 564
* Bahasa Pemrograman: Node.js
* Sistem Operasi: Windows, OSX, Linux, BSD
* FaaS Service: AWS Lambda

### AWS Lambda Go

AWS Lambda Go adalah *toolkit* untuk membangun aplikasi *serverless* dengan menggunakan Go di AWS Lambda.

* Github url: https://github.com/eawsy/aws-lambda-go
* Github Stars: 584
* Bahasa Pemrograman: Go
* Sistem Operasi: Windows, OSX, Linux, BSD
* FaaS Service: AWS Lambda


### Kappa

Kappa adalah *toolkit* untuk membangun aplikasi *serverless* yang dapat di-*deploy* di berbagai AWS Lambda menggunakan bahasa pemrograman Python. Namun kamu dapat mengintegrasikannya dengan berbagai *event source* seperti Cloudwatch, S3, dan SNS. Kamu juga dapat mengatur IAM Role melalui Kappa.

* Github url: https://github.com/garnaat/kappa
* Github Stars: 854
* Bahasa Pemrograman: Python
* Sistem Operasi: Windows, OSX, Linux, BSD
* FaaS Service: AWS Lambda

### Wsk

Wsk adalah *toolkit* untuk membangun aplikasi *serverless* yang di-*deploy* di Apache OpenWhisk. Sebuah proyek *open source* yang dapat membantu kamu membangun layanan Faas Sendiri. Wsk sudah terintegrasi di dalam proyek Apache OpenWhisk ini.

* Github url: https://github.com/apache/incubator-openwhisk
* Github Stars: 1570
* Bahasa Pemrograman: Node.js
* Sistem Operasi: Windows, OSX, Linux, BSD
* FaaS Service: Apache OpenWhisk

### IronFunction

Iron Function adalah *toolkit* untuk membangun aplikasi *serverless* yang di-*deploy* di Iron.IO. Sebuah layanan FaaS yang dikenal dengan IronMQ-nya.

* Github url: https://github.com/iron-io/functions
* Github Stars: 1570
* Bahasa Pemrograman: Go
* Sistem Operasi: Windows, OSX, Linux, BSD
* FaaS Service: Iron.IO

### Gordon

Gordon adalah sebuah *toolkit* yang dapat membantu kamu membangun aplikasi *serverless* yang memberikan pilihan bahasa pemrograman cukup banyak. Gordon ditujukan untuk membangun aplikasi *serverless* menggunakan AWS Lambda dan AWS Cloud Formation.

Gordon juga memiliki integrasi dengan API Gateway, Cloudwatch, DynamoDB, Kinesis Stream, dan S3. Selain itu kamu dapat melakukan *development* secara lokal menggunakan bahasa pemrograman kesukaan kamu.

* Github url: https://github.com/jorgebastida/gordon
* Github Stars: 1847
* Bahasa Pemrograman: Python, Node.js, Go, Java, Kotlin, Scala
* Sistem Operasi: Windows, OSX, Linux, BSD
* FaaS Service: AWS Lambda

### Claudia.js

Claudia.js adalah *toolkit* untuk membangun aplikasi *serverless* yang dapat di-*deploy* di AWS Lambda dan API Gateway. Kamu dapat menggunakan Node.js untuk membuat aplikasi *serverless* menggunakan Claudia.js.

* Github url: https://github.com/claudiajs/claudia
* Github Stars: 2059
* Bahasa Pemrograman: Node.js
* Sistem Operasi: Windows, OSX, Linux, BSD
* FaaS Service: AWS Lambda

### AWS Chalice

Chalice adalah *toolkit* untuk membangun aplikasi *serverless* yang dapat di-*deploy* di AWS Lambda dan API Gateway. Kamu dapat menggunakan Python untuk membuat aplikasi *serverless* menggunakan Chalice.

Chalice ini memiliki *pattern* yang mirip dengan Flask. Salah satu *web framework* populer di Python.

* Github url: https://github.com/awslabs/chalice
* Github Stars: 2770
* Bahasa Pemrograman: Python
* Sistem Operasi: Windows, OSX, Linux, BSD
* FaaS Service: AWS Lambda

### Zappa

Zappa adalah *toolkit* untuk membangun aplikasi *serverless* yang dapat di-*deploy* di AWS Lambda dan API Gateway. Kamu dapat menggunakan Python untuk membuat aplikasi *serverless* menggunakan Zappa.

Zappa memiliki dukungan terhadap berbagai layanan AWS seperti VPC, S3, SNS, SQS, Cloudwatch, DynamoDB, dan Kinesis Stream. Selain itu Zappa juga dapat membantu kamu menjalankan *asynchronous function*.

Uniknya, Zappa ini dapat membantu kamu menulis sebuah *service* yang ditulis menggunakan *web framework* berbasis WSGI seperti Flask, Django, Falcon, dan Bottle. Jadi bila *framework* *serverless* lain menggunakan *function* Python biasa dan mendefinisikannya di *file* konfigurasi. Berbeda dengan Zappa, kamu dapat membuat beberapa *endpoint*, misalnya ditulis menggunakan Flask, dan di-*deploy* ke satu *lambda*. Sehingga dalam satu *lambda* bisa mempunya *sub-endpoint*.

* Github url: https://github.com/Miserlou/Zappa
* Github Stars: 4113
* Bahasa Pemrograman: Python
* Sistem Operasi: Windows, OSX, Linux, BSD
* FaaS Service: AWS Lambda

### Apex

Apex adalah *toolkit* untuk membangun aplikasi *serverless* yang dapat di-*deploy* di AWS Lambda dan API Gateway. Kamu dapat menggunakan berbagai bahasa pemrograman untuk membuat aplikasi *serverless* menggunakan Apex.

Apex memiliki dukungan terhadap VPC, dan beberapa layanan AWS yang diintegrasikan dengan *function* yang kamu buat.

* Github url: https://github.com/apex/apex
* Github Stars: 5507
* Bahasa Pemrograman: Python, Node.js, Go, Java, Rust, Clojure
* Sistem Operasi: Windows, OSX, Linux, BSD
* FaaS Service: AWS Lambda

### Serverless Framework

Framework *serverless* yang dikembangkan oleh Serverless Inc. ini merupakan salah satu *framework* yang sangat populer dikalangan *serverless architecture*.

Serverless Framework adalah *toolkit* untuk membangun aplikasi *serverless* yang dapat di-*deploy* di berbagai FaaS. Kamu dapat menggunakan berbagai bahasa pemrograman untuk membuat aplikasi *serverless* menggunakan FaaS.

Selain itu, kehebatan *framework* yang satu ini adalah dukungan terhadap integrasi berbagai layanan yang ada di suatu *provider*. Misal bila kita ingin membuat aplikasi *serverless* di Azure, kamu dapat mengintegrasikannya dengan Service Bus Queue, Blob Storage, Notification Hub, Azure SQL Database, dan lainnya. Begitupun bila kita membidik AWS dan Google Cloud Platform.

Serverless Framework ini merupakan salah satu *framework* yang paling niat dikembangkan oleh komunitas dan kontributornya karena memiliki visi yang sangat kuat. Selain itu dokumentasinya sangat lengkap dan mudah dibaca. Kemudian Serverless Framework pun memiliki *plugin* yang kompatibel dengannya dalam jumlah yang sangat banyak.

Saat ini komunitasnya masih terpusah di Amerika Serikat, Eropa, dan Jepang. Dan mungkin popularitasnya ini disebabkan namanya sendiri yang merupakan nama dari arsitektur *serverless* itu sendiri sehingga selalu muncul di halaman hasil pencarian Google.

* Github url: https://github.com/serverless/serverless
* Github Stars: 17174
* Bahasa Pemrograman: Python, Node.js, Java, Scala
* Sistem Operasi: Windows, OSX, Linux, BSD
* FaaS Service: AWS Lambda, Azure Function, Google Cloud Function, IBM OpenWhisk

## Penutup

Dari berbagai Tools diatas yang telah saya catat, paling banyak bahasa pemrograman yang digunakan untuk *serverless architecture* ini adalah Node.js. Dan Amazon Web Service adalah salah satu layanan yang banyak digemari oleh para pembuat *framework* untuk membangun aplikasi berarsitektur *serverless*.

+++
author = "tajhulfaijin"
comments = true
date = "2017-09-03T02:24:24+07:00"
draft = false
image = ""
menu = ""
share = true
slug = "berkenalan-dengan-Claudiajs"
tags = ["claudiajs", "serverless","serverless-tools"]
title = "Berkenalan dengan ClaudiaJS"

+++

![ claudiajs.svg ](/images/berkenalan-dengan-claudiajs/claudiajs.svg "Claudisjs")


#### Claudiajs, apakah itu ?

[Claudiajs](https://Claudiajs.com "Claudia Js") merupakan salahsatu *deployment utility* berbasis Javascript (NodeJS) yang dapat membantu developer memangkas waktu dan *learning curve* dalam proses pengembangan aplikasi berbasis *Function As Service*. 

Claudiajs bukanlah sebuah framework melainkan hanya sebuah *deployment utility* yang membantu mempermudah developer untuk melakukan *deployment function* ke cloud *FaaS platform*. Berbeda dengan tools lainnya seperti [Serverless Framework](https://github.com/serverless/serverless) dan [Seneca](http://senecajs.org/), Claudiajs tidak melakukan abstraksi servis-servis *FaaS platform*. Claudiajs memberikan fleksibilitas tinggi dalam hal manajemen struktur kode aplikasi. Claudiajs tidak memiliki aturan khusus mengenai struktur kode aplikasi aplikasi.

> "Claudiajs bukanlah sebuah framework melainkan hanya sebuah deployment utility"

Sampai saat ini Claudiajs hanya support satu cloud FaaS provider saja, yaitu [AWS Lambda](https://aws.amazon.com/lambda/).

Versi terakhir Claudiajs sampai tulisan ini dibuat adalah versi **2.14.x** tepatnya versi **2.14.1** *dikomputer penulis*. Kita dapat memantau terus perkembangan *release history* melalui akun github Claudiajs [Claudis JS Release History](https://github.com/Claudiajs/claudia/blob/master/RELEASES.md).

```
⇒  claudia --version
2.14.1
```

#### Instalasi 

Claudiajs adalah *tools* yang dibangun diatas pondasi NodeJS, sehingga proses instalasi Claudiajs dapat dilakukan melalui Node Package Manager (NPM) seperti berikut :
```
npm install claudia -g
```

#### Fitur-fitur Claudiajs

Adapun fitur yang disediakan oleh Claudiajs, diantaranya :

1. Function deployment

    Fitur yang membantu kita untuk melakukan *deployment* fungsi Lambda. Seperti pada umumnya, fungsi Lambda disini digunakan dalam *event-driven micro services* sistem, dimana satu dua buah fungsi Lambda saling terkoneksi secara proses melalui event yang terjadi dan telah ditentukan oleh developer.
     

    ```
    claudia create --region us-east-1 --handler lambda.handler
    ```


2. API Builder

    Sebuah *library* dari Claudiajs yang membantu mempermudah developer dalam berinteraksi dengan servis [AWS API Gateway](https://aws.amazon.com/api-gateway/). Sangat membantu dalam memangkas waktu dan *learning curve* untuk membangun aplikasi web APIs diatas AWS. Developer tidak perlu melakukan proses manual untuk mengantur *request* dan *response*  ke dan dari API gateway, dan juga tidak perlu melakukan secara manual menghubungkan method yang ada di API gateway ke fungsi Lambda.


    ```
    const ApiBuilder = require('claudia-api-builder'),
        api = new ApiBuilder();

    module.exports = api;

    api.get('/about', function (request) {
        return 'Welcome ' + request.queryString.name + ' to Serverless Indonesia Community.';
    });
    ```

3. Chatbot Builder

    Sebuah *library* dari Claudiajs yang membantu developer untuk mengembangakan aplikasi chatbot. 
    
    Adapun platform chat yang didukung oleh library ini antara lain : *Facebook Messenger*, *Telegram*, *Skype*, *Slack slash commands*, *Twilio*, *Kik* dan *GroupMe*.

    Claudiajs akan secara otomatis melakukan *setup integration* seperti *webhooks* dan lain-lain untuk masing-masing platform chat diatas. Melakukan konversi format pesan yang masuk dan keluar dari platform chat diatas ke dalam satu format general yang lebih sederhana sehingga developer hanya menggunakan satu format untuk semua platform chat diatas.


    ```
    const botBuilder = require('claudia-bot-builder'),
        excuse = require('huh');

    module.exports = botBuilder(function (request) {
    return 'Thanks for sending ' + request.text  + 
        '. Welcome to Serverless Indonesia.' + 
        excuse.get();
    });
    ```
>> Untuk dokumentasi lebih lengkapnya, kunjungi [https://Claudiajs.com/documentation.html](https://Claudiajs.com/documentation.html) 

### Kesimpulan
Dengan Claudiajs, proses *deployment* fungsi Lambda akan jauh lebih sederhana dan cepat, developer tidak perlu lagi melakukan *setting* komponen-komponen yang dibutuhkan secara manual, dengan demikian dapat membantu mempercepat waktu pengembangan aplikasi berbasis FaaS. 

Demikan sekilas pengenalan tentang Claudiajs. Pada kesempatan berikutnya, kita akan membahas secara lebih mendetail ketiga fitur dari Claudiajs diatas. Semangat belajar dan berkarya!
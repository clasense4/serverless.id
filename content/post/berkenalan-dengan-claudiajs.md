+++
author = "tajhulfaijin"
comments = true
date = "2017-09-02T02:24:24+07:00"
draft = false
image = ""
menu = ""
share = true
slug = "berkenalan-dengan-claudiajs"
tags = ["claudiajs", "serverless", "serverless-framework"]
title = "Berkenalan dengan ClaudiaJS"

+++

![ claudiajs.svg ](/images/berkenalan-dengan-claudiajs/claudiajs.svg "Claudisjs")
[Claudiajs](https://claudiajs.com "Claudia Js") merupakan salahsatu *deployment utility* berbasis *javascript (NodeJS)* yang dapat membantu developer dalam proses pengembangan aplikasi berbasis *Function As Service*. 

Claudiajs bukanlah sebuah framework melainkan hanya sebuah *deployment utility* yang membantu mempermudah developer untuk melakukan *deployment function* ke cloud *FaaS platform*. Berbeda dengan tools lainnya seperti [Serverless Framework](https://github.com/serverless/serverless) dan [Seneca](http://senecajs.org/), claudiajs tidak melakukan abstraksi servis-servis *FaaS platform*. Claudiajs memberikan fleksibilitas tinggi dalam hal manajemen struktur kode aplikasi, claudiajs tidak memiliki aturan khusus mengenai struktur kode aplikasi aplikasi.

Proses instalasi claudiajs :
```
npm install claudia -g
```

Sampai saat ini claudiajs hanya support satu cloud FaaS provider saja, yaitu [AWS Lambda](https://aws.amazon.com/lambda/).

Versi terakhir claudiajs sampai tulisan ini dibuat adalah versi **2.14.x** tepatnya versi **2.14.1** *dikomputer penulis*. Kita dapat memantau terus perkembangan *release history* melalui akun github claudiajs [Claudis JS Release History](https://github.com/claudiajs/claudia/blob/master/RELEASES.md).

```
⇒  claudia --version
2.14.1
```

Adapun fitur yang disediakan oleh claudiajs, diantaranya :

1. Function deployment

    Fitur yang membantu kita untuk melakukan deployment fungsi Lambda.
    ```
    claudia create --region us-east-1 --handler lambda.handler
    ```

2. API Builder

    Adalah sebuah *library* dari claudiajs yang membantu mempermudah developer dalam berinteraksi dengan servis [AWS API Gateway](https://aws.amazon.com/api-gateway/). Sangat membantu dalam memangkas waktu dan *learning curve* untuk membangun aplikasi web APIs diatas AWS. Developer tidak perlu melakukan proses manual untuk mengantur *request* dan *response*  ke dan dari API gateway, dan juga tidak perlu melakukan secara manual menghubungkan method yang ada di API gateway ke fungsi Lambda.

    ```
    const ApiBuilder = require('claudia-api-builder'),
        api = new ApiBuilder();

    module.exports = api;

    api.get('/about', function (request) {
        return 'Welcome ' + request.queryString.name + ' to Serverless Indonesia Community.';
    });
    ```

3. Chatbot Builder 

    Adalah sebuah *library* dari claudiajs yang membantu developer untuk mengembangakan aplikasi chatbot. 
    
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

Demikan sekilas pengenalan tentang claudiajs *deployment utility*.

Pada tutorial berikutnya, kita akan membahas secara lebih mendetail ketiga fitur claudiajs diatas. Semangat belajar dan berkarya!
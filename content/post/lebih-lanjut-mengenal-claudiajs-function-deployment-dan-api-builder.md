+++
author = "tajhulfaijin"
comments = true
date = "2017-09-21T10:54:24+02:00"
draft = false
image = ""
menu = ""
share = true
slug = "function-deployment-dan-api-builder-claudiajs"
tags = ["claudiajs", "serverless","serverless-tools"]
title = "Mengenal fitur ClaudiaJS : Function deployment tools"

+++


>>> Lanjutan dari artikel sebelumnya [berkenalan dengan ClaudiaJS](/post/berkenalan-dengan-claudiajs/).

<!--more-->

Pada kesempatan ini kita akan membahas lebih dalam salahsatu dari tiga fitur yang dimiliki oleh [Claudiajs](https://Claudiajs.com "Claudia Js"), yaitu _Function Deployment Tools_.

![ gears-3.png ](https://pptcrafter.files.wordpress.com/2013/01/gears-3.png "functions is like gears")

### _Function deployment tools_, apakah itu ?

_Claudia function deployment tools_ adalah sebuah _command line interface (CLI)_ yang dapat digunakan untuk melakukan *deployment* fungsi _Lambda_ dari _local_ komputer kita ke _AWS Lambda console_. 

Proses deployment disini meliputi : membuat fungsi _Lambda_, memperbaharui fungsi _Lambda_, menghapus fungsi _Lambda_, mengatur versi dari fungsi _Lambda_, dan masih banyak lagi.  

Seperti pada umumnya, fungsi _Lambda_ disini digunakan dalam *event-driven micro services* sistem, dimana satu dua buah fungsi Lambda saling terkoneksi secara proses melalui *event* yang terjadi dan telah ditentukan oleh *developer*.


#### Membuat fungsi _Lambda_


Untuk melakukan proses _deployment_ fungsi _Lambda_ untuk pertama kalinya, kita bisa menggunakan perintah :

```
claudia create --region [kode region] --handler [nama handler]
```


Dimana :

-   **kode region** : adalah kode [region AWS](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-regions-availability-zones.html#concepts-available-regions) dimana kita akan mempublish kode _Lambda_ kita;

-   **nama handler** : nama fungsi yang akan digunakan sebagai _Lambda_ handler function. Konvensi untuk nama handler ini adalah : **nama-file[dot]nama-fungsi-handler** 


Contoh :

1. Inisialisasi project, dengan menggunakan perintah : [**npm init**](https://docs.npmjs.com/cli/init)
2. Buat sebuah javascript file dengan nama **lambda.js**

    ```
    exports.handler = function (event, context) {
        context.succeed('Halo, serverless Indonesia!');
    };
    ```
2. Deploy fungsi tersebut dengan perintah :
    
    ```
    claudia create --region ap-southeast-1 --handler lambda.handler
    ```
    Jika tidak mengalami kendala, kita akan mendapatkan _deployment status feedback_  pada console seperti berikut :

    ```json
    saving configuration
    {
        "lambda": {
            "role": "lambda-basic-executor",
            "name": "lambda-basic",
            "region": "ap-southeast-1"
        }
    }
    ```    

    Setelah proses _deployment_ selesai, pada direktori root project, akan terdapat file baru bernama **claudia.json**. 

    ![ claudiajson.png ](/images/claudiajs-function-deployment-dan-api-builder/claudiajson.png "claudia.json")

    Dimana pada file tersebut berisi informasi tentang fungsi _Lambda_ yang telah berhasil di deploy. Informasi tersebut meliputi :
    - **role** : berisi id dari [AWS IAM role](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html) yang dipakai fungsi _Lambda_ tersebut
    - **name** : adalah nama fungsi _Lambda_ tersebut (_Nama fungsi Lambda yang di deploy akan sama dengan nama project yang kita isi pada proses inisialisasi project pada langkah nomor 1 diatas_).
    - **region** : id region dimana fungsi _Lambda_ kita dideploy


Kita dapat melakukan testing fungsi _Lambda_ yang telah dideploy tersebut dari _local_ komputer kita secara langsung tanpa perlu melalui _Lambda_ console.

```
claudia test-[nama fungsi]
```

```
claudia test-lambda

{
  "StatusCode": 200,
  "Payload": "\"Halo, serverless Indonesia!\""
}
```

#### Memperbaharui fungsi _Lambda_

Untuk melakukan perubahan pada fungsi _Lambda_, kita bisa menggunakan perintah berikut :

```
claudia update
```


Contoh :

1. Perbaharui fungsi _Lambda_ pada _local_ komputer kita


    ```
    exports.handler = function (event, context) {
        context.succeed('Serverless Indonesia Jaya!');
    };
    ```

2. Kemudian deploy fungsi yang telah diperbaharui diatas agar fungsi _Lambda_ yang sudah dideploy sebelumnya juga ikut diperbaharui


    ```
    claudia update
    ```
    Jika tidak mengalami kendala, kita akan mendapatkan deployment update status feedback pada console seperti berikut :

    ```
    updating Lambda	lambda.setupRequestListeners
    {
        "FunctionName": "lambda-basic",
        "FunctionArn": "arn:aws:lambda:ap-southeast-1:996680382794:function:lambda-basic:2",
        "Runtime": "nodejs6.10",
        "Role": "arn:aws:iam::996680382794:role/lambda-basic-executor",
        "Handler": "lambda.handler",
        "CodeSize": 810,
        "Description": "test deploy basic lambda function",
        "Timeout": 3,
        "MemorySize": 128,
        "LastModified": "2017-09-21T13:28:53.194+0000",
        "CodeSha256": "UgJ+ClnSxgo+Ux8Bknp3Dj+O3KLJAeunNGW+Nk4Zk1E=",
        "Version": "2",
        "KMSKeyArn": null,
        "TracingConfig": {
            "Mode": "PassThrough"
        }
    }
    ```    

    Kemudian kita bisa test hasil pembaharuan tersebut dengan perintah claudia test 
   ```
    claudia test-lambda
    {
      "StatusCode": 200,
      "Payload": "\"Serverless Indonesia Jaya!\""
    }
   ``` 

#### Menghapus fungsi _Lambda_

Untuk menghapus fungsi _Lambda_ yang sudah di _deploy_, kita bisa menggunakan perintah [```claudia destroy```](https://github.com/claudiajs/claudia/blob/master/docs/destroy.md)

Contoh : 

```
claudia destroy
```

Proses ini akan menghapus fungsi _Lambda_ yang sudah kita deploy berserta dengan depedensi nya seperti _**IAM role**_ yang dipake fungsi _Lambda_ tersebut.

#### _Version aliasing_ fungsi _Lambda_

Dalam proses development aplikasi, sudah menjadi suatu kewajiban agar kita mempunyai _version stage_ dari aplikasi yang kita bangun. _Claudia CLI_ menyediakan fitur untuk memudahkan kita dalam melakukan versioning fungsi _Lambda_. Kita cukup menambahkan opsi ``` --version ``` pada proses create atau update fungsi _Lambda_.

Contoh ketika melakukan proses deployment pertama kali (disini kita set sebagai versi **development**) : 


```
claudia create --region ap-southeast-1 --handler lambda.handler --version development
```    

Kemudian ketika melakukan proses _update_ versi tertentu (versi **development**)

```
claudia update --version development
```    

#### Kesimpulan
_Claudia function deployment tools_ dapat membantu kita dalam proses _deployment_ fungsi _Lambda_ yang kita _develop_ di _local_ komputer kita. _Claudia function deployment tools_ ini bukanlah pengganti dari _AWS command line interface_, namun merupakan sebuah tools yang meng-_enkapsulasi_ proses _deployment_ fungsi _Lambda_ sehingga proses _deployment_ fungsi _Lambda_ menjadi lebih ringkas dan mudah.

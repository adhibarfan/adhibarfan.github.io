---
layout: post
title: Hello World CodeIgniter
modified:
categories: 
excerpt: Mengenal Controller dan View dalam Membuat Hello World
tags: []
comments: true
share: true
image:
  feature:
date: 2016-09-11T10:37:16+07:00
---

## CodeIgniter
>> CodeIgniter merupakan aplikasi sumber terbuka yang berupa framework PHP dengan model MVC (Model, View, Controller) untuk membangun website dinamis dengan menggunakan PHP. 

Dengan menggunakan framework akan mempermudah dan mempercepat pekerjaan seorang programmer tanpa harus membuat fungsi atau class dari awal. Framework Codeigniter menggunakan konsep MVC (Model, view, Controller) yaitu :

* ***Model*** biasanya digunakan untuk eksekusi query database, semua hal yang berhubungan dengan database akan di eksekusi oleh Model
* ***View*** digunakan untuk menerima dan merepresentasikan data kepada user, hasil yang telah di olah oleh Controller akan di tampilkan pada View.
* ***Controller*** digunakan untuk menghubungkan antara Model dan View.

Untuk lebih jelasnya alangkah lebih baik kalau langsung di praktikan. 

#### Install CodeIgniter

1. Download CodeIgniter, silahkan download file CodeIgniter pada website resmi nya [https://www.codeigniter.com](https://www.codeigniter.com/download)
2. Ekstrak file yang telah di download kemudian rename menjadi HelloWorldCodeIgniter, letakan file yang telah di rename di htdoc(Windows) bagi yang menggunakan ubuntu diletakan  /var/www/html/disini sedangkan bagi yang belum mempersiapkan coding pada php silahkan berkunjung ke blog [persiapan coding php](rizkimufrizal.github.io)
3. run file dengan mengakses 127.0.0.1/HelloWorldCodeIgniter/ maka akan tampil tampilan seperti pada gambar ![welcometoci.png](../images/welcometoci.png)

#### Membuat Hello World
Untuk membuat output Hello World langkah pertama adalah membuat Controller baru dengan nama HelloWorldController.php pada folder Controllers (HelloWorldcodeIgniter/application/controllers). 

![HelloWorldController.png](../images/HelloWorldController.png)

kemudian masukan code berikut ini
{% highlight php %}
<?php
defined('BASEPATH') OR exit('No direct script access allowed');

class HelloWorldController extends CI_Controller {

    public function index()
    {
        $this->load->view('tampilanIndex');
    }

    public function functionBelajar()
    {
        $this->load->view('tampilanFunctionBelajar');
    }
}
{% endhighlight %}

Disini kita membuat dua function, yaitu function index() dan function functionBelajar(). Funtion index akan menampilkan hasil tampilanIndex.php, sedangkan function functionBelajar() akan menampilkan tampilan tampilanFunctionBelajar.php. 

Setelah membuat controller HelloWorldController.php langkah selanjutnya adalah membuat tampilan tampilanIndex.php dan tampilanFunctionBelajar.php pada folder View (HelloWorldcodeIgniter/application/views) 

![Views.png](../images/Views.png)
***tampilanIndex.php***
{% highlight html %}
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Tampilan Index</title>
</head>
<body>
    <h1>Hello World</h1>
    <h2>Ini adalah tampilan Index()</h2>
</body>
</html>
{% endhighlight %}
***tampilanFunctionBelajar.php***
{% highlight html %}
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Tampilan Function Belajar</title>
</head>
<body>
    <h1>Hello World</h1>
    <h2>Ini adalah tampilan functionBelajar()</h2>
</body>
</html>
{% endhighlight %}

Setelah selesai membuat tampilan, langkah selanjutnya adalah menjalankan function yang telah dibuat dengan cara mengakses 127.0.0.1/HellowWorldCodeIgniter/index.php/NamaController/NamaFunction




---
layout: post
title: Convert Certificate .jks to .p12 Menggunakan Keytool
modified:
categories: 
excerpt: Convert .jks to .p12
tags: []
image:
  feature:
date: 2017-06-21T15:48:04+07:00
---
>>> Java KeyStore (JKS) adalah gudang sertifikat keamanan - sertifikat otorisasi atau sertifikat kunci publik - ditambah kunci pribadi yang sesuai, yang digunakan misalnya dalam enkripsi SSL. [wikipedia](https://en.wikipedia.org/wiki/Keystore)

Pada artikel ini membahas bagaimana merubah certificate.jks ke certificate.p12 menggunakan keytool. Kita harus install Java untuk menggunakan Keytool tersebut. Java yang kita install adalah java 8.

{% highlight bash %}
C:\Program Files\Java\jdk1.8.0_121\bin 
{% endhighlight %}

Command di atas adalah lokasi keytool.exe , langkah selanjutnya kita copy file.jks ke dalam direktori `bin` kemudian masuk ke direktori tersebut dengan menggunakan cmd (Run as administrator).
![path-keytool.png](../images/path-keytool.png)

### JKS -> P12
{% highlight bash %}
keytool -importkeystore -srckeystore adhibarfan.jks -destkeystore adhibarfan.p12 -srcstoretype JKS -deststoretype PKCS12 -deststorepass YourPassword
{% endhighlight %}

Command diatas adalah command yang digunakan untuk mengubah file.jks ke file.p12 dimana `adhibarfan.jks` diganti dengan file.jks yang akan dirubah menjadi file.p12, kemudian `YourPassword` diganti dengan password file.jks tersebut.

### P12 -> JKS
{% highlight bash %}
keytool -importkeystore -srckeystore adhibarfan.p12 -destkeystore adhibarfan.jks -srcstoretype JKS -deststoretype PKCS12 -deststorepass YourPassword
{% endhighlight %}

Command diatas adalah jika ingin mengembalikan file seperti sebelumnya. Berikut ini adalah output `JKS -> P12` ketika berhasil.
![output-p12.png](../images/output-p12.png)
[Terimakasih](https://stackoverflow.com/questions/2846828/converting-jks-to-p12)

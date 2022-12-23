---
layout: post
title: Cara Copy File Dari Server Ke Server Lain Menggunakan SCP
modified:
categories: 
excerpt: Transfer file manggunakan SCP
tags: []
image:
  feature:
date: 2017-06-21T09:59:39+07:00
---

>> Secure copy atau SCP adalah alat untuk mentransfer file komputer dengan aman antara host lokal dan host jarak jauh atau antara dua host jarak jauh. Hal ini didasarkan pada protokol Secure Shell (SSH). [wikipedia](https://en.wikipedia.org/wiki/Secure_copy)

Pada artikel ini adalah membahas bagaimana jika kita ingin mentransfer file dari server A ke server B ataupun sebaliknya. Bagi pengguna windows bisa langsung menggunakan [WinSCP](https://winscp.net/eng/download.php). Bagaimana jika server yang mau kita akses (kita anggap server A) tidak bisa di akses langsung menggunakan WinSCP dan hanya bisa diakses dari server B. 

Nah yang akan kita lakukan adalah masuk ke server B dengan menggunakan [Putty](http://www.putty.org/). setelah masuk ke server B, berikut ini adalah command yang digunakan untuk copy file.

### Copy file dari server B ke server A ketika login pada server B.
Login dari server B, kemudian jalankan perintah berikut.
{% highlight bash %}
scp -P 122/path/file username@ipServerA:/path/tujuan
{% endhighlight %}
`-P 122` adalah port server A, jika port server A masih menggunakan port default maka command `-P 122` dihilangkan.

### Copy file dari server B ke server A ketika login pada server A.
Login dari server A, kemudian jalankan perintah berikut.
{% highlight bash %}
scp -P 122 username@ipServerB:/path/file /path/tujuan
{% endhighlight %}
`-P 122` adalah port server B, jika port server B masih menggunakan port default maka command `-P 122` dihilangkan, [Terimakasih](https://unix.stackexchange.com/questions/106480/how-to-copy-files-from-one-machine-to-another-using-ssh).
---
layout: post
title: Membuka Port Redhat 7 Menggukanan firewall-cmd
modified:
categories: 
excerpt: Membuka firewall agar bisa diakses jaringan public
tags: []
image:
  feature:
date: 2017-06-01T15:21:46+07:00
---

>> Firewall adalah suatu sistem perangkat lunak yang mengizinkan lalu lintas jaringan yang dianggap aman untuk bisa melaluinya dan mencegah lalu lintas jaringan yang dianggap tidak aman. Umumnya, sebuah firewall diterapkan dalam sebuah mesin terdedikasi, yang berjalan pada pintu gerbang (gateway) antara jaringan lokal dengan jaringan Internet. [wikipedia](https://id.wikipedia.org/wiki/Tembok_api)

Dari penjelasan diatas dapat kita ambil kesimpulan bahwa firewall merupakan pengaman bagi lalu lintas jaringan yang sedang berlangsung yang dianggap aman. 

Secara default, port 80 untuk koneksi http difilter di Redhat 7 sehingga kita hanya dapat mengakses port ini dari localhost saja dan tidak bisa diakses dari host publik. Untuk membuka port 80 tersebut yaitu  menggunakan firewall-cmd. 

### Membuka port
{% highlight bash %}
firewall-cmd --zone=public --add-port=80/tcp --permanent
{% endhighlight %}

Perintah diatas digunakan untuk membuka port 80, atau bisa juga digunakan untuk membuka port lain sesuai dengan kebutuhan.

### Reload
Setelah port tersebut terbuka kemudian reload firewall dengan perintah

{% highlight bash %}
firewall-cmd --reload
{% endhighlight %}

### Melihat port yang sudah terbuka
Untuk melihat port yang sudah dibuka yaitu dengan perintah 
{% highlight bash %}
iptables-save | grep 80
{% endhighlight %}
grep 80 digunakan untuk filter

### Menutup port
Bagaimana jika kita ingin menutup port yang sudah dibuka? yaitu dengan perintah

{% highlight bash %}
firewall-cmd --zone=public --remove-port=80/tcp --permanent
{% endhighlight %}

[Terimakasih](https://linuxconfig.org/how-to-open-http-port-80-on-redhat-7-linux-using-firewall-cmd)


---
layout: post
title: Membuat Rumah Dengan Strawberry Prolog
modified:
categories: 
excerpt: Belajar membuat rumah dengan strawberry prolog
tags: [Membuat, rumah, strawberry prolog, prolog, laporan akhir]
comments: true
share: true
image:
  feature:
date: 2016-10-02T14:27:45+07:00
---

## Prolog
>> Prolog merupakan bahasa pemrograman logika atau disebut juga sebagai bahasa non-procedural. Nama Prolog merupakan singkatan dari “Programming in Logic“. Ide untuk mengembangkan pemrograman dalam logika, pertama kali dilakukan oleh Robert Kowalski di Edinburgh, Skotlandia pada tahun 1970-an.


nah trus apa bedanya prolog dengan strawberry prolog? ini dia penjelasan tentang strawberry prolognya.


## Strawberry Prolog
>> Strawberry Prolog dihasilkan oleh Institut Matematika dan Informatikapada Akademi Ilmu Pengetahuan Bulgaria. Versi pertama dirilis pada tahun 1996. Pemimpin tim Strawberry Dimiter Dobrev. Strawberry Prolog adalah dialek dari bahasa pemrograman Prolog. Sintaks-nya adalah sangat dekat dengan ISO-Prolog tetapi memiliki banyak ekstensi yang bukan bagian dari standar.

sekarang sudah tahu kan perbedaan antara prolog dan strawberry prolog? 

Sekarang langsung aja sesuai dengan judul yang saya tulis, bagaimana membuat rumah dengan menggunakan strawberry prolog? sebelum melihat code nya, saya tampilin dulu hasil nya seperti apa. ![rumahprolog.png](../images/rumahprolog.png) gimana cukup sederhana bukan rumahnya? berikut ini adalah code yang digunakan untuk membuat rumah seperti gambar diatas.

{% highlight prolog %}

?-
window(_,_,coba(),"Rumah",20,50,900,600).
coba(paint):-
%backgroundHijau
pen(5,rgb(55,199,32)),
brush(rgb(55,199,32)),
rect(0,400,900,600),

%backgroundLangit
pen(5,rgb(0,133,237)),
brush(5,rgb(0,133,237)),
rect(0,0,900,400),

%warnaRumah
pen(5,rgb(186,0,0)),
brush(rgb(186,0,0)),
fill_polygon(505,350,505,500,508,500,705,450),%tembok
fill_polygon(705,350,705,450,350,350,726,350),%tembok
fill_polygon(508,500,705,450,350,350,350,500),%pintuTembok

pen(5,rgb(95,55,21)),
brush(rgb(95,55,21)),
fill_polygon(428,245,323,350,323,350,726,350),%atap
fill_polygon(671,295,728,350,428,245,671,295),%atap
rect(390,390,470,500),
pen(5,rgb(255,255,50)),
brush(rgb(255,255,50)),
fill_polygon(580,450,640,440,580,390,580,450),%jendela
fill_polygon(640,440,640,387,580,450,640,440),%jendela
fill_polygon(580,390,640,387,580,450,640,440),%jendela

pen(5,rgb(218,218,218)),
brush(rgb(218,218,218)),
fill_polygon(470,500,175,600,400,500,50,600),%jalan
fill_polygon(390,500,470,500,50,600,175,600),%jalan

%membuatRumah
pen(5,rgb(0,0,0)),
brush(rgb(0,120,14)),
line(428,245,323,350),
line(323,350,726,350),
line(671,295,728,350),
line(428,245,533,350),
line(428,245,671,295),
line(705,350,705,450),
line(508,500,705,450),
line(350,500,505,500),

%membuatPintu
pen(5,rgb(0,0,0)),
brush(rgb(0,120,14)),
line(390,500,390,390),
line(390,390,470,390),
line(470,390,470,500),
line(390,500,470,500),
line(400,450,410,450),
line(390,500,470,500),
line(50,600,175,600),

%jendela
pen(5,rgb(0,0,0)),
line(580,390,640,387),
line(640,440,640,387),
line(580,390,580,450),
line(580,450,640,440),
line(580,420,640,415),
line(610,390,610,446),

%matahari
pen(5,rgb(255,255,50)),
brush(rgb(255,255,50)),
ellipse(295,45,375,125),
line(375,45,295,125),
line(295,45,375,125),
line(335,30,335,140),
line(375,45,295,125),
line(278,85,390,85).


{% endhighlight %}

penjelasan code program sebagai berikut:

1. ?-
Sintak yang digunakan untuk memulai program Strawberry Prolog

2. window(_,_,coba(),"Rumah",20,50,900,600)
Perintah window di buat untuk menampilkan jendela yang akan dijadikan sebagai program. Kalimat "Rumah" merupakan judul dari jendela outputnya. 20,50,900,600 adalah koordinat untuk menentukkan panjang dan lebar kotak window sesuai dengan kebutuhan.

3. coba(paint):-
Berfungsi untuk menandakan jendela output digunakan untuk menampilkan gambar.

4. pen(5,rgb(55,199,32)),
untuk memberikan garis tepi dengan ketebalan 5, dengan kombinasi warna rgb. rgb merupakan singkatan dari red green blue yang di dalamnya terdapat angka yang disesuaikan / dikombinasikan sesuai warna yang kita inginkan.

5. brush(rgb(55,199,32)),
Memberikan warna pada objek, misalnya untuk mewarnai bentuk bulat maka digunakan sintak ini.

6. rect(0,0,900,400),
Untuk membuat kotak background yang akan di brush menjadi warna biru langit.

7. ellipse(295,45,375,125),
Untuk membuat lingkaran pada matahari.

8. line(428,245,323,350),
Untuk membuat garis, sedangkan angka tersebut dapat diartikan x1,y1,x2,y2 dimana x1=428, y1=245, x2=323 dan y2=350.

9. fill_polygon(505,350,505,500,508,500,705,450),
Untuk mewarnai tembok dan pintu, fill_polygon ini membutuhkan tiga titik, dimana ketiga titik tersebut kita gunakan untuk 
mewarnai objek yang kita inginkan. Angka-angka yang diatas merupakan gabungan antara dua garis, ketika dijadikan satu dengan fill_polygon maka garis yang ketiga dengan sendirinya akan terbentuk. Misalnya kita ingin membuat segitiga, yang kita masukan kedalam fill_polygon adalah line untuk tinggi dan alas dari segitiga tersebut, maka dengan sendirinya garis miring pada segitiga akan terbentuk.

10. %
Memberikan komentar pada program yang sedang dibuat untuk mempermudah mengingat program yang sedang dibuat.

Sekian artikel tentang membuat rumah dengan strawberry prolog semoga bermanfaat :)
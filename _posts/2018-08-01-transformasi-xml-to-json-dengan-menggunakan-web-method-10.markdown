---
layout: post
title: Transformasi XML to JSON dengan Menggunakan Web Method 10
modified:
categories: 
excerpt: Transformasi XML to JSON
tags: []
image:
  feature:
date: 2018-08-01T11:36:01+07:00
---

Berikut ini adalah link dari web service yang akan di transform ke JSON  

* Description  
[http://www.dneonline.com/calculator.asmx](http://www.dneonline.com/calculator.asmx)

* WSDL  
[http://www.dneonline.com/calculator.asmx?WSDL ](http://www.dneonline.com/calculator.asmx?WSDL )

sample output soap  
![soapRequest.png](../images/soapRequest.png)  
sample output dari transformasi XML to JSON  
![restRequest.png](../images/restRequest.png)  

#### 1. Create new package dengan nama Calculator  
![packageCalculator.png](../images/packageCalculator.png)

#### 2. Create folder sesuai dengan kebutuhan yang akan digunakan  
![packageFolder.png](../images/packageFolder.png)  

#### 3.	Create new Web Service Descriptor 
web service descriptor ini digunakan untuk mendapatkan deskripsi dari webservice.  
![webServiceDescriptor.png](../images/webServiceDescriptor.png)  
  
* Disini kita sebagai consumer  -> `next`  
![consumerWsdl.png](../images/consumerWsdl.png)  
  
* kemudian input link wsdl yang akan digunakan  -> `finish`
![urlWdsl.png](../images/urlWdsl.png)  
  
* Hasil wdsl yang telah di import  
![folderCalculator.png](../images/folderCalculator.png)  
  
* Kemudian kita ganti Execute ACL nya menjadi Anonymous, agar service tersebut bisa di invoke tanpa menggunakan credentials.  
![aclAnonimous.png](../images/aclAnonimous.png)  

#### 4.	Membuat document type, yaitu digunakan sebagai data yang akan dijadikan sebagai input atau output.
![docType.png](../images/docType.png)  

* Membuat doctype dengan nama calInput
![calInput.png](../images/calInput.png)  

* dan membuat doctype dengan nama calOutput
![calOutput.png](../images/calOutput.png) 


#### 5.	Membuat flow service add (operasi tambah) dari kacamata web method.
![flowService.png](../images/flowService.png)  

* Drag and drop doctype yang telah dibuat sebelumnya.  
![addInputOutput.png](../images/addInputOutput.png) 

* Drag and drop service add pada soap yang telah di import, kemudian tambahkan flow MAP
![treeAdd.png](../images/treeAdd.png) 

* 1* mapping pipeline in dan out pada service CalculatorSoap_Add seperti gambar
![pipeline1.png](../images/pipeline1.png) 

* 2* mapping pipeline in dan out seperti gambar
![pipeline2.png](../images/pipeline2.png) 

* Jalankan flow tersebut
![runFlow.png](../images/runFlow.png) 

* Input value pada operation add
![inputAdd.png](../images/inputAdd.png) 

* Output yang dihasilkan
![outputAdd.png](../images/outputAdd.png) 


#### 6. Membuat flow baru dengan nama fAdd, yaitu flow yang dilihat dari sisi frontend
![fAdd.png](../images/fAdd.png) 

* Flow pada service fAdd
![flowServiceAdd.png](../images/flowServiceAdd.png) 

```Suquence 1 exit on success```  
```Sequence 2 exit on failure```  
```Sequence 3 exit on done```  

* 1*
![fAdd1.png](../images/fAdd1.png) 

* 2*
![fAdd2.png](../images/fAdd2.png) 

* 3*
![fAdd3.png](../images/fAdd3.png) 

* 4*
![fAdd4.png](../images/fAdd4.png) 

* Clear pipeline ini digunakan untuk menghapus semua output, jika ingin mengeluarkan output tertentu, tambahkan value dari preserve seperti gambar

![clearPipeline.png](../images/clearPipeline.png)

#### 7. Membuat rest client
![restResource.png](../images/restResource.png)

* REST V2 -> `Next`
![restv2.png](../images/restv2.png)

* penambahan method
![methodAdd.png](../images/methodAdd.png)

* done, silahkan invoke service tersebut sbb 

{% highlight bash %}
curl -X POST \   http://localhost:5555/restv2/calculator/add \   -H 'Content-Type: application/json' \   -d '{ 	"intA":"230", 	"intB":"3" }'
{% endhighlight %}


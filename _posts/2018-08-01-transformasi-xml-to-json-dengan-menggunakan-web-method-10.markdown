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



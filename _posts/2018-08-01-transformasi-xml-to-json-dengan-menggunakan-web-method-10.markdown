---
layout: post
title: Transformasi XML to JSON Dengan Menggunakan Web Method 10
modified:
categories: 
excerpt: Transformasi XML to JSON
tags: []
image:
  feature:
date: 2018-08-01T11:36:01+07:00
---

Berikut ini adalah link dari web service yang akan di transform ke JSON
Description
```sh
http://www.dneonline.com/calculator.asmx 
```
WSDL
```sh
http://www.dneonline.com/calculator.asmx?WSDL 
```
sample output soap  
![soapRequest.png](../images/soapRequest.png)  
Output dari transformasi XML to JSON  
![restRequest.png](../images/restRequest.png)  

#### 1. Create new package dengan nama Calculator  
![packageCalculator.png](../images/packageCalculator.png)

#### 2. Create folder sesuai dengan kebutuhan yang akan digunakan  
![packageFolder.png](../images/packageFolder.png)  

#### 3.	Create new Web Service Descriptor 
web service descriptor ini digunakan untuk mendapatkan deskripsi dari webservice.  
![webServiceDescriptor.png](../images/webServiceDescriptor.png)  

Disini kita sebagai consumer  -> `next`
![consumerWsdl.png](../images/consumerWsdl.png)  

kemudian input link wsdl yang akan digunakan  -> `finish`
![urlWdsl.png](../images/urlWdsl.png)  



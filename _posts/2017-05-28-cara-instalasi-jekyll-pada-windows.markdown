---
layout: post
title: Cara Instalasi Jekyll Pada Windows
modified:
categories: 
excerpt: Instalasi Jekyll untuk membuat blog
tags: []
image:
  feature:
date: 2017-05-28T14:13:32+07:00
---
>> Jekyll adalah generator situs statis sederhana (blog-aware) untuk situs pribadi, proyek, atau organisasi. Ditulis di Ruby oleh Tom Preston-Werner, pendiri GitHub, didistribusikan di bawah lisensi open source. [wikipedia](https://en.wikipedia.org/wiki/Jekyll_(software))


# Installation

Berikut ini adalah langkah-langkah yang diperlukan dalam instalasi Jekyll pada Windows

1. Install package manager untuk windows yaitu [Chocolatey](https://chocolatey.org/) sebagai berikut :
jalankan cmd dengan Run as administrator, kemudian copy paste perintah 
`@powershell -NoProfile -ExecutionPolicy Bypass -Command "iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"`

2. Install Ruby dan Ruby development kit
- Install Ruby `choco install ruby -version 2.2.4`
- Install RubyDevkit `choco install ruby2.devkit`

3. Configurasi Ruby development kit
 - Buka command prompt kemudian masuk ke direktori `C:\tools\DevKit2`
 - Execute `ruby dk.rb init` yang digunakan untuk membuat file `config.yml`
 - Edit file `config.yml` pada direktori `C:\tools\DevKit2` dengan menambahkan path Ruby `- C:/tools/ruby22`
 - Jalankan command ini to set the path: `ruby dk.rb install`

4. Nokogiri gem installation, Gem ini dibutuhkan pada github-pages agar bisa berjalan pada Windows x64.
 `choco install libxml2 -Source "https://www.nuget.org/api/v2/"`
 `choco install libxslt -Source "https://www.nuget.org/api/v2/"`
 `choco install libiconv -Source "https://www.nuget.org/api/v2/"`

5. Update latest RubyGems
 - Download lates `.gem` file [disini](https://rubygems.org/pages/download)
 - pada cmd jalankan perintah berikut `gem install --local C:\rubygems-update-2.6.12.gem` sesuaikan dengan direktori file `.gem` yang telah di download.
 - Kemudian jalankan perintah `update_rubygems` maka RubyGems akan melakukan update

 6. Install github-pages
 - Install [Bundler](http://bundler.io/), buka cmd Run as administrator kemudian jalankan perintah `gem install bundler`
 - Membuat file dengan nama `Gemfile` tanpa extension pada root direktori blog
 - copy & paste line berikut pada file `Gemfile`:
 `source 'https://rubygems.org'
gem 'github-pages', group: :jekyll_plugins
gem 'octopress', '~> 3.0'`
- Jalankan perintah `bundle install` pada root direktori blog.

After this process you should have github-pages installed on your system and you can host your blog again with `jekyll serve`, [Terimakasih](https://jekyllrb.com/docs/windows/). 



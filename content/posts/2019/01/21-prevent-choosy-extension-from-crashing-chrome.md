---
title: Choosy extension 搞掛 Chrome 的解法
description: ''
date: '2019-01-21T04:04:44.333Z'
slug: prevent-choosy-extension-from-crashing-chrome
tags: ['Chrome']
---

前陣子開始用 [Choosy](https://choosyosx.com) 讓不同的網站分別用不同的瀏覽器開。但是 Choosy 的 extension 一直讓 Chrome 掛掉，後來在[這篇](http://feedback.choosyosx.com/forums/6165-general/suggestions/35061085-choosy-crashes-chrome)找到解法：

在 Chrome 開啟 `x-choosy://prompt.all/` 這個網址，然後勾選「永遠用這個 App 開啟」、按下 OK。
---
title: JavaScript 的 diff 套件
description: diff 與 Google 的 diff-match-patch
date: '2019-03-22T08:34:59.090Z'
slug: diff-libraries-in-javascript
tags: ['JavaScript']
---

以前都用 [diff](https://www.npmjs.com/package/diff)，它能以字元（char）、單字（word）、行（line）、句（sentences）為單位比較；但是只能處理「行」為單位的 patch 。

最近發現 Google 的 [diff-match-patch](https://github.com/google/diff-match-patch) 能處理「字元」的 patch，而且支援非常多語言（C++、C#、Java、JavaScript、Python、……）。也有人把它包成 npm package：[diff-match-patch](https://www.npmjs.com/package/diff-match-patch)。
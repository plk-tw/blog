---
title: Git revision range
date: '2018-12-17T03:46:17.213Z'
slug: git-revision-range
tags:
  - Git
---

常忘記 `..` 跟 `...` 的差別：

- `A..B` （兩個點）表示：只列出在 B 有的
- `A...B` （三個點）表示：列出在 A 或 B 其中任一邊的  
  可以加上 `--left-right` 來顯示 commit 屬於哪一邊。

參考資料：[Git - Revision Selection](https://git-scm.com/book/en/v2/Git-Tools-Revision-Selection)
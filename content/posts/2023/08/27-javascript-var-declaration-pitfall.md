---
title: "踩到 JavaScript var 變數的雷"
slug: javascript-var-declaration-pitfall
date: 2023-08-27T02:29:05+08:00
series: 移植 Password Hasher Plus
tags: ["JavaScript"]
summary: 'tldr; 把 `var` 變數都換成 `let` 才發現原本的 test case 是跑心酸的。'
---

最近又開始把以前移植到一半的 Password Hahser Plus[^1] 撿起來繼續做。

因為先不想煩惱最終的 UI 形式，所以決定先把介面相關的部分拔掉、換成比較新的 JavaScript 語法（或是 TypeScript）。再來看要如何整理核心邏輯。

一開始當然就是處理一些瑣事，像是：
- 把 module 之間的相依從原本一堆 HTML 裡面的 `<script>` tag 換成 `require(...)`
- 用 ESlint + Prettier 整理原始碼的格式
- 測試套件從 Mocha + Chai 換成 Jest

本來以為只是無害的格式整理，結果原本的 test case 壞了好幾個。追了幾個小時才發現是原作者踩到用 `var` 宣告變數的雷。

原作者的 test case 寫法是：

```js
for (i = 1; i <= 24; ++i) {
  it('generates ' + i + ' digit(s)', function () {
    const result = generate(i, DIGITS);

    // ... [skiped]

    expect(result).toMatch(/* ... [skiped] ... */);
  });

  // ... [skiped]
}
```
用迴圈列舉不同 output 長度的 test case。

但因為 `var` 變數的作用範圍（scope）是 function，所以其實每個 test case 都是測試 `i = 25` 的狀況。我改成 `let` 之後反而讓其實不應該 pass 的 test 都浮了出來。

現在幾乎都用 `const` 或是 `let`，已經很少會踩到這個雷了。特此為記，順便累積一點寫部落格的手感。

[^1]: Source code: https://github.com/ericwoodruff/passwordhasherplus


---
title: Prettier + ESLint
slug: use-prettier-with-eslint
date: 2018-11-09T09:50:59.510Z
tags:
  - ESLint
  - Prettier
  - JavaScript
---

*   [ESLint](https://eslint.org/) — 程式碼檢查工具，包含排版風格與潛在問題
*   [Prettier](https://prettier.io/) — 支援多種語言的格式化工具

這篇不做個別介紹，只是整理一下兩個工具一起使用時的一些小細節。

## 方式 1：完全採用 Prettier 的排版規則

1.  安裝 [eslint-config-prettier](https://github.com/prettier/eslint-config-prettier)：關掉跟 Prettier 衝突或是不需要的規則。
2.  安裝 [eslint-plugin-prettier](https://github.com/prettier/eslint-plugin-prettier)：新增 `prettier/prettier` 規則。讓 ESLint 以 Prettier 排版結果為基準，指出需要修正的地方。

需要的 `.eslintrc.json` 設定如下：

```json
{  
  "extends": ["prettier"],  // use elsint-config-prettier  
  "plugins": ["prettier"],  // use eslint-plugin-prettier  
  "rules": {  
    "prettier/prettier": "error"  // from elsint-plugin-prettier  
  }  
}
```
或是等效簡短版：

```json
{  
  "extends": ["plugin:prettier/recommended"]  
}
```

然後透過執行 `prettier` 或是 `eslint --fix` 來調整排版，都有一樣效果。

## 方式 2：執行 Prettier 後，再以 ESLint 規則調整格式

好處：可以覆寫或客製化更有彈性的 Prettier 設定

1.  **不要** 使用 eslint-plugin-prettier
2.  _可_ 使用 eslint-config-prettier 
3. 在 `.eslintrc.json` 加上修正格式的規則

執行 `prettier` 後再執行 `eslint --fix`（或是改用 [prettier-eslint-cli](https://www.npmjs.com/package/prettier-eslint-cli) 一次搞定）。
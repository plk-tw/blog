---
title: 升級 npm 內附的 node-gyp
date: '2020-01-04T02:33:14.454Z'
slug: upgrade-node-gyp-bundled-in-npm
summary: 紀錄在 macOS 下用 asdf-nodejs 遇到的 Python 3、node-gyp 的坑。
tags: ['JavaScript', 'npm', 'node-gyp']
---

目前 npm (6.13.14) 用的 node-gyp (5.0.5) 在 macOS + Python 3 的環境會踩到這個 [bug](https://github.com/nodejs/node-gyp/issues/1917)：

> **TypeError: '>=' not supported between instances of 'tuple' and 'str'**

必須自己升級 npm 底下的 node-gyp。

一般狀況下，參考 [https://github.com/nodejs/node-gyp/wiki/Updating-npm's-bundled-node-gyp](https://github.com/nodejs/node-gyp/wiki/Updating-npm%27s-bundled-node-gyp) 跑下面這行指令就好了

```shell
npm explore npm -g -- npm install node-gyp@latest
```

但如果你剛好跟我一樣：1）用 asdf-vm 、2）用 yarn、3）升級過 npm，那就得改成：

```shell
cd $(asdf where nodejs)/lib/node_modules/npm
npm install node-gyp@latest
```

原因如下：

1.  yarn 只會在 Node.js 內附的 npm 路徑底下找 node-gyp
2.  asdf-nodejs 會設定 `NPM_CONFIG_PREFIX`，所以更新的 npm 不會蓋掉原先附的。
3.  而 npm explore 處理的是更新過的 npm

總之就是個踩坑紀錄……
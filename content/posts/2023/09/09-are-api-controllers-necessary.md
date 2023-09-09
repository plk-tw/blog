---
title: "API 一定要有 controller 嗎？"
date: 2023-09-09T20:35:46+08:00
slug: "are-api-controllers-necessary"
tags:
  - "MVC"
  - "Clean Architecture"
  - "Hexagonal Architecture"
---

今天在 YouTube 看了 [Fix Your Controllers By Refactoring To Minimal APIs](https://youtu.be/gsAuFIhXz3g) 然後被推薦 [Goodbye controllers, hello Minimal APIs - Nick Chapsas - NDC London 2023](https://youtu.be/pYl_jnqlXu8?t=1862)。後者提出一個觀點——「API controller 是個奇怪的存在」。

<!--more-->

## Class-based 的 controller 有什麼問題？

_（這節是對影片內容的摘要）_

「Controller」這個詞來自 [MVC (Model–view–controller) pattern](https://en.wikipedia.org/wiki/Model–view–controller)。但現在流行前後端分離，純提供 API 的 Web application 已經很少有 view 了，而 model 也更像是 client-server 之間的 protocol/contract。（註：這裡的 model 不是 ORM model 或 domain entity）。雖然說是「MVC」，但其實只有「C」。

Controller 之間的 (action) methods 很少互動、也不像其他 class 的 public method 會被「搭配使用」，每次的 request 只會呼叫單一 action method。除了 injected dependencies 幾乎不共享資料（state） 或 private methods。

而且，controller class 完全違反常見的 OO 原則，例如 Single-responsibility Principle、Open-closed principle。

大家繼續用 API controller 單純因為 framework （註：這裡說的是 .Net 生態系）只提供這種方式。

### 其他語言、框架的做法

開頭提到的兩支影片都是在介紹 .Net 界的 Minimal API。簡略地說就是 Django 的 view functions （相對於 class-based views）。Node.js 的基礎 web framework，例如 Express、Koa、Fastify 也都是這種架構，然後（其他 framework）再往上套 OO、controller class 的概念。

對其他語言的生態系比較沒這麼熟悉，就我所知，Ruby 的 Sinatra、Python 的 FastAPI 也是這種以 function 而非 controller (class) 為單位的架構。

## 個人經驗與感想

剛好最近團隊在推行 Clean Architecture（具體來說是 Hexagonal / Ports & Adapters) 。寫得愈多，也愈覺得 class-based controller 是個很累贅的概念——

當我習慣把 driving ports (queries/use cases) 切小、儘量只針對單一情境，controller 就得持有多而小的 dependencies，讓測試、修改都變得麻煩。例如要測試「修改密碼」的功能，我還是要生出 createUserUseCase、listUsersQuery、…… 的 mock，才能產生要測試的 controller 的 instance。如果今天多了一個新的 use case，原本該 controller 的所有 test case 都要加入一個新的（但用不到的 mock）。

於是我又開始考慮把 controller 切開、變小。到最後 controller 就只是特定 function 的一層薄薄包裝、為了讓 framework 可以注入 dependency。那這個 class 存在的意義到底何在？

進一步想：如果一路簡化（切小）下去，port/adapters、controller、use-case、repository 變成只是一層層的轉發，那這類架構的複雜分層是否弊大於利、不再有必要？是不是因為限在 OO 的思維下才需要 Clean Architecture、Ports & Adapters 這種架構？ 🤔
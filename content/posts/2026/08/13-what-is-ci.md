---
title: 何謂持續整合（Continuous Integration）？
date: 2026-08-13T13:43:22+08:00
slug: what-is-ci
summary: 在 FB DevOps Taiwan 社團看到，關於什麼是 CI 的 Twitter 討論串
tags:
  - CI
---

在 Facebook [DevOps Taiwan](https://www.facebook.com/groups/DevOpsTaiwan/permalink/2021691151251254/) 社團看到的 ~~Twitter~~ X 討論串：

1.  GitHub [說](https://x.com/github/status/1086354040429129728)：
  > 快來看怎麼用 GitHub 搭配 CircleCI/TravisCI 做 CI 的教學
2.  Nat Pryce [回](https://x.com/natpryce/status/1086358512043737089)：
  > 用 PR 做 CI，這樣一點都不持續（continuous）啊
3.  Martin Fowler [跳出來](https://x.com/martinfowler/status/1086642940653522944)：
  > 沒錯！CI 的基本就是每天推 code 進 master 啊
    [https://martinfowler.com/bliki/ContinuousIntegrationCertification.html](https://martinfowler.com/bliki/ContinuousIntegrationCertification.html)
4.  Christoph Sturm [反駁](https://x.com/globalo/status/1086646589396054016)：
  > 只要常常 rebase、不要開太久，有沒有合併進 master 沒差啊
5.  Martin Fowler 直接[丟定義](https://x.com/martinfowler/status/1086648144958492673)：
  > 我們可以討論 CI 好不好，但不要跟我吵 CI 的定義。  
  > CI 打從一開始就說是要 **每天推 code 進 master** 啊！
  > [https://martinfowler.com/articles/continuousIntegration.html](https://martinfowler.com/articles/continuousIntegration.html)

## 延伸閱讀
- [Enabling Trunk Based Development with Deployment Pipelines](https://www.thoughtworks.com/insights/blog/enabling-trunk-based-development-deployment-pipelines)
- [Continuous Integration - That's Not What They Meant](https://www.youtube.com/watch?v=97qyNQz7fxY)

----

## 後記

這篇在草稿區擺很久，擺到 [Twitter](https://twitter.com) 都變成 [X](https://x.com) 了。但現在看也不算過時，決定把它發一發。以後也比較好找。

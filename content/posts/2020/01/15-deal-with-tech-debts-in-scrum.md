---
title: 如何在 Scrum 裡處理技術債
date: '2020-01-15T07:30:54.832Z'
slug: deal-with-tech-debts-in-scrum
summary: 把 Twitter 上推友對這個問題的回應整理成文。
tags: ['Scrum']
---

在 Twitter 上問了[這個問題](https://twitter.com/WanCW/status/1217032648394072064)：
> #萬事問推友 各位跑 Scrum 的工程師推友，貴團隊如何在 sprint 中安排大規模重構或各種償還技術債的 task？

把推友的回應整理如下，具體討論可以看上面的連結或是 [Treeverse 整理的結果](https://treeverse.app/view/RWFE8jdz)

### 如何形成 task

依修正幅度小到大：

1.  在既有的 task 中一併處理 → 把時間估長一點
2.  開單獨的 task 排進 backlog，如同其他 story task
3.  規模太大的話可以考慮切成單獨的獨立 project

### 如何在 sprint 中安排 tech-only task

1.  找 feature 比較少、較鬆的 sprint 再拉進來做
2.  或是每個 sprint 留一定比例給這類 task
3.  也可以如同一般 story task，丟進 backlog 後由 PO 決定順序  
    （要讓 PO 了解技術債的影響，例如：造成往後 feature task 的時間、點數上升）

### 策略、心態

1.  從商業角度來看，每個 sprint 的重點還是要依 PO、stackholder 預期產出功能
2.  要能量化修技術債、重構的成果，以說服 PO、stakeholder

### 相關技術

*   如果不是短期可以完成的修改，可以考慮採用 [Strangler](https://docs.microsoft.com/en-us/azure/architecture/patterns/strangler) 或相關 pattern
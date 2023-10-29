---
title: "用 TypeScript 寫 Jest 的 matcher"
slug: custom-jest-matcher-using-typescript
date: 2023-10-29T15:13:07+08:00
tags:
  - "TypeScript"
  - "Jest"
summary: "官方給的範例沒辦法把 matcher 加到 Matcher interface"
---

一開始依照 [Jest 官方文件](https://jestjs.io/docs/expect#expectextendmatchers) 的寫法：

```typescript
// 省略實際 function 實作跟 `expect.extend(...)`

declare module 'expect' {
  interface Matchers<R> {
    toBeCustomValid(/*...*/): R;
  }
}
```

但還是出現 `... 'toBeCustomValid' does not exist on type 'JestMatchers<...` 的錯誤。

後來參考 [jest-extended](https://github.com/jest-community/jest-extended/blob/main/types/index.d.ts#L429) 的寫法：
```typescript
declare namespace jest {
  interface Matchers<R> {
    toBeCustomValid(/*...*/): R;
  }
}
```

把 matcher function 加到 `jest.Matchers`（而不是 `expect.Matchers`）底下就搞定了。

----

_註： Jest 版本是 29.6.4_

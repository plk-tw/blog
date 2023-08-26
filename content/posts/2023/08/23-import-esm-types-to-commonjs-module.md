---
title: "在 CommonJS module 中使用 ESM 型別"
slug: 'import-esm-types-to-commonjs-module'
date: 2023-08-23T02:07:26+08:00
tags: ["ESM", "CommonJS", "JavaScript", "TypeScript"]
---

要在 CommonJS module 中使用 ESM 必須透過[動態 import](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/import)；但型別是編譯時期的資訊，一定要用靜態 import。透過*宣告檔案*（Declaration File）可以解決這個問題。

首先加一個 `.d.ts` 重新 export 你用到的 type：

```typescript
// type-wrapper.d.ts
export type { SomeType } from 'some-esm-package';
// ...
```

這樣你就可以如同使用其他 CommonJS 一樣 import 它；實際使用到物件/值的地方還是得需要 dynamic import：

```typescript
// your .ts source file
import type { SomeType } from './type-wrapper'


// ...
    const module = await import('some-esm-package');
    const { someValue } = module;
// ...
```


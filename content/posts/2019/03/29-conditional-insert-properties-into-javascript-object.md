---
title: JavaScript 有條件增加物件屬性的簡短寫法
date: '2019-03-29T02:17:37.844Z'
slug: conditional-insert-properties-into-javascript-object
summary: "`const obj = {...condition && { prop: value } };`"
tags: ['JavaScript']
---

從 [The shortest way to conditional insert properties into an object literal](https://dev.to/jfet97/the-shortest-way-to-conditional-insert-properties-into-an-object-literal-4ag7) 看到的。

例如，為了避免出現 undefined 的 property ，通常會這樣寫：

```js
const obj = {};  
if (input1) {  
    obj.prop1 = input1;  
}  
if (input2) {  
    obj.prop2 = input2;  
}
```

可以寫成：

```js
const obj = {  
    ...input1 && { prop1: input1 },  
    ...input2 && { prop2: input2 }, 
};
```

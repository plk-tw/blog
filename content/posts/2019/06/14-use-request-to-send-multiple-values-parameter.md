---
title: '用 request 送出同名多值的 query 參數'
date: '2019-06-14T07:49:28.054Z'
slug: use-request-to-send-multiple-values-parameter
summary: tldr; 在 options 裡設定 useQuerystring 或是 qsStringifyOptions 的 arrayFormat
tags: ['JavaScript']
---

以 form POST 為例，一般寫法：

```js
request.post({  
    url: ...,  
    form: {  
        paramKey: [ 'value 1', 'value 2' ],  
    }  
}, (error, response, body) => { ... });
```

會送出這樣的 request body（key 後面加上 `[0]`、`[1]`、……）：

```
paramKey%5B0%5D=value+1&paramKey%5B1%5D=value+2
```

如果想像這樣重複送出同樣的 key：

```
paramKey=value+1&paramKey=value+2
```

可以

```js
request.post({  
    url: ...,  
    form: {  
        paramKey: [ 'value 1', 'value 2' ],  
    },  
  
    // 改用內建的 querystring 模組  
    useQueryString: true,    

}, (error, response, body) => { ... });
```

或是：

```js
request.post({  
    url: ...,  
    form: {  
        paramKey: [ 'value 1', 'value 2' ],  
    },

    // 指定給 qs 的參數  
    qsStringifyOptions: {  
        arrayFormat: 'repeat',  
    },

}, (error, response, body) => { ... });
```
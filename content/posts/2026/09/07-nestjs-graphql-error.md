---
title: "NestJS 的 GraphQL Error"
date: 2026-09-07T07:07:24+08:00
slug: "nestjs-graphql-error"
summary: "NestJS + Apollo driver 的 error response 產生過程"
tags:
  - GraphQL
  - NestJS
---

筆記一下 [NestJS （搭配 Apollo）](https://docs.nestjs.com/graphql) 是怎麼把內部丟出的 exception 轉換成 GraphQL 的 error response。

## 標準步驟

### 階段 1. Apollo server

- 如果 exception 不是 `GraphQLError`，會先將 resolver 丟出的 exception 包裝在 `GraphQLError` 的 `originalError` 裡面。
- 取用（轉換後的）`GraphQLError.extensions` 的 `code` 和 `http` ，產出第一階段的 error response (`GraphQLFormattedError`)：
  - 如果沒有 `code`，會使用 `INTERNAL_SERVER_ERROR` 作為預設值
  - `http` 如果有 `status`，必須是數字，會影響 HTTP 回應的狀態碼
  - `http` 如果有 `headers`，必須是 `Map` 物件
- 將 `GraphQLFormattedError` 丟給 `formatError` 選項，產出新的 error response

### 階段 2. NestJS Apollo driver

_（透過 Apollo server 的 `formatError` 選項改寫 error response）_

- 如果拿到的 `GraphQLError.originalError` 不是 NestJS 的 `HttpException`，不做改寫；
- 改寫方式：
  - 將原本 HttpExcpetion 的 `.response` 塞在 output 的 `.extensions.originalError` 欄位
  - 如果 `HttpException` 是 400、401、403 之一，會修改 `.extensions.code` 為對應的值；
    ```json
    {
      "code": "BAD_REQUEST"
    }
    ```
    如果不是，則保留 `INTERNAL_SERVER_ERROR` 作為預設值，新增 `.extensions.status` 欄位來表示 HTTP 狀態碼
    ```json
    {
      "code": "INTERNAL_SERVER_ERROR",
      "status": 404
    }
    ```

## 客製化方法

1. 想要改寫 HTTP status / header：
   丟出 `GraphQLError`，在 `extensions` 裡面新增 `http` 欄位

2. 只有要改寫 error response 的內容：
   透過 GraphQLModule 的 `formatError` 選項

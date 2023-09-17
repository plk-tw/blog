---
title: "用 OpenSSL 產生金鑰對"
slug: generate-key-pair-using-openssl
date: 2023-09-18T03:03:58+08:00
tags:
  - "OpenSSL"
---

手上的專案用 RSA256 做為 JWT 的簽章驗證方式，需要針對不同環境產生不同的金鑰對（key pair）。撰寫文件時發現網路上找到的方法通常都是用 `ssh-keygen(1)` 搭配 `openssl(1)`，但其實光用 `openssl(1)` 就足以產生 private key 與 public key。

<!--more-->

## 產生 private key

如果要產生 2048 bits 的 RSA private key，並寫入檔案 `private_key.pem`：

```shell
$ openssl genpkey -algorithm RSA -pkeyopt rsa_keygen_bits:2048 -out private_key.pem
```

## 從 RSA private key 產生 public key

將 private key 檔案 `private_key.pem` 對應的 public key 寫入檔案 `publickey_key.pem`：

```shell
$ openssl rsa -pubout -in private_key.pem -out public_key.pem
```

## 參考資料

1. [Cryptography/Generate a keypair using OpenSSL - Wikibooks](https://en.wikibooks.org/wiki/Cryptography/Generate_a_keypair_using_OpenSSL)
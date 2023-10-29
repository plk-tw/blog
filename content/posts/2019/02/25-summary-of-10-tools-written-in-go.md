---
title: 10 套用 Go 寫的開發者工具
date: '2019-02-25T07:16:10.281Z'
slug: summary-of-10-tools-written-in-go
tags: [Go]
---

簡單整理一下 [10 tools written in Go that every developer needs to know](https://golang.works-hub.com/learn/10-tools-written-in-go-that-every-developer-needs-to-know-6d45d)，當作自己的備忘。

<!--more-->

1.  Caddy - [https://caddyserver.com](https://caddyserver.com)  
    輕量的 HTTP/2 web server，透過 Let’s Encrypt 自動配置 HTTPS。
2.  Ngrok - [https://ngrok.com](https://ngrok.com)  
    幫本地 server 提供公開端點，支援 HTTP、HTTPS → HTTP、non-HTTP over TLS、TCP。不過是要註冊、收費的服務。
3.  ctop - [https://ctop.sh/](https://ctop.sh/)  
    類似 [top](https://en.wikipedia.org/wiki/Top_%28software%29)，用來看 container 狀態的 TUI 工具。
4.  GoTTY - [https://github.com/yudai/gotty](https://github.com/yudai/gotty)  
    把 CLI/TUI 轉變成 web application。（這感覺超危險的啊……
5.  Mattermost (server) - [https://mattermost.com](https://mattermost.com)  
    開源的 Slack 替代方案。前陣子發現 GitLab 的 Omnibus [有把 Mattermost 包進去](https://docs.gitlab.com/omnibus/gitlab-mattermost/)。
6.  Minio - [https://minio.io](https://minio.io)  
    提供相容於 AWS S3 API 的開源替代品，也可以當 gateway 後面接 Google Cloud Storage、Azure Blob Storage、NAS。
7.  Piknik - [https://github.com/jedisct1/piknik](https://github.com/jedisct1/piknik)  
    跨裝置的加密「剪貼簿」
8.  Pgweb - [https://sosedoff.github.io/pgweb](https://sosedoff.github.io/pgweb)  
    PostgreSQL 的 Web 介面
9.  pRest - [https://postgres.rest](https://postgres.rest)  
    把 SQL 資料庫包裝成 RESTful API，目前只支援 PostgreSQL、MySQL 開發中。（想不到這樣做有什麼好處……
10.  Terraform - [https://www.terraform.io](https://www.terraform.io)  
    無需多言，知名的 Infrastructure-as-Code 工具。
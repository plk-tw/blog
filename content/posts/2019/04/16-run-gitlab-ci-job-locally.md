---
title: 在本地端跑 GitLab CI job
date: '2019-04-16T08:57:26.972Z'
slug: run-gitlab-ci-job-locally
summary: "gitlab-runner 可以直接在本地端跑 `.gitlab-ci.yml` 中定義的 job；但得給不少 command line 參數，記錄一些常用的。"
tags: ['GitLab']
---

[gitlab-runner](https://docs.gitlab.com/runner/) 可以直接在本地端跑 `.gitlab-ci.yml` 中定義的 job；但比較麻煩的是它不會讀 `config.toml`，所以得給不少 command line 參數。

記錄一下方便以後找：

## docker-in-docker

```shell
gitlab-runner exec docker <job_name> \  
    --docker-volumes /var/run/docker.sock:/var/run/docker.sock
```

## 設定 job 的環境變數

```shell
gitlab-runner exec shell <job_name> \  
    --env "ENV_VAR_1=value1" \  
    --env "ENV_VAR_2=value2"
```

## 後記

其實這些命令列參數也都可以透過對應的環境變數；但是不支援多值，上面兩個情境就不太適合。
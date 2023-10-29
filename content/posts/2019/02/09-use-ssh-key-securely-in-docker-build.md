---
title: Docker build 不留下 SSH private key
date: '2019-02-09T01:36:00.797Z'
slug: use-ssh-key-securely-in-docker-build
summary: >-
  我以前是用 dockito/vault；Docker 17.05 後可以使用 multi-stage、Docker 18.09 後則可以使用
  BuildKit 的 SSH mount type。
tags:
  - Docker
  - SSH
---

我以前是用 [dockito/vault](https://github.com/dockito/vault)、Docker 17.05 後可以使用 multi-stage。  
Docker 18.09 後則可以使用 BuildKit 的 SSH mount type：

**Dockerfile**

這行加在 Dockerfile 最前面：

```Dockerfile
# syntax=docker/dockerfile:1.0.0-experimental
```

在需要用到 SSH private key 的地方加上 `--mount=type=ssh`

```Dockerfile
# 使用預設的 id 為 "default"  
RUN --mount=type=ssh do_something
```

**執行 docker build**

```shell
export DOCKER\_BUILDKIT=1  
docker build --ssh default=/path/to/ssh/private/key
```

----

*   參考資料：[https://medium.com/@amimahloof/securely-build-small-python-docker-image-from-private-git-repos-c3e6d5da4626](https://medium.com/@amimahloof/securely-build-small-python-docker-image-from-private-git-repos-c3e6d5da4626)
*   也能指定不同的 id 給 SSH key，細節可參考 [BuildKit 的文件](https://github.com/moby/buildkit/blob/master/frontend/dockerfile/docs/experimental.md#run---mounttypessh)。
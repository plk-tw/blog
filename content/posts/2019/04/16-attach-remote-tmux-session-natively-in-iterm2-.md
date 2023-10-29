---
title: iTerm2 + SSH + tmux
date: '2019-04-16T03:34:58.304Z'
slug: attach-remote-tmux-session-natively-in-iterm2
summary: 記錄 iTerm2 連上 SSH server 後直接操作遠端 tmux session 的方法
tags: ['iTerm2', 'tmux', 'SSH']
---

[iTerm2](https://www.iterm2.com/documentation-tmux-integration.html) 可以作為 tmux [control mode](http://man7.org/linux/man-pages/man1/tmux.1.html#CONTROL_MODE) 的 client，只要：

```shell
tmux -CC [new|attatch|..]
```

就可以用原生介面操作 tmux 的 window、pane。

## 遠端 session

因為是透過 terminal 文字溝通，所以也適用遠端的 tmux session。

通常會連上遠端機器後立刻執行 `tmux -CC ...`，或是乾脆用 command line 參數直接跑。但還是覺得有點麻煩，就在 `ssh_config` 加了一個 host alias：

```
Host terminus-tmux  
  Hostname 192.168.1.42  
  RequestTTY yes  
  RemoteCommand tmux ls | grep -vq attached && tmux -CC a || tmux -CC new
```

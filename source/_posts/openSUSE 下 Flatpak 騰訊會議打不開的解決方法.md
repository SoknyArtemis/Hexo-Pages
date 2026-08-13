---
title: OpenSUSE 下 Flatpak 騰訊會議打不開的解決方法
author: 星華輝月
categories: 操作系統
tags:
  - 安全
  - Linux
  - SELinux
  - openSUSE
  - Flatpak
abbrlink: '7684'
date: 2026-07-02 13:00:00
---

開會這一塊，騰訊會議是必備的，雖然騰訊會議也有官方的 linux 版本，但是哪個是 .deb 包，筆者的 suse 不支持 .deb，我也不是很想用 alien 轉換，所以就安裝了打包成 flatpak 的版本

但是 flatpak 包打不開，每次啓動轉圈轉一會兒就沒動靜了，查閱資料發現，原來是 OpenSUSE 的 SELinux 很嚴格，需要使用 `sudo setsebool -P selinuxuser_execstack 1` 關掉這個規則。

執行：

```
sudo setsebool -P selinuxuser_execstack 1
```

再打開騰訊會議，就可以了

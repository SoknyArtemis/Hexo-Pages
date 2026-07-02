---
title: OpenSUSE 下 Flatpak 的騰訊會議打不開的解決方法
author: 星華輝月
categories: 操作系統
tags:
  - 安全
  - Linux
  - OpenSUSE
  - Flatpak
abbrlink: b62e
---

開會這一塊，騰訊會議是必備的，雖然騰訊會議也有官方的 linux 版本，但是哪個是 .deb 包，筆者的 suse 不支持 .deb，我也不是很想用 alien 轉換，所以就安裝了打包成 flatpak 的版本

但是 flatpak 包打不開，每次啓動轉圈轉一會兒就沒動靜了，查閱資料發現，原來是 OpenSUSE 的 SELinux 很嚴格，需要使用 `sudo setsebool -P selinuxuser_execstack 1` 關掉這個規則。

關掉之後測試，確實可以成功運行，但是直接關的話顯然不符合「權限最小化原則」，要找一些別的辦法

搜索發現可以使用 `asusearch` 非常方便地直接抓取拒絕記錄，並生成可供使用的策略規則


```
# 抓取拒絕記錄並生成策略規則模塊
sudo ausearch -m avc -ts recent | audit2allow -M wemeet_fix
```

然後編譯安裝這個模塊：

```
sudo semodule -i wemeet_fix.pp
```

重新啓動騰訊會議，就可以啓動成功了！

*記得回退之前爲了測試改變的規則 （如果沒有更改過，請忽略）:*

```
sudo setsebool -P selinuxuser_execstack 0
```




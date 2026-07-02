---
title: 一些 Linux 發行版中， fcitx5 + rime 漢字輸入會錯誤地顯示拼音的解决方法
author: 星華輝月
categories: 操作系統
tags:
  - Linux
  - OpenSUSE
  - Rime
  - 輸入法
abbrlink: 258b
---

筆者在使用 OpenSUSE，fcitx5 + rime 時遇到了一個汉字模式下，输入框会顯示拼音的問題。

经过搜索找到了一篇 Issue：  [ 最新版本的错音错字提示强制显示拼音，可能影响输入体验](https://github.com/iDvel/rime-ice/issues/431)
按照評論區的說法，是 `librime` 包太舊了或者不匹配，導致 lua 腳本跑不了，正常能夠使用 lua 腳本的話，是不顯示拼音的。
librime 在大多數發行版應該是在安裝 `fcitx5-rime` 的時候就自動安裝進去了，但是在 NixOS 等發行版（比如筆者的 SUSE）中並不會打包進去。跑不了腳本就導致這樣了。

筆者運行：

```
zypper in librime*
```

後，成功地找到了一堆 「librime」打頭的包，安裝後重新部署：

```
fcitx5 -r
```

成功解决！

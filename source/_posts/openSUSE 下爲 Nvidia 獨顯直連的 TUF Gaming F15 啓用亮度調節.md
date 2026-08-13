---
title: openSUSE 下爲獨顯直連的 TUF Gaming F15 啓用亮度調節
author: 星華輝月
categories: 操作系統
tags:
  - Linux
  - openSUSE
  - Nvidia
abbrlink: 7f87
excerpt: 在大部分環境，似乎只需啓用 acpi_backlight=native 就可以啓用亮度調節，但是在 openSUSE 下...
---

在大部分環境，似乎只需啓用 `acpi_backlight=native` 就可以啓用亮度調節，
但是在 openSUSE 下，必須同時啓用這三個參數，才能成功開啓：


```
nvidia.NVreg_EnableBacklightHandler=1 nvidia.NVreg_RegistryDwords=EnableBrightnessControl=1
acpi_backlight=native
```

如果是 systemd-bootloader ，就在 `/etc/kernel/cmdline` 中編譯好，使用 `sudo update-bootloader --refresh` 更新即可。

注意：不需要使用 `echo "blacklist nvidia_wmi_ec_backlight" | sudo tee /etc/modprobe.d/disable-nvidia-wmi.conf` 屏蔽，只要加上這三個參數就好

*附上我的配置供參考：*

- **系統：** openSUSE Tumbleweed x86_64 (20260809)
- **主機：** ASUS TUF Gaming F15 FX507VU_FX507VU (1.0)
- **內核：** Linux 7.1.7-1-default
- **顯卡：** NVIDIA GeForce RTX 4050 Max-Q / Mobile
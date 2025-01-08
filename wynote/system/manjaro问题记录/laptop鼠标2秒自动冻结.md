cd /etc/laptop-mode/conf.d
sudo vim runtime-pm.conf
slociv@gg ~> lsusb
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 001 Device 002: ID 8087:0a2b Intel Corp. Bluetooth wireless interface
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 003 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 003 Device 002: ID 0408:1020 Quanta Computer, Inc. hm1091_techfront
Bus 003 Device 005: ID 093a:2510 Pixart Imaging, Inc. Optical Mouse  这个就是mouse
Bus 004 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub

AUTOSUSPEND_RUNTIME_DEVID_BLACKLIST="275d:0ba6 093a:2510"


sudo systemctl restart laptop-mode.service


从你的 `99-laptop-mode.rules` 文件来看，文件中定义了一些规则来管理电源供应和 USB 子系统的行为。为了确保 USB 自动暂停功能正常工作，你需要将规则调整为使用 `Runtime-pm` 模块而不是 `usb-autosuspend`。你可以修改文件如下：

bash

```
ACTION=="change", SUBSYSTEM=="power_supply", ENV{POWER_SUPPLY_NAME}=="|AC|ACAD|ADP*", RUN+="lmt-udev auto"
ACTION=="add|remove", SUBSYSTEM=="machinecheck", RUN+="lmt-udev auto"
ACTION=="add", SUBSYSTEM=="usb", RUN+="lmt-udev force modules=runtime-pm devices=%k"
```

这样，在 `SUBSYSTEM` 为 `usb` 的情况下，将 `usb-autosuspend` 替换为 `Runtime-pm` 模块。这将确保 USB 设备能够按照 `runtime-pm.conf` 文件中的设置进行自动暂停和恢复。

此外，在你的 `/etc/laptop-mode/conf.d/runtime-pm.conf` 文件中，你可以添加 USB 设备的黑名单来防止它们进入自动暂停状态。例如，如果你想将 USB 鼠标添加到黑名单，可以这样做：
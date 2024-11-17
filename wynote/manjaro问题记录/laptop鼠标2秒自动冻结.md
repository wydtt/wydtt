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


sudo systemctl restart laptop-mode-tools
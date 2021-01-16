# qBittorrent-openwrt-package
Openwrt package Makefiles for qBittorrent and its dependencies (libtorrent-rasterbar and qt5, libtorrent-rasterbar is named as rblibtorrent).

## How to use:
* Use `git` to clone the sources into your openwrt sources package directory (`OPENWRT_SRC_ROOT/package`):
```
git clone gitURL OPENWRT_SRC_ROOT/package/<dir_name>
```
You can change <dir_name> to any directory name you like.
* Select the packages in menuconfig:
```
cd OPENWRT_SRC_ROOT
make menuconfig
```
You can see the qt5 library packages in `Libraries --> Qt5`, the rblibtorrent (libtorrent-rasterbar) package in `Libraries --> rblibtorrent`, and the qBittorrent package in `Network --> BitTorrent --> qBittorrent`.
* At last, Build your own openwrt images and packages as usual.

After run qBittorrent will appear on 8080 port. login:admin password:adminadmin.

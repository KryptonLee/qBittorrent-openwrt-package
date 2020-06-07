# qBittorrent-openwrt-package
Openwrt package Makefiles for qBittorrent and its dependencies (libtorrent-rasterbar and qt5, libtorrent-rasterbar is named as rblibtorrent).

## How to use:
* Use `git` to clone the sources into your openwrt sources package directory (`OPENWRT_SRC_ROOT/package`):
```
git clone https://github.com/KryptonLee/qBittorrent-openwrt-package.git OPENWRT_SRC_ROOT/package/<dir_name>
```
You can change <dir_name> to any directory name you like.
* Select the packages in menuconfig:
```
cd OPENWRT_SRC_ROOT
make menuconfig
```
You can see the qt5 library packages in `Libraries --> Qt5`, the rblibtorrent (libtorrent-rasterbar) package in `Libraries --> rblibtorrent`, and the qBittorrent package in `Network --> BitTorrent --> qBittorrent`.
* At last, Build your own openwrt images and packages as usual.
## Tested platform:
* x86 and x64
* Newifi D2 (mipsel_24kc)
<br>Other platforms have not been tested. I am not sure qt5 could function properly on them, as some platforms may need to add additional flags to `QMAKE_CFLAGS` and `QMAKE_CXXFLAGS` in files `qmake.conf`.

# qBittorrent-openwrt-package
Openwrt package Makefiles for qBittorrent and its dependencies (libtorrent-rasterbar and qt5, libtorrent-rasterbar is named as rblibtorrent).

## branch introduction:
* `master` uses libtorrent-rasterbar in openwrt feeds of master branch and always keeps qBittorent up to date as soon as possible, but usually only works on the master branch of openwrt.
* `for-openwrt-21.02` uses the libtorrent-rasterbar package named as rblibtorrent rather than the libtorrent-rasterbar package in openwrt 21.02 feeds, as the version of the latter one stays at v2.0.1, which doesn't support qBittorrent v4.4.0 and above.
* `for-openwrt-19.07` uses libtorrent-rasterbar v1.2.X series, as the cmake version in openwrt 19.07 is too old to compile libtorrent-rasterbar v2.0.X.
* `for-openwrt-18.06` uses qBittorrent v4.3.1, libtorrent-rasterbar v1.2.12 and qt5 v5.14.2 as the final version that openwrt 18.06 can support.

## How to build:
* Use `git` to clone the sources into your openwrt sources package directory (`OPENWRT_SRC_ROOT/package`):
```
git clone https://github.com/KryptonLee/qBittorrent-openwrt-package.git OPENWRT_SRC_ROOT/package/<dir_name>
```
You can change <dir_name> to any directory name you like.
* List tag versions of this package:
```
cd OPENWRT_SRC_ROOT/package/<dir_name>
git tag
```
And get the sources of the specified tag version:
```
git checkout tag_name
```
* Select the packages in menuconfig:
```
cd OPENWRT_SRC_ROOT
make menuconfig
```
You can see the qt5 library packages in `Libraries --> Qt5`, the rblibtorrent (libtorrent-rasterbar) package in `Libraries --> rblibtorrent`, and the qBittorrent package in `Network --> BitTorrent --> qBittorrent`.
* Select package `Libraries --> boost` as `<*> built-in` or `<M> moudle`, otherwise libtorrent-rasterbar will miss dependency on boost-system, and it will fail to build the openwrt images, as the boost-system package will not be built unless boost package has been selected as `<*> built-in` or `<M> moudle`.
* At last, Build your own openwrt images and packages as usual.
## How to use after openwrt start-up:
* qBittorrent will run automatically after openwrt start-up. The WebUI runs on port `8080` with default username `admin` and password `adminadmin`. You can change username and password on WebUI setting page after login. By default, the WebUI only can be accessed from LAN side. If you want to access the WebUI from WAN side, you must create a rule in firewall for permitting incoming connections to this port from WAN side.
* The default save path for downloads is `/root/Downloads/`. You can change it on WebUI setting page. 
* Port 8999 is used for incoming connections by default. Of course you can change it on WebUI setting page. In order to reach a higher download speed, it is better to create a rule in firewall for permitting incoming connections to this port from WAN side.
## Tested platform:
* x86 and x64
<br>Other platforms have not been tested. I am not sure qt5 could function properly on them, as some platforms may need to add additional flags to `QMAKE_CFLAGS` and `QMAKE_CXXFLAGS` in files `qmake.conf`.

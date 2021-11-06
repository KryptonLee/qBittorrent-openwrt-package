# qBittorrent-openwrt-package
Openwrt package Makefiles for qBittorrent and its dependencies (libtorrent-rasterbar and qt5, libtorrent-rasterbar is named as rblibtorrent).

## Warning

You need install qt6 from there: https://www.qt.io/download-qt-installer

And set option -DQT_HOST_PATH in file qt6/makefile and qBittorrent/makefile.


```
## How to use:

1)git clone https://github.com/openwrt/openwrt

2)cd openwrt

3)./scripts/feeds update -a

4)./scripts/feeds install -a

5)cd package

6)git clone https://github.com/Deema35/qBittorrent-openwrt-package.git qBittorrent

6.1) cd ../

7)make menuconfig - set architecture and board and pick qbittorrent. QBittorrent package in `Network --> BitTorrent --> qBittorrent`.

8)make tools/install -jx

9)make toolchain/install -jx

10)make package/qBittorrent/compile -jx

-jx - number of CPU cores.

11)make package/index - create signature (key-build need put in openwrt folder)

## Generate keys for signature:

1)git clone https://git.openwrt.org/project/usign.git

2)cd usign

3)cmake .

4)make

5)usign -G -c 'openwrt test repo' -s key-build -p key-build.pub

6)ln -s "which usign" staging_dir/host/bin/usign

## Execute in router:

1)Copy .pub key to /etc/opkg/keys/ key need rename to signature ID in file Packages.sig

2)echo src/gz local file:///opt >> /etc/opkg/customfeeds.conf - Add local repository in folder /opt

3)Move file from folder bin/packages/archetecture to folder opt on router

4)opkg update

5)opkg install qbittorrent

After run qBittorrent will appear on 8080 port. login:admin password:adminadmin.



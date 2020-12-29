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


## After start

Fist you need create new user and user group:

In file: /etc/passwd add string : <code>qbittorrent:x:227:227:qbittorrent:/home/qbittorrent:/bin/false<code>

In file: /etc/group add string : <code>qbittorrent:x:227:qbittorrent<code>

In file: /etc/shadow add string : <code>qbittorrent:x:0:0:99999:7:::<code>

After that you need create home dir for user qbittorrent:

mkdir /home
mkdir /home/qbittorrent
chown qbittorrent:qbittorrent /home/qbittorrent
And then you need put this script to directory /etc/init.d

#! /bin/sh /etc/rc.common
USE_PROCD=1

START=98
STOP=01

DAEMON="/usr/bin/qbittorrent-nox"
USER="qbittorrent"
GROUP="qbittorrent"

start_service() {
	procd_open_instance
	procd_set_param command "$DAEMON"
	procd_set_param user $USER
	procd_set_param group $GROUP
	procd_set_param env HOME=/home/qbittorrent
	procd_close_instance
}
Allow execution:
chmod 755 /etc/init.d/qbittorrent

After run qBittorrent will appear on 8080 port. login:admin password:adminadmin.

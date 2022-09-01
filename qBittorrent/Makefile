#
# Copyright (C) 2020 Krypton Lee <jun.k.lee199410@outlook.com>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=qBittorrent
PKG_VERSION:=4.4.5
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/qbittorrent/qBittorrent/tar.gz/release-$(PKG_VERSION)?
PKG_HASH:=70c2128b44fe4df4dfc8afc765a304d70cf1b042b5214bcc855d8b3bbc9ccf36
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-release-$(PKG_VERSION)

PKG_MAINTAINER:=Krypton Lee <jun.k.lee199410@outlook.com>
PKG_LICENSE:=GPL-2.0+
PKG_LICENSE_FILES:=COPYING

PKG_BUILD_DEPENDS:=qt5tools
PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1
PKG_USE_MIPS16:=0

include $(INCLUDE_DIR)/package.mk

define Package/qBittorrent
  SUBMENU:=BitTorrent
  SECTION:=net
  CATEGORY:=Network
  TITLE:=BitTorrent Client Programmed in C++ / Qt
  URL:=https://www.qbittorrent.org/
  DEPENDS:=+libQt5Core +libQt5Network +libQt5Sql +libQt5Xml +rblibtorrent
endef

define Package/qBittorrent/description
qBittorrent is a bittorrent client programmed in C++ / Qt that uses 
libtorrent (sometimes called libtorrent-rasterbar) by Arvid Norberg.
It aims to be a good alternative to all other bittorrent clients out 
there. qBittorrent is fast, stable and provides unicode support as 
well as many features.
endef

CONFIGURE_VARS += \
	QT_QMAKE=$(STAGING_DIR_HOSTPKG)/bin \
	QMAKE_LRELEASE=$(STAGING_DIR_HOSTPKG)/bin/lrelease \
	PKG_CONFIG_PATH=$(STAGING_DIR)/usr/lib/pkgconfig

CONFIGURE_ARGS += \
	--disable-gui \
	--with-boost=$(STAGING_DIR)/usr

MAKE_VARS += \
	INSTALL_ROOT=$(PKG_INSTALL_DIR)

define Package/qBittorrent/install
	$(INSTALL_DIR) $(1)/usr/man/man1
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/man/man1/qbittorrent-nox.1 $(1)/usr/man/man1/qbittorrent-nox.1
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/qbittorrent-nox $(1)/usr/bin
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/qbittorrent $(1)/etc/init.d
	$(INSTALL_DIR) $(1)/.config/qBittorrent
	$(CP) ./files/qBittorrent.conf $(1)/.config/qBittorrent
	$(INSTALL_DIR) $(1)/root/Downloads
endef

$(eval $(call BuildPackage,qBittorrent))

#
# Copyright (C) 2020 Krypton Lee <jun.k.lee199410@outlook.com>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=qBittorrent
PKG_VERSION:=4.4.2
PKG_RELEASE:=2

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/qbittorrent/qBittorrent/tar.gz/release-$(PKG_VERSION)?
PKG_HASH:=f9406eb982a4b8a084341fb0bc30bd8b50babe5dcf4197204ab407b06e20e8a3
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-release-$(PKG_VERSION)

PKG_MAINTAINER:=Krypton Lee <jun.k.lee199410@outlook.com>
PKG_LICENSE:=GPL-2.0+
PKG_LICENSE_FILES:=COPYING

PKG_BUILD_DEPENDS:=qt6tools/host
PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1
PKG_USE_MIPS16:=0

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/qBittorrent
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=BitTorrent
  TITLE:=BitTorrent Client Programmed in C++ / Qt
  URL:=https://www.qbittorrent.org/
  DEPENDS:=+libQt6Core +libQt6Network +libQt6Sql +libQt6Xml +libtorrent-rasterbar +qt6-plugin-libqopensslbackend +qt6-plugin-libqsqlite
endef

define Package/qBittorrent/description
qBittorrent is a bittorrent client programmed in C++ / Qt that uses 
libtorrent (sometimes called libtorrent-rasterbar) by Arvid Norberg.
It aims to be a good alternative to all other bittorrent clients out 
there. qBittorrent is fast, stable and provides unicode support as 
well as many features.
endef

CMAKE_OPTIONS += \
	-DGUI=OFF \
	-DSTACKTRACE=OFF \
	-DQT6=ON \
	-DVERBOSE_CONFIGURE=ON \
	-DQT_ADDITIONAL_PACKAGES_PREFIX_PATH=$(STAGING_DIR_HOSTPKG)

define Package/qBittorrent/install
	$(INSTALL_DIR) $(1)/usr/share/man/man1
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/share/man/man1/qbittorrent-nox.1 $(1)/usr/share/man/man1/qbittorrent-nox.1
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/qbittorrent-nox $(1)/usr/bin
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/qbittorrent $(1)/etc/init.d
	$(INSTALL_DIR) $(1)/.config/qBittorrent
	$(CP) ./files/qBittorrent.conf $(1)/.config/qBittorrent
	$(INSTALL_DIR) $(1)/root/Downloads
endef

$(eval $(call BuildPackage,qBittorrent))


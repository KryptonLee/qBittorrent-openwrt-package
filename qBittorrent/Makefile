#
# Copyright (C) 2020 Krypton Lee <jun.k.lee199410@outlook.com>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=qBittorrent
PKG_VERSION:=4.4.0rc1
PKG_RELEASE=0

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/qbittorrent/qBittorrent/tar.gz/release-$(PKG_VERSION)?
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_HASH:=1cc48d0166e51a7f92ef6d25911970b277a244b6840ad8c7b07e6a22206d7803
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-release-$(PKG_VERSION)

PKG_MAINTAINER:=Krypton Lee <jun.k.lee199410@outlook.com>
PKG_LICENSE:=GPL-2.0+
PKG_LICENSE_FILES:=COPYING

PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1
PKG_USE_MIPS16:=0

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/qBittorrent
  SUBMENU:=BitTorrent
  SECTION:=net
  CATEGORY:=Network
  TITLE:=BitTorrent Client Programmed in C++ / Qt
  URL:=https://www.qbittorrent.org/
  DEPENDS:=+libQt5Core +libQt5Network +libQt5Xml +libQt5Sql +boost +libtorrent-rasterbar
  USERID:=qbittorrent=227:qbittorrent=227
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
    -DLIBTINS_BUILD_EXAMPLES=OFF \
	-DLIBTINS_BUILD_TESTS=OFF \
    -DCMAKE_BUILD_TYPE="Release" \
    -DCMAKE_BUILD_WITH_INSTALL_RPATH=ON

CONFIGURE_VARS += \
	QT_QMAKE=$(STAGING_DIR_HOSTPKG)/bin \
	QMAKE_LRELEASE=$(STAGING_DIR_HOSTPKG)/bin/lrelease \
	PKG_CONFIG_PATH=$(STAGING_DIR)/usr/lib/pkgconfig

#CONFIGURE_ARGS += \
#	--disable-gui \
#	--with-boost=$(STAGING_DIR)/usr \
#    --prefix=$(STAGING_DIR)

MAKE_VARS += \
	INSTALL_ROOT=$(PKG_INSTALL_DIR)

define Package/qBittorrent/install
	$(INSTALL_DIR) $(1)/usr/share/man/man1
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/share/man/man1/qbittorrent-nox.1 $(1)/usr/share/man/man1/qbittorrent-nox.1
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/qbittorrent-nox $(1)/usr/bin
	$(INSTALL_DIR) $(1)/etc/init.d/
	$(INSTALL_BIN) qbittorrent_init $(1)/etc/init.d/qbittorrent
endef

$(eval $(call BuildPackage,qBittorrent))

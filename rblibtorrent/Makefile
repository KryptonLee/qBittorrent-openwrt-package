#
# Copyright (C) 2020 Krypton Lee <jun.k.lee199410@outlook.com>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=rblibtorrent
PKG_VERSION:=2.0.5
PKG_RELEASE:=2

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/arvidn/libtorrent/tar.gz/v$(PKG_VERSION)?
PKG_HASH:=8879d233d81b9bc1b02fdac35f6e1f69509c74da9818c6a819d18b5e42983f56
PKG_BUILD_DIR:=$(BUILD_DIR)/libtorrent-$(PKG_VERSION)

PKG_MAINTAINER:=Krypton Lee <jun.k.lee199410@outlook.com>
PKG_LICENSE:=BSD
PKG_LICENSE_FILES:=COPYING

PKG_BUILD_PARALLEL:=1
PKG_USE_MIPS16:=0
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/rblibtorrent
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=Rasterbar BitTorrent Library
  URL:=https://www.libtorrent.org/
  DEPENDS:=+boost +boost-system +boost-chrono +boost-random +libopenssl +libstdcpp
  MAINTAINER:=Arvid Norberg <arvid@libtorrent.org>
endef

define Package/rblibtorrent/description
Rasterbar libtorrent is a C++ library that aims to be a good alternative to
all the other bittorrent implementations around. It is a library and not a
full featured client, although it comes with a working example client.
endef

TRY_SIGNAL_VERSION:=334fd139e2bb387017b42d36753a03935e3bca75
TRY_SIGNAL_FILE:=$(PKG_NAME)-try_signal-$(TRY_SIGNAL_VERSION).tar.xz
define Download/try_signal
	VERSION:=$(TRY_SIGNAL_VERSION)
	SUBDIR:=deps/try_signal
	FILE:=$(TRY_SIGNAL_FILE)
	URL:=https://github.com/arvidn/try_signal.git
	MIRROR_HASH:=4e7a16dc64e4ad9b25c9358b6dc00117920d16f034858b4c2cab2d31ae066d21
	PROTO:=git
endef

$(eval $(call Download,try_signal))

define Build/Prepare
	$(Build/Prepare/Default)
	xzcat $(DL_DIR)/$(TRY_SIGNAL_FILE) | tar -C $(PKG_BUILD_DIR) $(TAR_OPTIONS)
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/libtorrent $(1)/usr/include/
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libtorrent-rasterbar.so* $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/pkgconfig/libtorrent-rasterbar.pc $(1)/usr/lib/pkgconfig/
endef

define Package/rblibtorrent/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libtorrent-rasterbar.so* $(1)/usr/lib/
endef

$(eval $(call BuildPackage,rblibtorrent))

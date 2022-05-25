#
# Copyright (C) 2022 Krypton Lee <jun.k.lee199410@outlook.com>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
# 

include $(TOPDIR)/rules.mk

PKG_NAME:=qt5tools
PKG_BASE_VERSION:=5.15
PKG_SUBVERSION:=4
PKG_VERSION:=$(PKG_BASE_VERSION).$(PKG_SUBVERSION)
PKG_RELEASE:=1

PKG_MD5SUM:=2466004ad9aad55f3416aadc370f8504
PKG_SOURCE:=qttools-everywhere-opensource-src-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=http://download.qt-project.org/archive/qt/$(PKG_BASE_VERSION)/$(PKG_VERSION)/submodules
PKG_BUILD_DIR:=$(BUILD_DIR)/qttools-everywhere-src-$(PKG_VERSION)

PKG_MAINTAINER:=Krypton Lee <jun.k.lee199410@outlook.com>
PKG_LICENSE:=LGPL-2.1
PKG_LICENSE_FILES:=COPYING

PKG_BUILD_DEPENDS:=qt5base
PKG_BUILD_PARALLEL:=1
PKG_USE_MIPS16:=0

include $(INCLUDE_DIR)/package.mk

define Package/qt5tools
  SECTION:=libs
  CATEGORY:=Libraries
  SUBMENU:=Qt5
  TITLE:=Qt5 Tools
  URL:=http://qt-project.org
  HIDDEN:=1
endef

CONFIGURE_ARGS := \
        -no-feature-assistant \
        -no-feature-designer \
        -no-feature-distancefieldgenerator \
        -no-feature-kmap2qmap \
        -no-feature-macdeployqt \
        -no-feature-makeqpf \
        -no-feature-pixeltool \
        -no-feature-qdbus \
        -no-feature-qev \
        -no-feature-qtattributionsscanner \
        -no-feature-qtpaths \
        -no-feature-qtplugininfo \
        -no-feature-qtdiag \
        -no-feature-windeployqt \
        -no-feature-winrtrunner

CONFIGURE_CMD := qmake -o Makefile qttools.pro

define Build/Configure
	(cd $(PKG_BUILD_DIR); \
		$(CONFIGURE_CMD) -- \
		$(CONFIGURE_ARGS) \
	)
endef

define Build/Compile
	$(MAKE) $(PKG_JOBS) -C $(PKG_BUILD_DIR)
endef

define Build/InstallDev
	$(MAKE) -C $(PKG_BUILD_DIR) install
endef

$(eval $(call BuildPackage,qt5tools))

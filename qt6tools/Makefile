#
# Copyright (C) 2022 Krypton Lee <jun.k.lee199410@outlook.com>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
# 

include $(TOPDIR)/rules.mk

PKG_NAME:=qt6tools
PKG_BASE_VERSION:=6.2
PKG_SUBVERSION:=4
PKG_VERSION:=$(PKG_BASE_VERSION).$(PKG_SUBVERSION)
PKG_RELEASE:=0

PKG_MD5SUM:=17797d64a1c049bb5dfd919ba9203ffa
PKG_SOURCE:=qttools-everywhere-src-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=http://download.qt-project.org/archive/qt/$(PKG_BASE_VERSION)/$(PKG_VERSION)/submodules
HOST_BUILD_DIR:=$(BUILD_DIR_HOST)/qttools-everywhere-src-$(PKG_VERSION)

PKG_MAINTAINER:=Krypton Lee <jun.k.lee199410@outlook.com>
PKG_LICENSE:=LGPL-2.1
PKG_LICENSE_FILES:=COPYING

PKG_HOST_ONLY:=1
HOST_BUILD_DEPENDS:=qt6base/host
HOST_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/host-build.mk
include $(INCLUDE_DIR)/cmake.mk
include $(INCLUDE_DIR)/package.mk

define Package/qt6tools
  SECTION:=libs
  CATEGORY:=Libraries
  SUBMENU:=Qt6
  TITLE:=Qt6 Tools
  URL:=http://qt-project.org
  HIDDEN:=1
endef

HOST_CONFIGURE_ARGS := \
        -no-feature-assistant \
        -no-feature-designer \
        -no-feature-distancefieldgenerator \
        -no-feature-kmap2qmap \
        -no-feature-macdeployqt \
        -no-feature-pixeltool \
        -no-feature-qdbus \
        -no-feature-qev \
        -no-feature-qtattributionsscanner \
        -no-feature-qtplugininfo \
        -no-feature-qtdiag \
        -no-feature-windeployqt

define Host/Configure
	(cd $(HOST_BUILD_DIR); \
		$(STAGING_DIR_HOSTPKG)/bin/qt-configure-module . $(HOST_CONFIGURE_ARGS) \
	)
endef

$(eval $(call BuildPackage,qt6tools))
$(eval $(call HostBuild))


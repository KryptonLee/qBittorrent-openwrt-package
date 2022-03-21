#
# Copyright (C) 2022 Krypton Lee <jun.k.lee199410@outlook.com>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=qt5base
PKG_BASE_VERSION:=5.14
PKG_SUBVERSION:=2
PKG_VERSION:=$(PKG_BASE_VERSION).$(PKG_SUBVERSION)
PKG_RELEASE:=1

PKG_MD5SUM:=b6c14e01ff20925305be109785ed4aa4
PKG_SOURCE:=qtbase-everywhere-src-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=http://download.qt-project.org/archive/qt/$(PKG_BASE_VERSION)/$(PKG_VERSION)/submodules
PKG_BUILD_DIR:=$(BUILD_DIR)/qtbase-everywhere-src-$(PKG_VERSION)

PKG_MAINTAINER:=Krypton Lee <jun.k.lee199410@outlook.com>
PKG_LICENSE:=LGPL-2.1
PKG_LICENSE_FILES:=COPYING

PKG_BUILD_PARALLEL:=1
PKG_USE_MIPS16:=0

include $(INCLUDE_DIR)/package.mk

define Package/libQt5/Default
  SECTION:=libs
  CATEGORY:=Libraries
  SUBMENU:=Qt5
  TITLE:=Qt5
  URL:=http://qt-project.org
  DEPENDS:=+libatomic +libstdcpp +zlib
endef

define Package/libQt5
  $(call Package/libQt5/Default)
  HIDDEN:=1
endef

define Package/libQt5/install
	true
endef

define Build/Configure
	(cd $(PKG_BUILD_DIR); \
		$(CONFIGURE_CMD) \
		-release \
		-strip \
		-prefix /usr \
		-extprefix $(STAGING_DIR)/usr \
		-hostprefix $(STAGING_DIR_HOSTPKG) \
		-device linux-generic-g++ \
		-device-option CROSS_COMPILE="$(TARGET_CROSS)" \
		-opensource \
		-confirm-license \
		-make libs \
		-shared \
		-optimize-size \
		-system-zlib \
		-no-zstd \
		-qt-doubleconversion \
		-no-glib \
		-no-iconv \
		-no-icu \
		-mimetype-database \
		-system-pcre \
		$(if $(CONFIG_PACKAGE_libQt5Concurrent),,-no-feature-concurrent) \
		$(if $(CONFIG_PACKAGE_libQt5DBus),,-no-dbus) \
		$(if $(CONFIG_PACKAGE_libQt5Gui),-no-opengl -system-freetype,-no-gui -no-freetype) \
		-no-feature-accessibility \
		-no-harfbuzz \
		-no-gif \
		-no-ico \
		-no-libjpeg \
		-no-libpng \
		-no-feature-texthtmlparser \
		-no-feature-cssparser \
		-no-feature-textodfwriter \
		-no-libmd4c \
		-no-feature-textmarkdownwriter \
		-no-feature-sessionmanager \
		-no-evdev \
		-no-linuxfb \
		$(if $(CONFIG_PACKAGE_libQt5Network),,-no-feature-network) \
		-openssl-linked \
		-no-feature-ocsp \
		$(if $(CONFIG_PACKAGE_libQt5Sql),,-no-feature-sql) \
		-no-feature-sqlmodel \
		-qt-sqlite \
		$(if $(CONFIG_PACKAGE_libQt5Test),,-no-feature-testlib) \
		-no-feature-itemmodeltester \
		$(if $(CONFIG_PACKAGE_libQt5Widgets),,-no-widgets) \
		$(if $(CONFIG_PACKAGE_libQt5Xml),,-no-feature-xml) \
		$(if $(CONFIG_PACKAGE_qt5-plugin-libqtuiotouchplugin),,-no-feature-tuiotouch) \
		-v \
	)
endef

define Build/Compile
	+$(MAKE) $(PKG_JOBS) -C $(PKG_BUILD_DIR)
endef

define Build/Install
	$(MAKE) -C $(PKG_BUILD_DIR) install
endef

define Package/libQt5/Default/install
  	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) $(STAGING_DIR)/usr/lib/libQt5$(2).so* $(1)/usr/lib/
endef

# 1: short name
# 2: dependencies on other qt5 libraries (short name)
# 3: dependencies on other packages
define DefineQt5Package
  QT5BASE_LIBS+=$(1)
  PKG_CONFIG_DEPENDS+=CONFIG_PACKAGE_libQt5$(1)

  define Package/libQt5$(1)
    $(call Package/libQt5/Default)
    TITLE+=$(1) Library
    DEPENDS+=$(foreach lib,$(2),+libQt5$(lib)) $(3)
  endef

  define Package/libQt5$(1)/description
This package provides the Qt5 $(1) v$(PKG_VERSION) library.
  endef

  define Package/libQt5$(1)/install
	$(call Package/libQt5/Default/install,$$(1),$(1))
  endef
endef

$(eval $(call DefineQt5Package,Concurrent,Core,))
$(eval $(call DefineQt5Package,Core,,+libpcre2-16))
$(eval $(call DefineQt5Package,DBus,Core,))
$(eval $(call DefineQt5Package,Gui,Core,+libfreetype))
$(eval $(call DefineQt5Package,Network,Core,+libopenssl))
$(eval $(call DefineQt5Package,PrintSupport,Widgets))
$(eval $(call DefineQt5Package,Sql,Core,))
$(eval $(call DefineQt5Package,Test,Core,))
$(eval $(call DefineQt5Package,Widgets,Gui,))
$(eval $(call DefineQt5Package,Xml,Core,))

define Package/qt5-plugin/Default/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) $(STAGING_DIR)/usr/plugins/$(2)/libq$(3).so* $(1)/usr/lib/
endef

# 1: plugin diretory
# 2: plugin name (short name)
# 3: dependencies on other qt5 libraries (short name)
define DefineQt5PluginPackage
  QT5_PLUGINS+=$(2)

  define Package/qt5-plugin-libq$(2)
    $(call Package/libQt5/Default)
    TITLE+=Plugin libq$(2)
    DEPENDS+=$(foreach lib,$(3),+libQt5$(lib))
  endef
  
  define Package/qt5-plugin-libq$(2)/install
	$(call Package/qt5-plugin/Default/install,$$(1),$(1),$(2))
  endef
endef

$(eval $(call DefineQt5PluginPackage,bearer,connmanbearer,DBus Network))
$(eval $(call DefineQt5PluginPackage,bearer,genericbearer,Network))
$(eval $(call DefineQt5PluginPackage,bearer,nmbearer,DBus Network))
$(eval $(call DefineQt5PluginPackage,generic,tuiotouchplugin,Gui Network))
$(eval $(call DefineQt5PluginPackage,platforms,minimal,Gui))
$(eval $(call DefineQt5PluginPackage,platforms,offscreen,Gui))
$(eval $(call DefineQt5PluginPackage,platformthemes,xdgdesktopportal,DBus Gui))
$(eval $(call DefineQt5PluginPackage,sqldrivers,sqlite,Sql))
PKG_CONFIG_DEPENDS+=qt5-plugin-libqtuiotouchplugin

$(foreach lib,$(QT5BASE_LIBS),$(eval $(call BuildPackage,libQt5$(lib))))
$(foreach lib,$(QT5_PLUGINS),$(eval $(call BuildPackage,qt5-plugin-libq$(lib))))
$(eval $(call BuildPackage,libQt5))

#
# Copyright (C) 2022 Krypton Lee <jun.k.lee199410@outlook.com>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=qt5base
PKG_BASE_VERSION:=5.15
PKG_SUBVERSION:=2
PKG_VERSION:=$(PKG_BASE_VERSION).$(PKG_SUBVERSION)
PKG_RELEASE:=1

PKG_MD5SUM:=0eb522ff6c2194f9690cbdcd5b33e803
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

define Package/libQt5/config
	choice
		prompt "Build Variant"
		default qt5_variant_release
		help
			Choose which Qt5 variant should be built:
			-> Release: Build Qt with debugging turned off.
			-> Debug: Build Qt with debugging turned on.

		config qt5_variant_release
			bool "Release"

		config qt5_variant_debug
			bool "Debug"
	endchoice

	config qt5_optimize_size
		depends on qt5_variant_release
		bool "Optimize Size"
		help
			Optimize release builds for size instead of speed.
			(Not available in debug variant)
		default n

	config qt5_optimize_debug
		depends on qt5_variant_debug
		bool "Optimize Debug"
		help
			Enable debug-friendly optimizations in debug builds.
			(Not available in release variant)
		default n

	config qt5_optimized_tools
		depends on qt5_variant_debug
		bool "Optimized Tools"
		help
			Build optimized host tools even in debug build.
		default n
endef

PKG_CONFIG_DEPENDS+= \
	qt5_variant_release \
	qt5_variant_debug \
	qt5_optimize_size \
	qt5_optimize_debug \
	qt5_optimized_tools

define Package/libQt5/install
	true
endef

define Build/Prepare
	$(call Build/Prepare/Default)
	$(INSTALL_DIR) $(PKG_BUILD_DIR)/mkspecs/linux-openwrt-g++
	$(CP) ./files/qplatformdefs.h $(PKG_BUILD_DIR)/mkspecs/linux-openwrt-g++/qplatformdefs.h
	$(CP) ./files/qmake.conf $(PKG_BUILD_DIR)/mkspecs/linux-openwrt-g++/qmake.conf
	$(SED) 's@$$$$(TARGET_CROSS)@$(TARGET_CROSS)@g' $(PKG_BUILD_DIR)/mkspecs/linux-openwrt-g++/qmake.conf
endef

define Build/Configure
	(cd $(PKG_BUILD_DIR); \
		$(CONFIGURE_CMD) \
		-prefix /usr \
		-extprefix $(STAGING_DIR)/usr \
		-hostprefix $(STAGING_DIR_HOSTPKG) \
		-xplatform linux-openwrt-g++ \
		-opensource \
		-confirm-license \
		-make libs \
		-shared \
		$(if $(CONFIG_qt5_variant_release),-release -strip,) \
		$(if $(CONFIG_qt5_variant_debug),-debug,) \
		$(if $(CONFIG_qt5_optimize_size),-optimize-size,-no-optimize-size) \
		$(if $(CONFIG_qt5_optimize_debug),-optimize-debug,-no-optimize-debug) \
		$(if $(CONFIG_qt5_optimized_tools),-optimized-tools,-no-optimized-tools) \
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
		$(if $(CONFIG_PACKAGE_libQt5Network),,-no-feature-network) \
		-openssl-linked \
		-no-feature-ocsp \
		$(if $(CONFIG_PACKAGE_libQt5Sql),,-no-feature-sql) \
		-qt-sqlite \
		$(if $(CONFIG_PACKAGE_libQt5Test),,-no-feature-testlib) \
		$(if $(CONFIG_PACKAGE_libQt5Widgets),,-no-widgets) \
		$(if $(CONFIG_PACKAGE_libQt5Xml),,-no-feature-xml) \
		-v \
	)
endef

define Build/Compile
	$(MAKE) $(PKG_JOBS) -C $(PKG_BUILD_DIR)
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

-----------------------------------------------------------------------------
|                                Warning                                    |
| In order to build the Qt5 Libraries, it is necessary to make sure your    |
| host system satisfies the requirements below:                             |
| - Perl 5.8 or later                                                       |
| - Python 2.7 or later                                                     |
| - C++ compiler supporting the C++11 standard                              |
-----------------------------------------------------------------------------
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
$(eval $(call DefineQt5Package,Sql,Core,))
$(eval $(call DefineQt5Package,Test,Core,))
$(eval $(call DefineQt5Package,Widgets,Gui,))
$(eval $(call DefineQt5Package,Xml,Core,))

define Package/qt5-plugin/Default/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) $(STAGING_DIR)/usr/plugins/$(2)/lib*.so* $(1)/usr/lib/
endef

# 1: plugin name
# 2: dependencies on other qt5 libraries (short name)
define DefineQt5PluginPackage
  QT5_PLUGINS+=$(1)

  define Package/qt5-plugin-$(1)
    $(call Package/libQt5/Default)
    TITLE+=Plugin $(1) Libraries
    DEPENDS+=$(foreach lib,$(2),+libQt5$(lib))
  endef
  
  define Package/qt5-plugin-$(1)/install
	$(call Package/qt5-plugin/Default/install,$$(1),$(1))
  endef
endef

$(eval $(call DefineQt5PluginPackage,bearer,DBus Network))
$(eval $(call DefineQt5PluginPackage,generic,Gui Network))
$(eval $(call DefineQt5PluginPackage,platforms,DBus Gui Network))
$(eval $(call DefineQt5PluginPackage,platformthemes,DBus Gui))
$(eval $(call DefineQt5PluginPackage,sqldrivers,Sql))

$(foreach lib,$(QT5BASE_LIBS),$(eval $(call BuildPackage,libQt5$(lib))))
$(foreach lib,$(QT5_PLUGINS),$(eval $(call BuildPackage,qt5-plugin-$(lib))))
$(eval $(call BuildPackage,libQt5))

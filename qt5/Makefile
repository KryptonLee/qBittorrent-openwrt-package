#
# Copyright (C) 2020 Krypton Lee <jun.k.lee199410@outlook.com>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=qt5
PKG_VERSION:=5.14
PKG_SUBVERSION:=2
PKG_RELEASE:=0

PKG_MD5SUM:=b3d2b6d00e6ca8a8ede6d1c9bdc74daf
PKG_SOURCE:=qt-everywhere-src-$(PKG_VERSION).$(PKG_SUBVERSION).tar.xz
PKG_SOURCE_URL:=http://download.qt-project.org/archive/qt/$(PKG_VERSION)/$(PKG_VERSION).$(PKG_SUBVERSION)/single
PKG_BUILD_DIR=$(BUILD_DIR)/qt-everywhere-src-$(PKG_VERSION).$(PKG_SUBVERSION)

PKG_MAINTAINER:=Krypton Lee <jun.k.lee199410@outlook.com>
PKG_LICENSE:=LGPL-2.1
PKG_LICENSE_FILES:=COPYING

PKG_BUILD_PARALLEL:=1
PKG_USE_MIPS16:=0
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/libQt5/Default
  SECTION:=libs
  CATEGORY:=Libraries
  SUBMENU:=Qt5
  TITLE:=Qt5
  URL:=http://qt-project.org
  DEPENDS:=+libatomic +libpthread +librt +libstdcpp +libzstd +zlib @!LINUX_2_6
endef

define Package/libQt5
  $(call Package/libQt5/Default)
  HIDDEN:=1
endef

define Package/libQt5/config
	choice
		prompt "Build Variant"
		default qt5-variant-release
		help
			Choose which Qt5 variant should be built:
			-> Release: Build Qt with debugging turned off.
			-> Debug: Build Qt with debugging turned on.

		config qt5-variant-release
			bool "Release"

		config qt5-variant-debug
			bool "Debug"
	endchoice

	config qt5-optimize-size
		depends on qt5-variant-release
		bool "Optimize Size"
		help
			Optimize release builds for size instead of speed.
			(Not available in debug variant)
		default n

	config qt5-optimize-debug
		depends on qt5-variant-debug
		bool "Optimize Debug"
		help
			Enable debug-friendly optimizations in debug builds.
			(Not available in release variant)
		default n

	config qt5-optimized-tools
		depends on qt5-variant-debug
		bool "Optimized Tools"
		help
			Build optimized host tools even in debug build.
		default n
endef

PKG_CONFIG_DEPENDS+=qt5-variant-release
PKG_CONFIG_DEPENDS+=qt5-variant-debug
PKG_CONFIG_DEPENDS+=qt5-optimize-size
PKG_CONFIG_DEPENDS+=qt5-optimize-debug
PKG_CONFIG_DEPENDS+=qt5-optimized-tools

define DefineQt5PackageConfig
  define Package/libQt5$(1)/config
  endef
endef

# 1: short name
# 2: dependencies on other qt5 libraries (short name)
# 3: whether add the package config to PKG_CONFIG_DEPENDS
# 4: whether define a blank config for the package 
define DefineQt5Package
  QT5_LIBS+=$(1)
  PKG_CONFIG_DEPENDS+=$(if $(3),CONFIG_PACKAGE_libQt5$(1),)

  define Package/libQt5$(1)
    $(call Package/libQt5/Default)
    TITLE+=$(1) Library
    DEPENDS+=$(foreach lib,$(2),+libQt5$(lib))
  endef

  $(if $(4),$(call DefineQt5PackageConfig,$(1)))

  define Package/libQt5$(1)/description
This package provides the Qt5 $(1) v$(PKG_VERSION).$(PKG_SUBVERSION) library.

-----------------------------------------------------------------------------
|                                Warning                                    |
| In order to build the Qt5 Libraries, it is necessary to make sure your    |
| host system satisfies the requirements below:                             |
| - Perl 5.8 or later                                                       |
| - Python 2.7 or later                                                     |
| - C++ compiler supporting the C++11 standard                              |
-----------------------------------------------------------------------------
  endef
endef

$(eval $(call DefineQt5Package,Bluetooth,Core,y,y))
$(eval $(call DefineQt5Package,Bodymovin,Gui,y,y))
$(eval $(call DefineQt5Package,Charts,Widgets,y,y))
$(eval $(call DefineQt5Package,Concurrent,Core))
$(eval $(call DefineQt5Package,Core,))
$(eval $(call DefineQt5Package,DBus,Core))
$(eval $(call DefineQt5Package,Gamepad,Gui,y,y))
$(eval $(call DefineQt5Package,Gui,Core,y,y))
$(eval $(call DefineQt5Package,Help,Network Sql Widgets))
$(eval $(call DefineQt5Package,Location,PositioningQuick))
$(eval $(call DefineQt5Package,Multimedia,Gui Network,y,y))
$(eval $(call DefineQt5Package,MultimediaQuick,Multimedia Quick))
$(eval $(call DefineQt5Package,MultimediaWidgets,Multimedia Widgets))
$(eval $(call DefineQt5Package,Network,Core))
$(eval $(call DefineQt5Package,NetworkAuth,Network,y,y))
$(eval $(call DefineQt5Package,Nfc,DBus,y,y))
$(eval $(call DefineQt5Package,Positioning,Core,y,y))
$(eval $(call DefineQt5Package,PositioningQuick,Positioning Quick))
$(eval $(call DefineQt5Package,PrintSupport,Widgets))
$(eval $(call DefineQt5Package,Purchasing,Core,y,y))
$(eval $(call DefineQt5Package,Qml,Network,y,y))
$(eval $(call DefineQt5Package,QmlModels,Qml))
$(eval $(call DefineQt5Package,QmlWorkerScript,Qml))
$(eval $(call DefineQt5Package,Quick,Gui QmlModels))
$(eval $(call DefineQt5Package,QuickControls2,QuickTemplates2))
$(eval $(call DefineQt5Package,QuickShapes,Quick))
$(eval $(call DefineQt5Package,QuickTemplates2,Quick,y,y))
$(eval $(call DefineQt5Package,QuickTest,Quick Test Widgets))
$(eval $(call DefineQt5Package,QuickWidgets,Quick Widgets))
$(eval $(call DefineQt5Package,RemoteObjects,Network,y,y))
$(eval $(call DefineQt5Package,Script,Core,y,y))
$(eval $(call DefineQt5Package,ScriptTools,Script Widgets))
$(eval $(call DefineQt5Package,Scxml,Qml,y,y))
$(eval $(call DefineQt5Package,Sensors,Core,y,y))
$(eval $(call DefineQt5Package,SerialBus,Network SerialPort,y,y))
$(eval $(call DefineQt5Package,SerialPort,Core,y,y))
$(eval $(call DefineQt5Package,Sql,Core))
$(eval $(call DefineQt5Package,Svg,Widgets,y,y))
$(eval $(call DefineQt5Package,Test,Core))
$(eval $(call DefineQt5Package,TextToSpeech,Core,y,y))
$(eval $(call DefineQt5Package,VirtualKeyboard,Quick,y,y))
$(eval $(call DefineQt5Package,WebChannel,Qml,y,y))
$(eval $(call DefineQt5Package,WebSockets,Network,y,y))
$(eval $(call DefineQt5Package,WebView,Quick,y,y))
$(eval $(call DefineQt5Package,Widgets,Gui,y,y))
$(eval $(call DefineQt5Package,Xml,Core))
$(eval $(call DefineQt5Package,XmlPatterns,Network,y,y))

# 1: plugin name
# 2: dependencies on other qt5 libraries (short name)
define DefineQt5PluginPackage
  QT5_PLUGINS+=$(1)

  define Package/qt5-plugin-$(1)
    $(call Package/libQt5/Default)
    TITLE+=Plugin $(1) Libraries
    DEPENDS+=$(foreach lib,$(2),+libQt5$(lib))
  endef
endef

$(eval $(call DefineQt5PluginPackage,bearer,DBus Network))
$(eval $(call DefineQt5PluginPackage,canbus,SerialBus))
$(eval $(call DefineQt5PluginPackage,gamepads,Gamepad))
$(eval $(call DefineQt5PluginPackage,generic,Gui Network))
$(eval $(call DefineQt5PluginPackage,geoservices,Concurrent Location))
$(eval $(call DefineQt5PluginPackage,iconengines,Svg))
$(eval $(call DefineQt5PluginPackage,imageformats,Svg))
$(eval $(call DefineQt5PluginPackage,mediaservice,Multimedia))
$(eval $(call DefineQt5PluginPackage,platforminputcontexts,VirtualKeyboard))
$(eval $(call DefineQt5PluginPackage,platforms,DBus Gui Network))
$(eval $(call DefineQt5PluginPackage,platformthemes,DBus Gui))
$(eval $(call DefineQt5PluginPackage,playlistformats,Multimedia))
$(eval $(call DefineQt5PluginPackage,position,DBus Positioning SerialPort))
$(eval $(call DefineQt5PluginPackage,qmltooling,Quick))
$(eval $(call DefineQt5PluginPackage,sensorgestures,Sensors))
$(eval $(call DefineQt5PluginPackage,sensors,DBus Sensors))
$(eval $(call DefineQt5PluginPackage,sqldrivers,Sql))
$(eval $(call DefineQt5PluginPackage,virtualkeyboard,VirtualKeyboard))

CONFIGURE_ARGS:= \
	-prefix /usr \
	-extprefix $(PKG_INSTALL_DIR)/usr \
	-hostprefix $(STAGING_DIR_HOSTPKG) \
	-xplatform linux-openwrt-g++ \
	-opensource \
	-confirm-license \
	-make libs \
	-shared \
	-no-opengl \
	-skip 3d \
	-skip activeqt \
	-skip androidextras \
	-skip datavis3d \
	-skip doc \
	-skip macextras \
	-skip quick3d \
	-skip quickcontrols \
	-skip quicktimeline \
	-skip translations \
	-skip wayland \
	-skip webengine \
	-skip webglplugin \
	-skip winextras \
	-skip x11extras \
	-v

define Build/Prepare
	$(call Build/Prepare/Default)
	$(INSTALL_DIR) $(PKG_BUILD_DIR)/qtbase/mkspecs/linux-openwrt-g++
	$(CP) ./files/qplatformdefs.h $(PKG_BUILD_DIR)/qtbase/mkspecs/linux-openwrt-g++/qplatformdefs.h
	$(CP) ./files/qmake.conf $(PKG_BUILD_DIR)/qtbase/mkspecs/linux-openwrt-g++/qmake.conf
	$(SED) 's@$$$$(TARGET_CROSS)@$(TARGET_CROSS)@g' $(PKG_BUILD_DIR)/qtbase/mkspecs/linux-openwrt-g++/qmake.conf
endef

define Build/Configure
	(cd $(PKG_BUILD_DIR); \
		$(CONFIGURE_CMD) \
		$(CONFIGURE_ARGS) \
		$(if $(CONFIG_qt5-variant-release),-release,) \
		$(if $(CONFIG_qt5-variant-debug),-debug,) \
		$(if $(CONFIG_qt5-optimize-size),-optimize-size,) \
		$(if $(CONFIG_qt5-optimize-debug),-optimize-debug,) \
		$(if $(CONFIG_qt5-optimized-tools),-optimized-tools,) \
		$(if $(CONFIG_PACKAGE_libQt5Bluetooth),,$(if $(CONFIG_PACKAGE_libQt5Nfc),,-skip connectivity)) \
		$(if $(CONFIG_PACKAGE_libQt5Bodymovin),,-skip lottie) \
		$(if $(CONFIG_PACKAGE_libQt5Charts),,-skip charts) \
		$(if $(CONFIG_PACKAGE_libQt5Gamepad),,-skip gamepad) \
		$(if $(CONFIG_PACKAGE_libQt5Gui),-no-opengl,-no-gui) \
		$(if $(CONFIG_PACKAGE_libQt5Multimedia),,-skip multimedia) \
		$(if $(CONFIG_PACKAGE_libQt5NetworkAuth),,-skip networkauth) \
		$(if $(CONFIG_PACKAGE_libQt5Positioning),,-skip location) \
		$(if $(CONFIG_PACKAGE_libQt5Purchasing),,-skip purchasing) \
		$(if $(CONFIG_PACKAGE_libQt5Qml),,-skip declarative) \
		$(if $(CONFIG_PACKAGE_libQt5QuickTemplates2),,-skip quickcontrols2 -skip graphicaleffects) \
		$(if $(CONFIG_PACKAGE_libQt5RemoteObjects),,-skip remoteobjects) \
		$(if $(CONFIG_PACKAGE_libQt5Script),,-skip script) \
		$(if $(CONFIG_PACKAGE_libQt5Scxml),,-skip scxml) \
		$(if $(CONFIG_PACKAGE_libQt5Sensors),,-skip sensors) \
		$(if $(CONFIG_PACKAGE_libQt5SerialBus),,-skip serialbus) \
		$(if $(CONFIG_PACKAGE_libQt5SerialPort),,-skip serialport) \
		$(if $(CONFIG_PACKAGE_libQt5Svg),,-skip svg) \
		$(if $(CONFIG_PACKAGE_libQt5TextToSpeech),,-skip speech) \
		$(if $(CONFIG_PACKAGE_libQt5VirtualKeyboard),,-skip virtualkeyboard) \
		$(if $(CONFIG_PACKAGE_libQt5WebChannel),,-skip webchannel) \
		$(if $(CONFIG_PACKAGE_libQt5WebSockets),,-skip websockets) \
		$(if $(CONFIG_PACKAGE_libQt5WebView),,-skip webview) \
		$(if $(CONFIG_PACKAGE_libQt5Widgets),,-no-widgets) \
		$(if $(CONFIG_PACKAGE_libQt5XmlPatterns),,-skip xmlpatterns) \
	)
endef

define Build/Compile
	$(MAKE) $(PKG_JOBS) -C $(PKG_BUILD_DIR)
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/Qt* $(1)/usr/include/
	$(INSTALL_DIR) $(1)/usr/lib
	if [ $$(ls lib*.a | wc -l) != 0 ]; then \
		$(CP) $(PKG_INSTALL_DIR)/usr/lib/lib*.a $(1)/usr/lib/; \
	fi
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/lib*.so* $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/pkgconfig/Qt5*.pc $(1)/usr/lib/pkgconfig/
endef

define DefineQt5PackageInstall
  define Package/libQt5$(1)/install
  	$$(INSTALL_DIR) $$(1)/usr/lib/
	$$(CP) $$(PKG_INSTALL_DIR)/usr/lib/libQt5$(1).so* $$(1)/usr/lib/
  endef
endef

define Package/libQt5/install
	true
endef

$(foreach lib,$(QT5_LIBS),$(eval $(call DefineQt5PackageInstall,$(lib))))

define DefineQt5PluginPackageInstall
  define Package/qt5-plugin-$(1)/install
	$$(INSTALL_DIR) $$(1)/usr/lib/
	$$(CP) $$(PKG_INSTALL_DIR)/usr/plugins/$(1)/lib*.so* $$(1)/usr/lib/
  endef
endef

$(foreach lib,$(QT5_PLUGINS),$(eval $(call DefineQt5PluginPackageInstall,$(lib))))

$(foreach lib,$(QT5_LIBS),$(eval $(call BuildPackage,libQt5$(lib))))
$(foreach lib,$(QT5_PLUGINS),$(eval $(call BuildPackage,qt5-plugin-$(lib))))
$(eval $(call BuildPackage,libQt5))

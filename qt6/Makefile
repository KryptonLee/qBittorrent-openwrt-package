#
# Copyright (C) 2021 Pavlov Dmitriy 
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=qt6
PKG_VERSION:=6.2
PKG_SUBVERSION:=1

PKG_MD5SUM:=9c9adc6cb60cbd7792b9d0226b7467fa
PKG_SOURCE:=qt-everywhere-src-$(PKG_VERSION).$(PKG_SUBVERSION).tar.xz
PKG_SOURCE_URL:=http://download.qt-project.org/archive/qt/$(PKG_VERSION)/$(PKG_VERSION).$(PKG_SUBVERSION)/single
PKG_BUILD_DIR=$(BUILD_DIR)/qt-everywhere-src-$(PKG_VERSION).$(PKG_SUBVERSION)

PKG_MAINTAINER:=Pavlov Dmitriy 
PKG_LICENSE:=LGPL-2.1
PKG_LICENSE_FILES:=COPYING

PKG_BUILD_PARALLEL:=1
PKG_USE_MIPS16:=0
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/libQt6/Default
  SECTION:=libs
  CATEGORY:=Libraries
  SUBMENU:=Qt6
  TITLE:=Qt6
  URL:=http://qt-project.org
  DEPENDS:=+libatomic +libpthread +librt +libstdcpp +libopenssl +zlib @!LINUX_2_6
endef

define Package/libQt6
  $(call Package/libQt6/Default)
  HIDDEN:=1
endef

define Package/libQt6/config
	choice
		prompt "Build Variant"
		default Qt6-variant-release
		help
			Choose which Qt6 variant should be built:
			-> Release: Build Qt with debugging turned off.
			-> Debug: Build Qt with debugging turned on.

		config Qt6-variant-release
			bool "Release"

		config Qt6-variant-debug
			bool "Debug"
	endchoice

	config Qt6-optimize-size
		depends on @Qt6-variant-release
		bool "Optimize Size"
		help
			Optimize release builds for size instead of speed.
			(Not available in debug variant)
		default n

	config Qt6-optimize-debug
		depends on @Qt6-variant-debug
		bool "Optimize Debug"
		help
			Enable debug-friendly optimizations in debug builds.
			(Not available in release variant)
		default n

	config Qt6-optimized-tools
		depends on @Qt6-variant-debug
		bool "Optimized Tools"
		help
			Build optimized host tools even in debug build.
		default n
endef

PKG_CONFIG_DEPENDS+=Qt6-variant-release
PKG_CONFIG_DEPENDS+=Qt6-variant-debug
PKG_CONFIG_DEPENDS+=Qt6-optimize-size
PKG_CONFIG_DEPENDS+=Qt6-optimize-debug
PKG_CONFIG_DEPENDS+=Qt6-optimized-tools

define DefineQt6PackageConfig
  define Package/libQt6$(1)/config
  endef
endef



# 1: short name
# 2: dependencies on other Qt6 libraries (short name)
# 3: whether add the package config to PKG_CONFIG_DEPENDS
# 4: whether define a blank config for the package 
define DefineQt6Package
  Qt6_LIBS+=$(1)
  PKG_CONFIG_DEPENDS+=$(if $(3),CONFIG_PACKAGE_libQt6$(1),)

  define Package/libQt6$(1)
    $(call Package/libQt6/Default)
    TITLE+=$(1) Library
    DEPENDS+=$(foreach lib,$(2),+libQt6$(lib))
  endef

  $(if $(4),$(call DefineQt6PackageConfig,$(1)))

  define Package/libQt6$(1)/description
This package provides the Qt6 $(1) v$(PKG_VERSION).$(PKG_SUBVERSION) library.

-----------------------------------------------------------------------------
|                                Warning                                    |
| In order to build the Qt6 Libraries, it is necessary to make sure your    |
| host system satisfies the requirements below:                             |
| - Perl 5.8 or later                                                       |
| - Python 2.7 or later                                                     |
| - C++ compiler supporting the C++11 standard                              |
-----------------------------------------------------------------------------
  endef
endef

$(eval $(call DefineQt6Package,Bluetooth,Core,y,y))
$(eval $(call DefineQt6Package,Bodymovin,Gui,y,y))
$(eval $(call DefineQt6Package,Charts,Widgets,y,y))
$(eval $(call DefineQt6Package,Concurrent,Core))
$(eval $(call DefineQt6Package,Core,))
$(eval $(call DefineQt6Package,DBus,Core))
$(eval $(call DefineQt6Package,Gamepad,Gui,y,y))
$(eval $(call DefineQt6Package,Gui,Core,y,y))
$(eval $(call DefineQt6Package,Help,Network Sql Widgets))
$(eval $(call DefineQt6Package,Location,PositioningQuick))
$(eval $(call DefineQt6Package,Multimedia,Gui Network,y,y))
$(eval $(call DefineQt6Package,MultimediaQuick,Multimedia Quick))
$(eval $(call DefineQt6Package,MultimediaWidgets,Multimedia Widgets))
$(eval $(call DefineQt6Package,Network,Core))
$(eval $(call DefineQt6Package,NetworkAuth,Network,y,y))
$(eval $(call DefineQt6Package,Nfc,DBus,y,y))
$(eval $(call DefineQt6Package,Positioning,Core,y,y))
$(eval $(call DefineQt6Package,PositioningQuick,Positioning Quick))
$(eval $(call DefineQt6Package,PrintSupport,Widgets))
$(eval $(call DefineQt6Package,Purchasing,Core,y,y))
$(eval $(call DefineQt6Package,Qml,Network,y,y))
$(eval $(call DefineQt6Package,QmlModels,Qml))
$(eval $(call DefineQt6Package,QmlWorkerScript,Qml))
$(eval $(call DefineQt6Package,Quick,Gui QmlModels))
$(eval $(call DefineQt6Package,QuickControls2,QuickTemplates2))
$(eval $(call DefineQt6Package,QuickShapes,Quick))
$(eval $(call DefineQt6Package,QuickTemplates2,Quick,y,y))
$(eval $(call DefineQt6Package,QuickTest,Quick Test Widgets))
$(eval $(call DefineQt6Package,QuickWidgets,Quick Widgets))
$(eval $(call DefineQt6Package,RemoteObjects,Network,y,y))
$(eval $(call DefineQt6Package,Script,Core,y,y))
$(eval $(call DefineQt6Package,ScriptTools,Script Widgets))
$(eval $(call DefineQt6Package,Scxml,Qml,y,y))
$(eval $(call DefineQt6Package,Sensors,Core,y,y))
$(eval $(call DefineQt6Package,SerialBus,Network SerialPort,y,y))
$(eval $(call DefineQt6Package,SerialPort,Core,y,y))
$(eval $(call DefineQt6Package,Sql,Core))
$(eval $(call DefineQt6Package,Svg,Widgets,y,y))
$(eval $(call DefineQt6Package,Test,Core))
$(eval $(call DefineQt6Package,TextToSpeech,Core,y,y))
$(eval $(call DefineQt6Package,VirtualKeyboard,Quick,y,y))
$(eval $(call DefineQt6Package,WebChannel,Qml,y,y))
$(eval $(call DefineQt6Package,WebSockets,Network,y,y))
$(eval $(call DefineQt6Package,WebView,Quick,y,y))
$(eval $(call DefineQt6Package,Widgets,Gui,y,y))
$(eval $(call DefineQt6Package,Xml,Core))
$(eval $(call DefineQt6Package,XmlPatterns,Network,y,y))

# 1: plugin name
# 2: dependencies on other Qt6 libraries (short name)
define DefineQt6PluginPackage
  Qt6_PLUGINS+=$(1)

  define Package/Qt6-plugin-$(1)
    $(call Package/libQt6/Default)
    TITLE+=Plugin $(1) Libraries
    DEPENDS+=$(foreach lib,$(2),+libQt6$(lib))
  endef
endef

$(eval $(call DefineQt6PluginPackage,bearer,DBus Network))
$(eval $(call DefineQt6PluginPackage,canbus,SerialBus))
$(eval $(call DefineQt6PluginPackage,gamepads,Gamepad))
$(eval $(call DefineQt6PluginPackage,generic,Gui Network))
$(eval $(call DefineQt6PluginPackage,geoservices,Concurrent Location))
$(eval $(call DefineQt6PluginPackage,iconengines,Svg))
$(eval $(call DefineQt6PluginPackage,imageformats,Svg))
$(eval $(call DefineQt6PluginPackage,mediaservice,Multimedia))
$(eval $(call DefineQt6PluginPackage,platforminputcontexts,VirtualKeyboard))
$(eval $(call DefineQt6PluginPackage,platforms,DBus Gui Network))
$(eval $(call DefineQt6PluginPackage,platformthemes,DBus Gui))
$(eval $(call DefineQt6PluginPackage,playlistformats,Multimedia))
$(eval $(call DefineQt6PluginPackage,position,DBus Positioning SerialPort))
$(eval $(call DefineQt6PluginPackage,qmltooling,Quick))
$(eval $(call DefineQt6PluginPackage,sensorgestures,Sensors))
$(eval $(call DefineQt6PluginPackage,sensors,DBus Sensors))
$(eval $(call DefineQt6PluginPackage,sqldrivers,Sql))
$(eval $(call DefineQt6PluginPackage,virtualkeyboard,VirtualKeyboard))

CMAKE_OPTIONS += \
    -DQT_HOST_PATH=/home/dmitriy/Qt/6.2.1/gcc_64 \
    -DCMAKE_BUILD_TYPE="Release" \
    -DQT_FEATURE_optimize_full=ON \
    -DQT_FEATURE_gui=OFF \
    -DQT_FEATURE_openssl_linked=ON \
    -DQT_FEATURE_dbus=OFF \
    -DQT_FEATURE_LinguistTools=ON \
    -DQT_FEATURE_zstd=OFF \
    -DQT_FEATURE_concurrent=OFF \
    -DQT_FEATURE_printsupport=OFF \
    -DQT_FEATURE_system_pcre2=OFF \
    -DQT_FEATURE_widgets=OFF \
    -DQT_FEATURE_testlib=OFF \
    -DQT_BUILD_EXAMPLES=OFF \
    -DQT_BUILD_TESTS=OFF \
    -DFEATURE_icu=OFF \
    -DBUILD_SHARED_LIBS=ON \
	-DCMAKE_SKIP_RPATH=ON \
    -DCMAKE_SKIP_INSTALL_RPATH=ON \
    -DBUILD_qtwebview=OFF \
    -DBUILD_qtwebsockets=OFF \
    -DBUILD_qtwebengine=OFF \
    -DBUILD_qtwebchannel=OFF \
    -DBUILD_qtwayland=OFF \
    -DBUILD_qtvirtualkeyboard=OFF \
    -DBUILD_qttranslations=OFF \
    -DBUILD_qttools=ON \
    -DBUILD_qtsvg=OFF \
    -DBUILD_qtshadertools=OFF \
    -DBUILD_qtserialport=OFF \
    -DBUILD_qtserialbus=OFF \
    -DBUILD_qtsensors=OFF \
    -DBUILD_qtscxml=OFF \
    -DBUILD_qtremoteobjects=OFF \
    -DBUILD_qtquicktimeline=OFF \
    -DBUILD_qtquick3d=OFF \
    -DBUILD_qtnetworkauth=OFF \
    -DBUILD_qtmultimedia=OFF \
    -DBUILD_qtlottie=OFF \
    -DBUILD_qtlocation=OFF \
    -DBUILD_qtimageformats=OFF \
    -DBUILD_qtdoc=OFF \
    -DBUILD_qtdeclarative=OFF \
    -DBUILD_qtdatavis3d=OFF \
    -DBUILD_qtconnectivity=OFF \
    -DBUILD_qtcharts=OFF \
    -DBUILD_qtactiveqt=OFF \
    -DBUILD_qt5compat=OFF \
    -DBUILD_qt3d=OFF \
    -DBUILD_qtmqtt=OFF \
    -DBUILD_qtopcua=OFF \
    -DBUILD_qtcoap=OFF 


define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/Qt* $(1)/usr/include/
	$(INSTALL_DIR) $(1)/usr/lib
	if [ $$(ls lib*.a | wc -l) != 0 ]; then \
		$(CP) $(PKG_INSTALL_DIR)/usr/lib/lib*.a $(1)/usr/lib/; \
	fi
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/lib*.so* $(1)/usr/lib/
#	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
#	$(CP) $(PKG_INSTALL_DIR)/usr/lib/pkgconfig/Qt6*.pc $(1)/usr/lib/pkgconfig/
	$(INSTALL_DIR) $(1)/usr/lib/cmake/Qt6
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/cmake/Qt6/*.cmake $(1)/usr/lib/cmake/Qt6/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/cmake/Qt6/QtFileConfigure.txt.in $(1)/usr/lib/cmake/Qt6/QtFileConfigure.txt.in
	$(INSTALL_DIR) $(1)/usr/mkspecs
	$(INSTALL_DIR) $(1)/usr/mkspecs/linux-g++
	$(CP) $(PKG_INSTALL_DIR)/usr/mkspecs/linux-g++/qmake.conf $(1)/usr/mkspecs/linux-g++/qmake.conf
	$(CP) $(PKG_INSTALL_DIR)/usr/mkspecs/linux-g++/qplatformdefs.h $(1)/usr/mkspecs/linux-g++/qplatformdefs.h
#	$(INSTALL_DIR) $(1)/usr/lib/cmake/Qt6AttributionsScannerTools
#	$(CP) $(PKG_INSTALL_DIR)/usr/lib/cmake/Qt6AttributionsScannerTools/*.cmake $(1)/usr/lib/cmake/Qt6AttributionsScannerTools/
#	$(INSTALL_DIR) $(1)/usr/lib/cmake/Qt6BootstrapDBus
#	$(CP) $(PKG_INSTALL_DIR)/usr/lib/cmake/Qt6BootstrapDBus/*.cmake $(1)/usr/lib/cmake/Qt6BootstrapDBus/
	$(INSTALL_DIR) $(1)/usr/lib/cmake/Qt6BuildInternals
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/cmake/Qt6BuildInternals/*.cmake $(1)/usr/lib/cmake/Qt6BuildInternals/
#	$(INSTALL_DIR) $(1)/usr/lib/cmake/Qt6Concurrent
#	$(CP) $(PKG_INSTALL_DIR)/usr/lib/cmake/Qt6Concurrent/*.cmake $(1)/usr/lib/cmake/Qt6Concurrent/
	$(INSTALL_DIR) $(1)/usr/lib/cmake/Qt6Core
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/cmake/Qt6Core/*.cmake $(1)/usr/lib/cmake/Qt6Core/
#	$(INSTALL_DIR) $(1)/usr/lib/cmake/Qt6DBus
#	$(CP) $(PKG_INSTALL_DIR)/usr/lib/cmake/Qt6DBus/*.cmake $(1)/usr/lib/cmake/Qt6DBus/
#	$(INSTALL_DIR) $(1)/usr/lib/cmake/Qt6LinguistTools
#	$(CP) $(PKG_INSTALL_DIR)/usr/lib/cmake/Qt6LinguistTools/*.cmake $(1)/usr/lib/cmake/Qt6LinguistTools/
#	$(INSTALL_DIR) $(1)/usr/lib/cmake/Qt6Zlib
#	$(CP) $(PKG_INSTALL_DIR)/usr/lib/cmake/Qt6Zlib/*.cmake $(1)/usr/lib/cmake/Qt6Zlib/
	$(INSTALL_DIR) $(1)/usr/lib/cmake/Qt6Sql
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/cmake/Qt6Sql/*.cmake $(1)/usr/lib/cmake/Qt6Sql/
#	$(INSTALL_DIR) $(1)/usr/lib/cmake/Qt6Test
#	$(CP) $(PKG_INSTALL_DIR)/usr/lib/cmake/Qt6Test/*.cmake $(1)/usr/lib/cmake/Qt6Test/
	$(INSTALL_DIR) $(1)/usr/lib/cmake/Qt6Network
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/cmake/Qt6Network/*.cmake $(1)/usr/lib/cmake/Qt6Network/
	$(INSTALL_DIR) $(1)/usr/lib/cmake/Qt6Xml
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/cmake/Qt6Xml/*.cmake $(1)/usr/lib/cmake/Qt6Xml/
	$(INSTALL_DIR) $(1)/usr/plugins
#	$(INSTALL_DIR) $(1)/usr/plugins/bearer
#	$(CP) $(PKG_INSTALL_DIR)/usr/plugins/bearer/*.so $(1)/usr/plugins/bearer/
	$(INSTALL_DIR) $(1)/usr/plugins/sqldrivers
	$(CP) $(PKG_INSTALL_DIR)/usr/plugins/sqldrivers/*.so $(1)/usr/plugins/sqldrivers/
	$(INSTALL_DIR) $(1)/usr/modules
	$(CP) $(PKG_INSTALL_DIR)/usr/modules/*.json $(1)/usr/modules/

endef

define DefineQt6PackageInstall
  define Package/libQt6$(1)/install
  	$$(INSTALL_DIR) $$(1)/usr/lib/
	$$(CP) $$(PKG_INSTALL_DIR)/usr/lib/libQt6$(1).so* $$(1)/usr/lib/
  endef
endef

define Package/libQt6/install
	true
endef

$(foreach lib,$(Qt6_LIBS),$(eval $(call DefineQt6PackageInstall,$(lib))))

define DefineQt6PluginPackageInstall
  define Package/Qt6-plugin-$(1)/install
	$$(INSTALL_DIR) $$(1)/usr/lib/
	$$(CP) $$(PKG_INSTALL_DIR)/usr/plugins/$(1)/lib*.so* $$(1)/usr/lib/
  endef
endef

$(foreach lib,$(Qt6_PLUGINS),$(eval $(call DefineQt6PluginPackageInstall,$(lib))))

$(foreach lib,$(Qt6_LIBS),$(eval $(call BuildPackage,libQt6$(lib))))
$(foreach lib,$(Qt6_PLUGINS),$(eval $(call BuildPackage,Qt6-plugin-$(lib))))
$(eval $(call BuildPackage,libQt6))

#
# Copyright (C) 2015 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=libcrafter
PKG_VERSION:=0.3
PKG_RELEASE:=1

PKG_SOURCE:=version-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/pellegre/libcrafter/archive/
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)
PKG_MD5SUM:=dcad7565600eccaf36eebf97f400e47a

PKG_INSTALL:=1
PKG_FIXUP:=autoreconf

UNPACK_CMD=tar --strip-components=2 -C $(1) -xf "$(DL_DIR)/$(PKG_SOURCE)"

include $(INCLUDE_DIR)/uclibc++.mk
include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/autotools.mk

define Package/libcrafter
  TITLE:=A high level library for C++ to generate and sniff network packets
  URL:=https://code.google.com/p/libcrafter/
  DEPENDS:=+libpcap +libpthread +librt +uclibcxx
  SECTION:=libs
  CATEGORY:=Libraries
endef

CONFIGURE_ARGS += \
	--with-libpcap=$(STAGING_DIR)/usr

define Package/libcrafter/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libcrafter.so* $(1)/usr/lib/
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/crafter.h $(1)/usr/include/
	$(INSTALL_DIR) $(1)/usr/include/crafter
	$(CP) $(PKG_INSTALL_DIR)/usr/include/crafter/* $(1)/usr/include/crafter/
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libcrafter.so* $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/lib/pkgconfig/crafter.pc $(1)/usr/lib/pkgconfig
endef

$(eval $(call BuildPackage,libcrafter))

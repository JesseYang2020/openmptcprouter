#
# Copyright (C) 2013-2019 OpenWrt.org
# Copyright (C) 2019 Alexey Loukianov
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_VERSION:=2020.04

PKG_HASH:=fe732aaf037d9cc3c0909bad8362af366ae964bbdac6913a34081ff4ad565372

PKG_MAINTAINER:=Cristian Ciobanu <cioby.service@gmail.com>

include $(INCLUDE_DIR)/u-boot.mk
include $(INCLUDE_DIR)/package.mk

define U-Boot/Default
  BUILD_TARGET:=mediatek
  UBOOT_IMAGE:=u-boot.bin
  UENV:=default
  HIDDEN:=1
endef

define U-Boot/mt7623n_bpir2
  BUILD_SUBTARGET:=mt7623
  NAME:=Bannana PI R2 (mt7623)
  BUILD_DEVICES:=bpi_bananapi-r2
endef

UBOOT_TARGETS := \
	mt7623n_bpir2

UBOOT_CONFIGURE_VARS += USE_PRIVATE_LIBGCC=yes

UBOOT_MAKE_FLAGS = \
	HOSTCC="$(HOSTCC)" \
	HOSTCFLAGS="$(HOST_CFLAGS) $(HOST_CPPFLAGS) -std=gnu11" \
	HOSTLDFLAGS="$(HOST_LDFLAGS)"

define Build/Prepare
        $(call Build/Prepare/Default)
	$(CP) uEnv-$(UENV).txt ${PKG_BUILD_DIR}/uEnv.txt
endef

define Build/InstallDev
	$(INSTALL_DIR) $(STAGING_DIR_IMAGE)
	$(CP) $(PKG_BUILD_DIR)/$(UBOOT_IMAGE) $(STAGING_DIR_IMAGE)/$(BUILD_DEVICES)-uboot-mediatek.bin
	$(CP) $(PKG_BUILD_DIR)/uEnv.txt $(STAGING_DIR_IMAGE)/$(BUILD_DEVICES)-uEnv.txt
endef

define Package/u-boot/install/default
endef

$(eval $(call BuildPackage/U-Boot))

#
# Copyright (C) 2008 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.


include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=sx1278
PKG_RELEASE:=1

include $(INCLUDE_DIR)/package.mk

define KernelPackage/sx1278
  SUBMENU:=WPAN 802.15.4 Support
  TITLE:=Semtech SX127x and HopeRF RFM9x LoRa WPAN driver
  DEPENDS:=+kmod-mac802154
  FILES:=$(PKG_BUILD_DIR)/sx1278.ko
	AUTOLOAD:=$(call AutoProbe,sx1278)
  KCONFIG:=
endef

define KernelPackage/sx1278/description
 Semtech SX127x and HopeRF RFM9x LoRa WPAN driver
endef
EXTRA_KCONFIG:= \
	CONFIG_MAC802154_SX1278=m

EXTRA_CFLAGS:= \
	$(patsubst CONFIG_%, -DCONFIG_%=1, $(patsubst %=m,%,$(filter %=m,$(EXTRA_KCONFIG)))) \
	$(patsubst CONFIG_%, -DCONFIG_%=1, $(patsubst %=y,%,$(filter %=y,$(EXTRA_KCONFIG))))

MAKE_OPTS:= \
	$(KERNEL_MAKE_FLAGS) \
	SUBDIRS="$(PKG_BUILD_DIR)" \
	CONFIG_OF=1

#define Build/Prepare
#	mkdir -p $(PKG_BUILD_DIR)
#	$(CP) ./src/* $(PKG_BUILD_DIR)/
#endef

define Build/Compile
	$(MAKE) -C "$(LINUX_DIR)" \
		$(MAKE_OPTS) \
		modules
endef

$(eval $(call KernelPackage,sx1278))


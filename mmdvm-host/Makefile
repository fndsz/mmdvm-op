#
# Copyright 2019-2020 Michael BD7MQB <bd7mqb@qq.com>
# This is free software, licensed under the GNU GENERAL PUBLIC LICENSE, Version 2.0
#

include $(TOPDIR)/rules.mk

PKG_NAME:=mmdvm-host
PKG_REV:=81ad9f0
PKG_VERSION:=1.3.2
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=https://github.com/lazywalker/MMDVMHost.git
PKG_MIRROR_HASH:=022b634973d5f1836623c37bc4dae13719a18f3c56411a466f4e5e8f31931ed8
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=$(PKG_REV)
PKG_SOURCE_PROTO:=git
PKG_LICENSE:=GPL-2.0
PKG_MAINTAINER:=Michael BD7MQB <bd7mqb@qq.com>

include $(INCLUDE_DIR)/package.mk

define Package/${PKG_NAME}
	SECTION:=net
	CATEGORY:=MMDVM
	TITLE:=MMDVM Host
	URL:=https://github.com/g4klx/MMDVMHost/
	DEPENDS:=+libpthread +libstdcpp +ysf-clients +p25-clients +nxdn-clients +ircddb-gateway +dapnet-gateway
	USERID:=mmdvm:mmdvm
endef

define Package/${PKG_NAME}/description
The host program for the MMDVM
endef

TARGET_CFLAGS += -std=c++0x -DOPENWRT

ifeq ($(ARCH),mips)
	TARGET_CFLAGS += -DWORDS_BIGENDIAN=1
	TARGET_CPPFLAGS += -DWORDS_BIGENDIAN=1
endif

TARGET_LDFLAGS += \
    -Wl,-rpath-link=$(STAGING_DIR)/usr/lib \

MAKE_FLAGS +=\
    CFLAGS="$(TARGET_CFLAGS) $(TARGET_CPPFLAGS)" \
    LDFLAGS="$(TARGET_LDFLAGS)" \

define Package/${PKG_NAME}/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/MMDVMHost $(1)/usr/sbin/
	$(CP) -a files/* $(1)/
endef

define Package/${PKG_NAME}/conffiles
/etc/MMDVM.ini
/etc/getdmrid
/etc/crontabs/root
endef

# define Package/${PKG_NAME}/postinst
# #!/bin/sh
# [ ! -f /etc/config/mmdvm ] && touch /etc/config/mmdvm
# [ -z `uci -q get mmdvm.DMR.Enable` ] && {
# 	uci set mmdvm.DMR=mmdvmhost
# 	uci set mmdvm.DMR.Enable=0
# 	uci commit mmdvm
# }
# exit 0
# endef

$(eval $(call BuildPackage,${PKG_NAME}))

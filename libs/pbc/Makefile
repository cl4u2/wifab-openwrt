#
# Copyright (C) 2017 Claudio Pisa <claudio.pisa@uniroma2.it>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
# 

include $(TOPDIR)/rules.mk

PKG_NAME:=pbc
PKG_VERSION:=0.5.14
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://crypto.stanford.edu/pbc/files/pbc-0.5.14.tar.gz
PKG_MD5SUM:=842b85c50ba1464b207fc7b7a1f6ac18
PKG_MAINTAINER := Claudio Pisa <claudio.pisa@uniroma2.it>
PKG_BUILD_DEPENDS:=+libgmp +libreadline +libncurses

include $(INCLUDE_DIR)/host-build.mk
include $(INCLUDE_DIR)/package.mk

define Package/pbc
  SECTION:=libs
  CATEGORY:=Libraries
  DEPENDS:=+libgmp +libncurses
  TITLE:=pbc library.
endef

CLFAGS += -fPIC

CONFIGURE_VARS += LDFLAGS=" -L$(STAGING_DIR)/usr/lib/ "
OURLDLIBS=" -lgmp -lm -lncurses "

define Build/Compile
	$(call Build/Compile/Default, -C $(PKG_BUILD_DIR) LDLIBS=$(OURLDLIBS) -f simple.make)
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_BUILD_DIR)/include/* $(1)/usr/include/
	$(INSTALL_DIR) $(1)/usr/include/pbc
	$(CP) $(PKG_BUILD_DIR)/include/* $(1)/usr/include/pbc
	
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/libpbc{.a,.so*} $(1)/usr/lib/
endef


define Package/pbc/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/libpbc.a   $(1)/usr/lib/
	$(CP) $(PKG_BUILD_DIR)/libpbc.so  $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_BUILD_DIR)/include/*.h $(1)/usr/include/
endef

$(eval $(call BuildPackage,pbc))


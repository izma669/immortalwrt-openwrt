include $(TOPDIR)/rules.mk

PKG_NAME:=clx-s20p-files
PKG_VERSION:=1
PKG_RELEASE:=1
PKG_LICENSE:=GPL-2.0

PKG_MAINTAINER:=CLX S20P
PKG_BUILD_DEPENDS:=
PKGARCH:=all

include $(INCLUDE_DIR)/package.mk

define Package/clx-s20p-files
  SECTION:=base
  CATEGORY:=Base system
  TITLE:=CLX S20P board glue (wan1 naming, port order)
  PKGARCH:=all
endef

define Package/clx-s20p-files/description
 Board specific glue for the CLX S20P only:

  * renames the standalone 2.5G WAN netdev (gmac1, "eth1") to "wan1"
    before netifd starts, so that board.json, UCI and LuCI agree with the
    label printed on the case;
  * keeps the LuCI port overview in the physical order (wan1, lan6..lan1)
    by refreshing a local copy of 29_ports.js when it differs.
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
endef

define Build/Compile
endef

define Package/clx-s20p-files/install
	$(INSTALL_DIR) $(1)/etc/init.d $(1)/etc/rc.d $(1)/etc/uci-defaults
	$(INSTALL_DIR) $(1)/usr/share/clx-s20p
	$(INSTALL_BIN) ./files/wan1-rename $(1)/etc/init.d/wan1-rename
	$(LN) ../init.d/wan1-rename $(1)/etc/rc.d/S19wan1-rename
	$(INSTALL_BIN) ./files/99-clx-port-order $(1)/etc/uci-defaults/99-clx-port-order
	$(INSTALL_DATA) ./files/29_ports.js $(1)/usr/share/clx-s20p/29_ports.js
endef

$(eval $(call BuildPackage,clx-s20p-files))

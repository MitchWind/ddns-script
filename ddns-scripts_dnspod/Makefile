include $(TOPDIR)/rules.mk

PKG_NAME:=ddns-scripts_dnspod
PKG_VERSION:=1.0.2
PKG_RELEASE:=1

PKG_LICENSE:=GPLv2
PKG_MAINTAINER:=Small_5

PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)
	SECTION:=net
	CATEGORY:=Network
	SUBMENU:=IP Addresses and Names
	TITLE:=DDNS extension for Dnspod.com/Dnspod.cn
	PKGARCH:=all
	DEPENDS:=+ddns-scripts +wget +ca-certificates
endef

define Package/$(PKG_NAME)/description
	Dynamic DNS Client scripts extension for Dnspod.com/Dnspod.cn
endef

define Build/Configure
endef

define Build/Compile
	$(CP) ./*.sh $(PKG_BUILD_DIR)
	$(CP) ./*.json $(PKG_BUILD_DIR)
endef

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/usr/lib/ddns
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/*.sh $(1)/usr/lib/ddns

	$(INSTALL_DIR) $(1)/usr/share/ddns/default
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/*.json $(1)/usr/share/ddns/default/
endef


define Package/$(PKG_NAME)/prerm
	#!/bin/sh
	# if NOT run buildroot then stop service
	[ -z "$${IPKG_INSTROOT}" ] && /etc/init.d/ddns stop >/dev/null 2>&1
endef

$(eval $(call BuildPackage,$(PKG_NAME)))

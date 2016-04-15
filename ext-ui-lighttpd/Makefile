#
# Copyright (C) 2016
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=ext-ui-lighttpd
PKG_VERSION:=0.1
PKG_RELEASE:=2

include $(INCLUDE_DIR)/package.mk

define Package/ext-ui-lighttpd
  SECTION:=test
  CATEGORY:=test
  DEPENDS:=+curl +lighttpd +lighttpd-mod-access +lighttpd-mod-accesslog \
  +lighttpd-mod-auth +lighttpd-mod-cgi +lighttpd-mod-fastcgi \
  +lighttpd-mod-redirect +lighttpd-mod-rewrite +ndmq +php5 \
  +php5-cli +php5-fastcgi +php5-mod-curl +php5-mod-dom \
  +php5-mod-exif +php5-mod-gd +php5-mod-json +php5-mod-mbstring \
  +php5-mod-simplexml +php5-mod-xml +php5-mod-xmlreader \
  +php5-mod-xmlwriter +php5-mod-zip +vnstat
  TITLE:=Easy installation script for extended web UI
endef

define Package/ext-ui-lighttpd/description
 PHP version extended web user interface (ext-UI) for keenetic routers with NDMSv2
endef

define Build/Prepare
endef

define Build/Configure
endef

define Build/Compile
endef

define Package/ext-ui-lighttpd/install
	$(INSTALL_DIR) $(1)/opt/{etc,share}
	$(CP) ./files/{etc,share} $(1)/opt/
endef

define Package/ext-ui-lighttpd/postinst
#!/bin/sh

logger "Welcome to Extended GUI installer"

#logger "Creating system backup..."
#tar cvzf /opt/backup-`date "+%Y-%m-%d"`.tar.gz -C /opt/ etc share var

logger "Executing post-installation script..."
vnstat -u -i br0
vnstat -u -i eth2
vnstat -u -i eth2.1
vnstat -u -i eth2.2
vnstat -u -i ppp0
vnstat -u -i ra0

echo -n -e "\n Done! Pay your attention! The web-interfase login name \n\
    is root! Extended web UI will be available at following URL:\n\n\
    http://<ip_address_of_router>:88 \n\n\
    Do you wish to start extended web UI? [y]: "
read wish_to_start
[ -z "$$wish_to_start" ] && wish_to_start=y
if [ "$$wish_to_start" == "y" ]
then
    /opt/etc/init.d/S32vnstat start
    /opt/etc/init.d/S80lighttpd start
fi
endef

$(eval $(call BuildPackage,ext-ui-lighttpd))
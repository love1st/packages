# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NPM_NAME:=ffmpeg-for-homebridge
PKG_NAME:=node-$(PKG_NPM_NAME)
PKG_VERSION:=0.1.2
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NPM_NAME)-$(PKG_VERSION).tgz
PKG_SOURCE_URL:=https://mirrors.tencent.com/npm/$(PKG_NPM_NAME)/-/ \
                https://registry.npmjs.org/$(PKG_NPM_NAME)/-/
PKG_HASH:=841ac93e21930f0d000f410dbb7c0be6df88d7bc3f4c6c3aa48461fcdd84b986

PKG_MAINTAINER:=Hirokazu MORIKAWA <morikw2@gmail.com>
PKG_LICENSE:=none
PKG_LICENSE_FILES:=

PKG_BUILD_DEPENDS:=node/host

include $(INCLUDE_DIR)/package.mk

define Package/node-ffmpeg-for-homebridge
  SUBMENU:=Node.js
  SECTION:=lang
  CATEGORY:=Languages
  TITLE:=ffmpeg for homebridge
  URL:=https://www.npmjs.com/package/ffmpeg-for-homebridge
  DEPENDS:=+node +ffmpeg
endef

define Package/node-ffmpeg-for-homebridge/description
 Static ffmpeg binaries for Homebridge with support for audio (libfdk-aac) and hardware decoding (h264_omx).
endef

TAR_OPTIONS+= --strip-components 1
TAR_CMD=$(HOST_TAR) -C $(1) $(TAR_OPTIONS)

define Build/Compile
	# do nothing
endef

define Package/node-ffmpeg-for-homebridge/install
	$(INSTALL_DIR) $(1)/usr/lib/node/$(PKG_NPM_NAME)
	$(CP) $(PKG_BUILD_DIR)/package.json \
		$(1)/usr/lib/node/$(PKG_NPM_NAME)/
	$(CP) $(PKG_BUILD_DIR)/{README.md,index.js} \
		$(1)/usr/lib/node/$(PKG_NPM_NAME)/
	$(INSTALL_DIR) $(1)/usr/lib/node_modules
	$(LN) ../node/$(PKG_NPM_NAME) $(1)/usr/lib/node_modules/$(PKG_NPM_NAME)
endef

define Package/node-ffmpeg-for-homebridge/postrm
#!/bin/sh
rm /usr/lib/node_modules/ffmpeg-for-homebridge || true
rm -rf /usr/lib/node/ffmpeg-for-homebridge || true
endef

$(eval $(call BuildPackage,node-ffmpeg-for-homebridge))

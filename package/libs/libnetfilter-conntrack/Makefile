#
# Copyright (C) 2009-2013 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=libnetfilter_conntrack
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://git.netfilter.org/libnetfilter_conntrack
PKG_SOURCE_DATE:=2017-07-25
PKG_SOURCE_VERSION:=e870432649955d377a73ee5a72cb23f0f6b5e4c5
PKG_MIRROR_HASH:=6891e6bea956d5d3514524918f439dfe8b5806397d8d40d1afc69b9bfebc1d57

# dirty trick - build iptables first (so iptables does not depend om libnetfilter-conntrack
PKG_BUILD_DEPENDS:=iptables

PKG_MAINTAINER:=Jo-Philipp Wich <jo@mein.io>

PKG_FIXUP:=autoreconf
PKG_LICENSE:=GPL-2.0+

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/libnetfilter-conntrack
  SECTION:=libs
  CATEGORY:=Libraries
  DEPENDS:=+libnfnetlink +libmnl
  TITLE:=API to the in-kernel connection tracking state table
  URL:=http://www.netfilter.org/projects/libnetfilter_conntrack/
endef

define Package/libnetfilter-conntrack/description
 libnetfilter_conntrack is a userspace library providing a programming
 interface (API) to the in-kernel connection tracking state table. The
 library libnetfilter_conntrack has been previously known as
 libnfnetlink_conntrack and libctnetlink. This library is currently
 used by conntrack-tools among many other applications.
endef

TARGET_CFLAGS += $(FPIC)

CONFIGURE_ARGS += \
	--enable-static \
	--enable-shared \

define Build/InstallDev
	$(INSTALL_DIR) $(1)/opt/include/libnetfilter_conntrack
	$(CP) \
		$(PKG_INSTALL_DIR)/opt/include/libnetfilter_conntrack/*.h \
		$(1)/opt/include/libnetfilter_conntrack/

	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) \
		$(PKG_INSTALL_DIR)/opt/lib/libnetfilter_conntrack.{so*,a,la} \
		$(1)/opt/lib/

	$(INSTALL_DIR) $(1)/opt/lib/pkgconfig
	$(CP) \
		$(PKG_INSTALL_DIR)/opt/lib/pkgconfig/libnetfilter_conntrack.pc \
		$(1)/opt/lib/pkgconfig/
endef

define Package/libnetfilter-conntrack/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) \
		$(PKG_INSTALL_DIR)/opt/lib/libnetfilter_conntrack.so.* \
		$(1)/opt/lib/
endef

$(eval $(call BuildPackage,libnetfilter-conntrack))

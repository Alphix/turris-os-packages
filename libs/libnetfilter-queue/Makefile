#
# Copyright (C) 2007-2010 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=libnetfilter_queue
PKG_VERSION:=1.0.2
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:= \
	http://www.netfilter.org/projects/libnetfilter_queue/files/ \
	ftp://ftp.netfilter.org/pub/libnetfilter_queue/ \
	http://mirrors.evolva.ro/netfilter.org/libnetfilter_queue/
PKG_MD5SUM:=df09befac35cb215865b39a36c96a3fa

PKG_FIXUP:=autoreconf

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/libnetfilter-queue
  SECTION:=libs
  CATEGORY:=Libraries
  DEPENDS:=+libnfnetlink +libmnl +kmod-nfnetlink-queue +kmod-ipt-nfqueue
  TITLE:=API to packets queued by the kernel packet filter
  URL:=http://www.netfilter.org/projects/libnetfilter_queue/
endef

define Package/libnetfilter-queue/description
 libnetfilter_queue is a userspace library providing an API to packets
 that have been queued by the kernel packet filter.
endef

TARGET_CFLAGS += $(FPIC)

CONFIGURE_ARGS += \
	--enable-static \
	--enable-shared \

CONFIGURE_VARS += \
	LIBNFNETLINK_CFLAGS="$(TARGET_CPPFLAGS)" \
	LIBNFNETLINK_LIBS="$(TARGET_LDFLAGS)"

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include/libnetfilter_queue
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/include/libnetfilter_queue/*.h \
		$(1)/usr/include/libnetfilter_queue/

	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/libnetfilter_queue*.{so*,a,la} \
		$(1)/usr/lib/

	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/lib/pkgconfig/libnetfilter_queue.pc \
		$(1)/usr/lib/pkgconfig/
endef

define Package/libnetfilter-queue/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libnetfilter_queue*.so.* $(1)/usr/lib/
endef

$(eval $(call BuildPackage,libnetfilter-queue))

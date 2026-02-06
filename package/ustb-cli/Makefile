include $(TOPDIR)/rules.mk

PKG_NAME:=ustb-cli
PKG_VERSION:=1.3.10
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/Jason23347/ustb-cli-c.git
PKG_SOURCE_VERSION:=v$(PKG_VERSION)
# 启用 submodule：github_archive 不支持，会 fallback 到 rawgit；rawgit 打包时会包含这些 submodule
PKG_SOURCE_SUBMODULES:=external/cargs external/linenoise
PKG_MIRROR_HASH:=2041dc5044c411ad93f15485458599b0bf8ebee8b5885c37047617a91bf10063
# 跳过 mirror 下载，直接从 git clone（镜像站无此包时会卡住）
PKG_SOURCE_MIRROR:=1
PKG_MIRROR:=0

PKG_MAINTAINER:=Shuaicheng Zhu <jason23347@163.com>
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/ustb-cli
  SECTION:=net
  CATEGORY:=Network
  TITLE:=USTB campus network CLI
  DEPENDS:=+libopenssl
  URL:=https://github.com/Jason23347/ustb-cli-c
endef

define Package/ustb-cli/description
  USTB campus network command-line client (login, devices, speedtest, etc.)
endef

CMAKE_OPTIONS += \
	-DWITH_BALANCE=on \
	-DWITH_ACCOUNT=on \
	-DWITH_SPEEDTEST=on \
	-DWITH_COMPLETION=off \
	-DGB2312_DECODER=disabled \
	-DUSE_INTERACTIVE=off \
	-DUSE_THREADS=on \
	-DWITH_COLOR=on

# 不覆盖 Build/Prepare：rawgit 打包时已包含 submodule，解压后无 .git 无法再执行 git submodule

define Package/ustb-cli/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/ustb-cli $(1)/usr/bin/
endef

$(eval $(call BuildPackage,ustb-cli))

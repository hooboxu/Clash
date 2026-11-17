1. 相关链接
dae 官方 OpenWrt 软件源 — 支持的版本、架构与常见错误
honk 官方仓库-多点star
honk 配置（标准版） — 按服务分组，兜底组自动选节点
honk 配置（精简版） — 只有一个组，国内直连、其他走代理
上期：dae（大鹅）OpenWrt 保姆级教程
2. 命令
查看内核版本与架构（需内核 6.12 以上，x86_64 或 aarch64）
换行
折叠
复制
BASH
uname -rm
添加 dae 官方软件源（ImmortalWrt）
如果命令出现了问题，去参考顶部官方源网站去复制，这里不会维护。

换行
折叠
复制
BASH
wget -O /etc/apk/keys/daeuniverse.pem https://openwrt.daeuniverse.org/public-key.pem
. /etc/openwrt_release
FEED=https://openwrt.daeuniverse.org/${DISTRIB_RELEASE%.*}
cat > /etc/apk/repositories.d/daeuniverse.list <<EOF
@daeuniverse $FEED/packages/$DISTRIB_ARCH/packages.adb
EOF
apk update
添加 dae 官方软件源（官方 OpenWrt，多一行内核 BTF 源）
如果命令出现了问题，去参考顶部官方源网站去复制，这里不会维护。

换行
折叠
复制
BASH
wget -O /etc/apk/keys/daeuniverse.pem https://openwrt.daeuniverse.org/public-key.pem
. /etc/openwrt_release
FEED=https://openwrt.daeuniverse.org/${DISTRIB_RELEASE%.*}
cat > /etc/apk/repositories.d/daeuniverse.list <<EOF
@daeuniverse $FEED/packages/$DISTRIB_ARCH/packages.adb
@daeuniverse $FEED/kmods/$DISTRIB_RELEASE/$DISTRIB_TARGET/packages.adb
EOF
apk update
安装 honk 与 LuCI 界面
换行
折叠
复制
BASH
apk add honk@daeuniverse luci-app-honk@daeuniverse luci-i18n-daeuniverse-zh-cn@daeuniverse
doona 面板地址（首次打开创建管理员）
换行
折叠
复制
APACHE
http://路由器IP:9090/ui/


增加host
echo "192.168.1.110 nas.yoikoto.cn" >> /etc/hosts
/etc/init.d/honk restart
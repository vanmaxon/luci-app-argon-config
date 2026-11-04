# Argon 配置兼容包

[English](README.md) · 简体中文

Argon 3.0 已将设置页、背景、Logo 和 RPC 服务集成到 [luci-theme-argon](https://github.com/jerrykuku/luci-theme-argon)。本仓库的 master 现在提供 **3.0 空迁移包**，沿用 `luci-app-argon-config` 包名，不再安装这些文件或独立语言包。

编译新固件只需选择 `luci-theme-argon`。已有构建脚本若仍克隆本仓库，更新到本次兼容包后可保留原包名；同一构建树中只保留一份包定义，不要同时引入主题仓库中的同名迁移包。旧版 1.0 插件与 3.0 主题同时安装会产生 `trying to overwrite ... owned by luci-theme-argon` 错误。

已有路由器从旧独立插件迁移时，先升级本空迁移包，再安装同次发行的 3.0 主题。迁移包先备份旧配置，主题恢复设置；无需先卸载旧插件。完整命令见[主题迁移说明](https://github.com/jerrykuku/luci-theme-argon/blob/master/README_ZH.md#安装)。

翻译包 `luci-i18n-argon-config-*` 由主题仓库提供。Argon 2.x 与更早的主题不应使用此空迁移包；旧独立插件源码保留在提交 `445af53fbee6e00fa6efc0ae33f8b2854df65500`，18.06 分支维持原有用途。

## OpenWrt 25.12 和在线壁纸

本仓库的构建流程使用 OpenWrt 25.12.5 SDK 生成 APK 包，并固定搭配[主题 fork](https://github.com/vanmaxon/luci-theme-argon)。构建产物包含主题、迁移包和语言包。要使用下述 Waifu 功能，请使用本仓库 Actions 构建产物或本 fork 的发行包，而非上游主题发行包。全新安装只需主题，使用 APK v3 的路由器先执行 `apk update`，再安装下载的主题包：

```sh
apk add --allow-untrusted ./luci-theme-argon-*.apk
```

如果已安装旧版独立配置插件，请先按照上面的主题迁移说明安装对应的迁移包，再安装主题。需要中文界面时，还可安装同一发行版的 `luci-i18n-argon-config-zh-cn` APK。

在 **系统 → Argon Config** 的壁纸来源中选择 **Unsplash** 或 **Wallhaven**，保存并应用。Unsplash 需要在页面中填写从 [Unsplash Developers](https://unsplash.com/developers) 获取的 Access Key；Wallhaven 的普通随机壁纸不需要密钥。路由器需要能访问对应服务，浏览器也需要能访问返回的图片地址。请求失败时会回退到本地背景；在线图片地址通常缓存 12 小时。

选择 **Waifu (NEKOS.BEST / Wallhaven)** 可使用全年龄二次元图片，无需密钥：竖屏优先使用 NEKOS.BEST，横屏使用 Wallhaven 动漫分类。Unsplash、Wallhaven 和 Waifu 会随浏览器窗口横竖方向切换对应壁纸；Bing 和本地背景保持原有方式。Waifu.im 曾公告停止服务，未用作图片源。主题内的上游在线更新可能覆盖这些改动，请使用本 fork 构建的主题包更新。

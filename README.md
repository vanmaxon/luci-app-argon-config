# Argon configuration compatibility package

English · [简体中文](README_ZH.md)

Argon 3.0 includes its settings page, backgrounds, branding and RPC services in [luci-theme-argon](https://github.com/jerrykuku/luci-theme-argon). This repository's master branch now supplies an **empty 3.0 migration package** under the existing `luci-app-argon-config` name. It no longer installs these files or separate translations.

New firmware only needs `luci-theme-argon`. Existing scripts that clone this repository can retain the package name after updating to the migration package. Keep exactly one package definition in the build tree; do not also include the theme repository's copy. The old 1.0 plugin conflicts with the integrated theme and causes `trying to overwrite ... owned by luci-theme-argon` errors.

On an existing router, upgrade to the empty migration package first, then install the 3.0 theme from the same release. The migration package backs up old settings for the theme to restore. Do not uninstall the old plugin first. See the [theme's migration instructions](https://github.com/jerrykuku/luci-theme-argon/blob/master/README.md#installation).

The theme repository supplies `luci-i18n-argon-config-*` translations. Argon 2.x and earlier themes should not use this empty package; the standalone plugin remains available at commit `445af53fbee6e00fa6efc0ae33f8b2854df65500`. The 18.06 branch retains its existing purpose.

## OpenWrt 25.12 and online wallpapers

The build uses the OpenWrt 25.12.5 SDK to produce APK packages together with the pinned Argon 3.1.2 theme. Artifacts contain the theme, migration package and translations; matching packages are also available from the [theme releases](https://github.com/jerrykuku/luci-theme-argon/releases). A fresh install only needs the theme. On a router using APK v3, run `apk update`, then install the downloaded theme:

```sh
apk add --allow-untrusted ./luci-theme-argon-*.apk
```

If the old standalone configuration plugin is installed, follow the theme migration instructions above and install the matching migration package before the theme. Install the appropriate `luci-i18n-argon-config-<language>` APK from the same release for translations.

Under **System → Argon Config**, choose **Unsplash** or **Wallhaven** as the wallpaper source, then save and apply. Unsplash requires an Access Key from [Unsplash Developers](https://unsplash.com/developers); ordinary random Wallhaven wallpapers do not require a key. The router must be able to reach the service and the browser must be able to reach the returned image URL. Failed requests fall back to a local background; online image URLs are normally cached for 12 hours.

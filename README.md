# flint3-packages

Signed apk package feeds for the GL.iNet GL-BE9300 (Flint 3) images built from
[Zakkaus/openwrt-flint3](https://github.com/Zakkaus/openwrt-flint3) and
[Zakkaus/immortalwrt-flint3](https://github.com/Zakkaus/immortalwrt-flint3). Each feed holds the
packages of one build, kernel modules included, signed with the key its images trust.

The feeds match the released images `flint3-20261120-2` (OpenWrt) and `flint3-20261120`
(ImmortalWrt), both booted on a GL-BE9300 on 2026-11-20. Kernel modules install only on an image
with the same kernel package version.

| Directory | Images | Signing key, sha256 of the DER public key |
| --- | --- | --- |
| `openwrt/` | `openwrt-*` from openwrt-flint3 | `3e3c6b58f7671aad0de438b9dd864fb9986fac83e1fa350eadb0936c117849f1` |
| `immortalwrt/` | `immortalwrt-*` from immortalwrt-flint3 | `5532a06a1cf888980ba08ad118d12c0a1288b05b6544bf0d3890ddafa39c3635` |

Each directory also holds the key as `public-key.pem`.

## Use

The images already list their feed in `/etc/apk/repositories.d/distfeeds.list` and trust its key,
so `apk update`, `apk add` and the LuCI software page work without changes. The OpenWrt image
lists these lines; the ImmortalWrt image lists the same lines with `immortalwrt` in place of
`openwrt`:

```
https://zakkaus.github.io/flint3-packages/openwrt/targets/qualcommbe/ipq53xx/packages/packages.adb
https://zakkaus.github.io/flint3-packages/openwrt/packages/aarch64_cortex-a53/base/packages.adb
https://zakkaus.github.io/flint3-packages/openwrt/packages/aarch64_cortex-a53/luci/packages.adb
https://zakkaus.github.io/flint3-packages/openwrt/packages/aarch64_cortex-a53/packages/packages.adb
```

The images also list the `routing`, `telephony` and `video` feeds, commented out: the builds
select no package from them, so these feeds hold no index.

## Kernel modules

A feed holds only the newest published build. Kernel module packages (`kmod-*`) install only on
the image of that build, because they must match its kernel. Upgrade the router to the newest image
of the same source before installing a kernel module.

## This branch

`gh-pages` is a published artifact, not a source branch. Each publish replaces one source's
directory and force-pushes the branch as a single new commit, so old packages do not pile up and
no history is kept. Do not commit to it by hand.

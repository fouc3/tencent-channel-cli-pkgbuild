# tencent-channel-cli-pkgbuild

Arch Linux 用 PKGBUILD：把腾讯官方 `tencent-channel-cli`（npm 上的**预编译 Go 二进制**）重打包为 pacman 包 `tencent-channel-cli-bin`。

- 上游 CLI：npm `tencent-channel-cli` / 平台包 `tencent-channel-cli-linux-x64`（官方入口 <https://connect.qq.com/ai>）
- 配套 Skill：https://github.com/fouc3/tencent-channel-community/tree/dsh-adaptation （DSH 适配分支）
- 当前版本：`tencent-channel-cli-bin 1.0.10-1`（x86_64）

## 用法

```bash
makepkg -f
sudo pacman -U tencent-channel-cli-bin-1.0.10-1-x86_64.pkg.tar.zst
tencent-channel-cli version && tencent-channel-cli doctor
```

## 设计取舍

- 只取平台包内的 `bin/tencent-channel-cli`（静态链接、无运行时依赖），不含 npm 元包的 node 转发脚本
- `provides/conflicts=tencent-channel-cli`，避免与 npm 全局安装并存
- `options=('!strip' '!debug')`：上游二进制已 stripped，无需二次处理
- `namcap` 预期仅剩两条上游固有警告（lacks PIE / FULL RELRO）

## 许可提醒

上游 npm 包**未声明任何 license 字段**，因此本包标为 `LicenseRef-custom`，
随包安装 `/usr/share/licenses/tencent-channel-cli-bin/LICENSE` 说明权属归腾讯。
二进制版权归腾讯；若计划公开分发该包，请先自行确认上游许可条件。

## 升级流程

见 `BUILD.md`。

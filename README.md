# Grok Bot 安装包（私有镜像）

公开镜像，便于手机端免登录下载；仅供个人设备侧载试用。

| 项 | 值 |
|---|---|
| 应用 | Grok Bot（xAI / X Corp） |
| 包名 | `ai.x.grok.bot` |
| 版本 | 1.19.1（versionCode 3050） |
| 格式 | `.xapk` —— 拆分安装包，**不是**单个可点装的 APK |
| 大小 | 93.74 MB |
| 导入来源 | Google Play 应用包，经 APKPure 导出 |

## 为什么不能直接点安装

1. `base.apk`（63.57 MB）内**没有 `lib/` 目录**，原生库全在拆分包里；
2. AndroidManifest 声明 `requiredSplitTypes = base__abi, base__density`，只装 base 会被系统拒绝（`INSTALL_FAILED_MISSING_SPLIT`）；
3. 该 XAPK 只含 **32 位** ARM 库（`config.armeabi_v7a`），**没有 arm64-v8a**。

## 安装方式（纯血鸿蒙）

1. 应用市场安装「卓易通」；
2. 在卓易通容器内安装一个拆分安装器（SAI / Split APKs Installer，或 APKMirror Installer）；
3. 把 `grokbot-1.19.1.xapk` 放到容器可读目录（`我的手机 > sharedata > download`）；
4. 用安装器打开 xapk，按提示安装全部拆分。

## 已知风险

- 应用内含 Google Play **PairIP 完整性保护**（`libpairipcore.so`）、`CHECK_LICENSE` 与 Play Billing；
- 无 GMS 环境下，Google 登录、订阅内购、FCM 推送很可能异常；
- 32 位库在 arm64 容器上可能报 `NO_MATCHING_ABIS`；
- 合并/重签 APK 会破坏官方签名，几乎必然触发完整性校验失败，不建议。
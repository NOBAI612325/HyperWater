⁢
```
```
# HyperWater
为\*\*澎湃OS 4（HyperOS 4）\*\*中未开放「高级材质 / 柔光玻璃」的小米、红米机型，提供一条可逆的开启方案。
⁢
## 下载
预编译 APK 见 GitHub Releases：
<https://github.com/NOBAI612325/HyperWater/releases>
⁢
## 它做什么
| 步骤 | 内容 |
| --- | --- |
| 1 | 写入 23 个 `persist.sys` 属性，含原机缺失的总门控 `persist.sys.bionic_material_supported` |
| 2 | 写入 3 个 `Settings.Secure`：`background_blur_enable`、`material_style_selected`、`material_style` |
| 3 | 逐项 `getprop` / `settings get` 读回验证，未生效的会列出来 |
| 4 | 自动重启设置进程，让 `<clinit>` 里缓存的门控重新读取 |
| 5 | 可一键恢复全部原始值 |
**不写** `/system`、`/vendor`、`/boot`，**不**替换系统 APK，**不** Hook `system_server`。
## 环境要求
- 澎湃OS 4：`ro.mi.os.version.code = 4`
- 硬件支持背景模糊：`ro.surface_flinger.supports_background_blur = 1`
- 可用 root（临时 root 即可）
打开应用第一屏会显示**只读兼容性自检**。
## 从源码构建
```
# JDK 17 + Android SDK 34 + Gradle 8.x
gradle :app:assembleRelease
# 产物
# app/build/outputs/apk/release/app-release.apk
```
⁢
## 免责声明
- 柔光玻璃是实时渲染效果，官方对硬件有门槛；在未适配的老机型上强开 可能带来耗电、发热或掉帧。
- 本项目只写 `persist.*` 属性与 `Settings.Secure`，可完整还原， 但不承诺对所有 ROM 版本、所有第三方模块组合都有效。
- 使用本项目产生的任何风险由使用者自行承担。
## License
[MIT](LICENSE)
⁢
⁢
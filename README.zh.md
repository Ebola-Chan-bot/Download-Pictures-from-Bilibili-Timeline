English Version: [README.md](README.md)

# 从“Bilibili动态”页面下载图片和视频
用于从“BiliBili动态”时间线页面上下载图片的Tampermonkey脚本，也可以在时间线和播放页面下载视频。
下载视频时，可下载最高质量的视频和音频分轨，并通过ffmpeg.wasm**完全在浏览器**中合并为单个MP4文件。
可以在设置窗口里自定义下载的文件名。图片默认以动态标题命名（`{title}.{ext}`）：无标题时用原文件名，重名时自动追加原文件名作后缀，避免相互覆盖。
可以在设置窗口里按图片方向过滤（横图／方图／竖图）：封面被过滤则整条跳过（不发请求）；封面通过后内部图再逐张按方向过滤，不符合的不下载（无宽高元数据的图放行）；判断只用接口／页面元数据和已加载的缩略图，绝不发送额外网络请求。连续下载间隔仅对产生真实下载的动态生效，被过滤跳过的动态不等待间隔。
可以自动连续下载时间线动态中的图片和视频。连续下载期间会自动保持标签页后台活跃（下载间隔计时在 Worker 中运行不受后台节流，并播放几乎不可闻的低音量音频豁免浏览器冻结/节能丢弃，标签页可能显示小喇叭图标），切到其它标签页下载也不会暂停；下载结束或停止后自动关闭。
也支持UP主个人空间的“投稿-图文”页（`space.bilibili.com/<uid>/upload/opus`）：每张卡片上有下载按钮，也可自动连续下载整个瀑布流；专栏型图文会抓取正文中的全部图片（而非仅封面）。
可在设置中选择“直接保存到指定文件夹”（仅Chromium系浏览器，如Chrome/Edge）：授权一次后，图片和视频直接写入所选目录，不经过浏览器下载、无逐张保存弹窗；不支持或未授权时自动退回浏览器下载。

## 下载:
- 前往[Greasy Fork](https://greasyfork.org/zh-CN/scripts/421885)。
- 或前往[发布页面](https://github.com/owendswang/Download-Pictures-from-Bilibili-Timeline/releases)。

## 使用平台：
（仅列出了我测试并使用的平台版本。）
- **Tampermonkey** (测试于v5.4.1)
- Firefox (测试于v150.0.2 64-bit)
- Windows 10 22H2，Windows 11 24H2 (我测试用的版本)

## 安装方法:
从[Greasy Fork](https://greasyfork.org/zh-CN/scripts/421885)直接安装。

或手动安装：
1. 下载最新的ZIP包 (从[这里](https://github.com/owendswang/Download-Pictures-from-Bilibili-Timeline/releases)下载).
2. 打开Tampermonkey -> 切换至'实用工具'选项卡. -> 选择'压缩包' -> '导入': 浏览 -> 选择刚下载的ZIP文件 -> 选择'安装'。

## 使用方法：
- 第一次使用本脚本，会自动弹出设置页面，修改或维持默认设置，点击确认保存设置即可。  
  （如果改变了“开启视频下载”功能，会在保存设置时，自动刷新页面。）  
![截图](res/1.PNG?raw=true)
- “设置”按钮和“下载当前瀑布流”按钮在页面左上角。  
![截图](res/2.PNG?raw=true)
- 最好关闭浏览器设置中的这个选项，不然下载多文件时，会不停弹出保存位置窗口。  
![截图](res/7.png?raw=true)

## 页面截图:
![截图](res/4.png?raw=true)  
![截图](res/3.png?raw=true)  
![截图](res/5.PNG?raw=true)  
![截图](res/6.png?raw=true)

## 特别鸣谢：
[SocialSisterYi/bilibili-API-collect](https://github.com/SocialSisterYi/bilibili-API-collect)

## 第三方许可证
本项目使用了以下第三方库：

### ffmpeg.wasm
- 包名：[@ffmpeg/ffmpeg](https://www.jsdelivr.com/package/npm/@ffmpeg/ffmpeg)
- 许可证：MIT
- 仓库：[ffmpegwasm/ffmpeg.wasm](https://github.com/ffmpegwasm/ffmpeg.wasm)

### FFmpeg WebAssembly 核心
- 包名：[@ffmpeg/core](https://www.jsdelivr.com/package/npm/@ffmpeg/core)
- 许可证：GPL-2.0-or-later
- 描述：FFmpeg 多媒体框架的 WebAssembly 构建版本
- 原始项目：[https://ffmpeg.org/](https://ffmpeg.org/)

ffmpeg.wasm 的 JavaScript 封装部分采用 MIT 许可证发布。
FFmpeg WebAssembly 核心源自 FFmpeg 的 C 语言代码库，
并根据上游项目的规定继续采用 GPL-2.0-or-later 许可证。

本用户脚本 **未对** FFmpeg 或其 WebAssembly 二进制文件进行任何修改；
仅在浏览器中加载并调用上游提供的构建版本。
FFmpeg WebAssembly 二进制文件从上游项目下载，并可能在本地缓存以提高性能。

## 许可证
由于本仓库包含 FFmpeg WebAssembly，本仓库作为一个整体分发时，采用 GPL-2.0 许可证。
除非另有说明，本项目原创代码采用 MIT 许可证。
第三方组件保留其各自的许可证。

**中文介绍：[README.zh.md](README.zh.md)**

# Download Pictures and Videos from Bilibili Timeline
A Tampermonkey script to download pictures from Bilibili timeline. Also able to download videos from timeline and play page.
It could download Bilibili DASH video/audio streams in highest quality available and merges them into a single MP4 file **entirely in the browser** using ffmpeg.wasm.
The filenames could be modified as you like in the settings pannel. Pictures are named after the dynamic title by default (`{title}.{ext}`): the original filename is used when there is no title, and automatically appended as a suffix on name collisions to avoid overwriting.
Posts can be filtered by cover-picture orientation (landscape / square / portrait) in the settings panel: only the cover is checked, a filtered cover skips the whole post while a passing cover downloads all its pictures; orientation is determined solely from API metadata or already-loaded thumbnails, never sending extra network requests. The auto-download interval applies only to posts that actually download files; filtered posts are skipped without waiting.
Able to download from timeline one by one automatically. During auto-download the tab is kept active in the background (interval timers run in a Worker immune to background throttling, and a nearly inaudible low-volume audio keeps the tab exempt from browser freezing / memory-saver discarding, so a speaker icon may appear on the tab); switching to other tabs will not pause the download, and the keep-alive stops automatically when the download finishes or is stopped.
Also supports the uploader's opus page (`space.bilibili.com/<uid>/upload/opus`): per-card download buttons on the picture grid, waterfall auto-download, and full-body picture extraction for article-type opus.
Optional "save directly to a chosen folder" mode (Chromium-based browsers only, e.g. Chrome/Edge): after granting access once, files are written straight into the folder without browser downloads or per-file save prompts; falls back to browser downloads when unsupported or unauthorized.

## Download:
- Go to [Greasy Fork](https://greasyfork.org/zh-CN/scripts/421885).

Or
- Go to [Release Page](https://github.com/owendswang/Download-Pictures-from-Bilibili-Timeline/releases).

## Platform:
(Only listed those versions I tested. You could try it on other platforms by yourself.)
- **Tampermonkey** (tested on v5.4.1)
- Firefox (tested on v150.0.2 64-bit)
- Windows 10 22H2, Windows 11 24H2 (which I tested on)

## Installation:
Install from [Greasy Fork](https://greasyfork.org/zh-CN/scripts/421885).

Or Install manually:
1. Download the newest release ZIP file (from [here](https://github.com/owendswang/Download-Pictures-from-Bilibili-Timeline/releases)).
2. Open Tampermonkey. -> Switch to 'Utilities' tab. -> 'Zip' -> 'Import': Browse -> Choose the ZIP file -> 'Install'.

## Usage:
- If opened for the first time, the 'Settings Panel' would show up. Change the settings as you like or leave it there as default. Press 'OK' to save your settings.  
  (If the 'Enable video download' setting changed, the page would reload to make it effective.)  
![Screenshot](res/1.PNG?raw=true)
- The button to call out the settings panel and the button to auto download current timeline arge at the top-left corner on the webpage.  
![Screenshot](res/2.PNG?raw=true)
- It's better to uncheck this settings of the web browser. Otherwise, it would keep popping up for saving location.  
![Screenshot](res/7.png?raw=true)

## Screenshot:
![Screenshot](res/4.png?raw=true)  
![Screenshot](res/3.png?raw=true)  
![Screenshot](res/5.PNG?raw=true)  
![Screenshot](res/6.png?raw=true)  

## Special Thanks:
[SocialSisterYi/bilibili-API-collect](https://github.com/SocialSisterYi/bilibili-API-collect)

## Third-Party Licenses
This project uses the following third-party libraries:

### ffmpeg.wasm
- Package: [@ffmpeg/ffmpeg](https://www.jsdelivr.com/package/npm/@ffmpeg/ffmpeg)
- License: MIT
- Repository: [ffmpegwasm/ffmpeg.wasm](https://github.com/ffmpegwasm/ffmpeg.wasm)

### FFmpeg WebAssembly Core
- Package: [@ffmpeg/core](https://www.jsdelivr.com/package/npm/@ffmpeg/core)
- License: GPL-2.0-or-later
- Description: WebAssembly build of the FFmpeg multimedia framework
- Original Project: [https://ffmpeg.org/](https://ffmpeg.org/)

The ffmpeg.wasm JavaScript wrapper is licensed under the MIT License.
The FFmpeg WebAssembly core is derived from the FFmpeg C codebase and
remains licensed under GPL-2.0-or-later, according to the upstream project.

This userscript does **not modify** FFmpeg or its WebAssembly binaries;
it only loads and invokes the upstream builds in the browser.
The FFmpeg WebAssembly binaries are downloaded from upstream sources
and may be cached locally for performance purposes.

## License
This repository, as distributed as a whole, is licensed under GPL-2.0 due to the inclusion of FFmpeg WebAssembly.
Unless otherwise stated, the original code authored for this project is licensed under the MIT License.
Third-party components retain their respective licenses.

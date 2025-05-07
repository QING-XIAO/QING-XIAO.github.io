---
layout:     post                         # 使用的布局（不需要改）
title:      视频下载方案               #标题 
subtitle:   Video & Audio Downloader.              # 副标题
date:       2025-05-06				     # 时间
author:     QING-XIAO                    # 作者
header-img: //raw.githubusercontent.com/QING-XIAO/giscus-comments/main/img/background/img4.jpg	                #这篇文章标题背景图片
catalog: true 						     # 是否归档
tags:								     #标签
    - Video&Audio
---

> 介绍两种从Bilibili & Youtube上下载视频的解决方案

### <a href="https://www.internetdownloadmanager.com/" target="_blank">IDM</a>
- #### Bilibili
> 只需要在IDM里添加 **M4S**、**XS**两种文件类型, IDM即可在网页中嗅探出可下载链接
>
> **NOTE:** 视频和音频是分开下载的后续还要用 **ffmpeg** 工具进行合并

  ```
  下载 == 选项 == 常规 == 自定义浏览器中的IDM下载浮动条 == 添加 == M4S、XS
  ```

- #### Youtube
> IDM可以说是Youtube视频下载利器, 各种分辨率都可以嗅探出来, 但是最近YT和IDM好像杠上了要么浮动条识别不出来要么只能下载360p视频, 若不能正常使用则试试 **yt-dlp**

![1](https://raw.githubusercontent.com/QING-XIAO/giscus-comments/main/img/post/20250506/img1.jpg)

### <a href="https://github.com/yt-dlp/yt-dlp" target="_blank">yt-dlp</a>
> yt-dlp 是一款功能丰富的命令行音频/视频下载器，支持数千个网站, 巨NB!!!

- #### 环境准备
> 1.安装 <a href="https://www.python.org/downloads/release/python-3913/" target="_blank">Python3.9+</a> 版本
>
> 2.安装 <a href="https://ffmpeg.org/download.html" target="_blank">FFmpeg</a>（用于音视频合并）
>
> 3.安装 <a href="https://github.com/yt-dlp/yt-dlp/releases" target="_blank">yt-dlp.exe</a>
>
> **Note:** 务必要将Python、FFmpeg、yt-dlp所在目录添加到 **系统环境变量**.

- #### 使用方法
> 列出每个视频的可用格式

  ```
  -F, --list-formats              List available formats of each video.
  ```
> 视频下载（可指定Video+Audio格式）

  ```
  -f, --format FORMAT             Video format code
  ```
> 调用cookies文件(B站不调用cookies最高只能下载1080p FPS30的视频)
>
> 使用插件 <a href="https://www.crxsoso.com/webstore/detail/hlkenndednhfkekhgcdicdfddnkalmdm" target="_blank">Cookie-Editor</a> 将cookies导出为Netscape格式.

  ```
  --cookies FILE                  Netscape formatted file to read cookies from and dump cookie jar in.

  如若遇到如下报错, 要检查复制的文件路径是否包含了 U+202A 隐形字符
  OSError: [Errno 22] Invalid argument: '\u202aC:/Users/QING/Desktop/cookies.txt'****
  ```

> 手动更新版本（需管理员权限）

  ```
  yt-dlp -U
  ```


  ```
  自用命令如下:

  yt-dlp --cookies "D:\RuanJian\yt-dlp\cookies.txt" -F "https://www.bilibili.com/video/BV1Q5cWeyEZe/?spm_id_from=333.337.search-card.all.click&vd_source=edb895583eda476ea7670a1d9f216861"

  yt-dlp --cookies "D:\RuanJian\yt-dlp\cookies.txt" -f 30116+30280 --merge-output-format mp4 -o "D:/QING/Downloads/%(title)s.%(ext)s" "https://www.bilibili.com/video/BV1Q5cWeyEZe/?spm_id_from=333.337.search-card.all.click&vd_source=edb895583eda476ea7670a1d9f216861"
  ```

> 最终结果如图
![2](https://raw.githubusercontent.com/QING-XIAO/giscus-comments/main/img/post/20250506/img2.jpg)
---

  ![ByeBye](/img/thank-you.jpg "Thank you!")
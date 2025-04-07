---
layout:     post   				    # 使用的布局（不需要改）
title:      Blog中引用另一个Github库中的图片 				# 标题 
subtitle:   Image url. #副标题
date:       2025-04-06 				# 时间
author:     QING-XIAO						# 作者
header-img: //raw.githubusercontent.com/QING-XIAO/giscus-comments/main/img/background/img1.jpg	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签
    - Picture
---

博客是基于GitHub Pages搭建的, 没有搞图床所以文章的背景图以及内部引用的图片都存储在GitHub仓库, 但Github仓库貌似有限制空间不能>1GB, 那就多建立几个仓库用来存放img就是了, 开搞!

> PS: 我认为其实不这么搞也绝对绝对够用了, 能更多少文章啊🤣🤣🤣

### 背景图部分
这部分 ```header-img``` 是YAML语法不能按照Markdown格式来写, 直接写 ```图片的URL``` 就可以.

- #### 第一次尝试
```
header-img: https://raw.githubusercontent.com/QING-XIAO/giscus-comments/main/img/background/img1.jpg
```
没有正常加载出背景图, 在 ```控制台``` == ```Network``` 找到 ```img1.jpg``` 可以看到返回的结果是 ```404```, 检查发现RequestURL的地址不正确, 前半部分多了GitHub Pages的地址
```
RequestURL: https://qing-xiao.github.io/https://raw.githubusercontent.com/QING-XIAO/giscus-comments/main/img/background/img1.jpg
```
![img4.jpg](https://raw.githubusercontent.com/QING-XIAO/giscus-comments/main/img/post/20250406/img4.jpg)

- #### 第二次尝试
将 ```header-img``` 改用 **绝对路径协议头**, OK 背景图成功加载出来.
```
header-img: //raw.githubusercontent.com/QING-XIAO/giscus-comments/main/img/background/img1.jpg
```

### 文章内图片
这没什么好说的直接用Markdown格式来写就ok, 唯一值得注意的就是检查好图片的URL即可.
```
![img2.jpg](https://raw.githubusercontent.com/QING-XIAO/giscus-comments/main/img/post/20250406/img2.jpg)
```
![img2.jpg](https://raw.githubusercontent.com/QING-XIAO/giscus-comments/main/img/post/20250406/img2.jpg)

### 获取图片Raw URL
在Github仓库内直接复制图片链接所获取的不是图片的真实地址, 需要转换格式不过可以搭配下面的油猴脚本来自动转换为图片的Raw URL
> PS: 有点小问题就是访问图片脚本不会自动执行每次都需要刷新一下页面才行

```javascript
// ==UserScript==
// @name         GitHub 图片 URL 重定向并添加复制按钮
// @namespace    https://github.com/
// @version      0.2
// @description  将 GitHub 图片 URL 重定向为原始格式，并在图片上添加复制按钮
// @author       QING-XIAO
// @match        https://github.com/*/*/blob/*
// @grant        GM_setClipboard
// ==/UserScript==

(function() {
    'use strict';

    // 获取当前页面的 URL
    const currentUrl = window.location.href;

    // 使用正则表达式提取仓库名、分支名和文件路径
    const regex = /https:\/\/github\.com\/([^\/]+)\/([^\/]+)\/blob\/([^\/]+)\/(.+)/;
    const match = currentUrl.match(regex);

    if (match) {
        const username = match[1];
        const repoName = match[2];
        const branchName = match[3];
        const filePath = match[4];

        // 构建原始图片的 URL
        const rawUrl = `https://raw.githubusercontent.com/${username}/${repoName}/${branchName}/${filePath}`;

        // 查找页面中的所有图片元素
        const images = document.querySelectorAll('img');

        images.forEach(img => {
            // 获取图片的 src 属性
            const imgSrc = img.src;

            // 如果图片的 src 包含当前仓库和分支的信息
            if (imgSrc.includes(`github.com/${username}/${repoName}/blob/${branchName}`)) {
                // 将图片的 src 替换为原始图片的 URL
                img.src = rawUrl;

                // 创建复制按钮
                const copyButton = document.createElement('button');
                copyButton.textContent = '复制 URL';
                copyButton.style.position = 'absolute';
                copyButton.style.top = '0';
                copyButton.style.left = '0';
                copyButton.style.zIndex = '1000';
                copyButton.style.backgroundColor = 'rgba(0, 0, 0, 0.5)';
                copyButton.style.color = '#fff';
                copyButton.style.border = 'none';
                copyButton.style.padding = '5px';
                copyButton.style.cursor = 'pointer';

                // 将按钮添加到图片的父元素
                img.parentElement.style.position = 'relative';
                img.parentElement.appendChild(copyButton);

                // 添加点击事件，复制 URL 到剪贴板
                copyButton.addEventListener('click', () => {
                    GM_setClipboard(rawUrl);
                    alert('URL 已复制到剪贴板');
                });
            }
        });
    } else {
        console.warn('未能从 URL 中提取仓库信息');
    }
})();
```



最后的最后~
![ByeBye](/img/thank-you.jpg "Thank you!")

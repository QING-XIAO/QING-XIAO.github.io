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

客是基于GitHub Pages搭建的, 没有搞图床所以文章的背景图以及内部引用的图片都存储在GitHub仓库, 但Github仓库貌似有限制空间不能>1GB, 那就多建立几个仓库用来存放img就是了, 开搞!

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



最后的最后~
![ByeBye](/img/thank-you.jpg "Thank you!")

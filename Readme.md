### 介绍
> Github Page 规定一个账户只能创建一个 个人或组织站点，项目站点则没有限制。简单来说，我们可以把 Github Page 当成一个服务器来搭建博客。
>
> 如果你也想通过 Github Page 搭建个人博客，可以参考[qiubaiying](https://github.com/qiubaiying/qiubaiying.github.io/blob/master/README.md)的这篇文章, 此博客通过这篇文章教程搭建的，
>
> 在此感谢 BY 大佬, 仓库Fork with [BlackDn](https://github.com/BlackDn).
>
> **PS:** 封面先借用下, 之后再慢慢搞, 侵删~

### 撰写博文
> 要发表的文章一般以 Markdown 的格式放在这里 ```_posts/```, 文件命名采用的是 ```2017-02-04-Hello-2017.md``` 时间+标题的形式，空格用 ```-``` 替换连接.
>
> [MarkDown](https://markdown.com.cn/) 是一种轻量级的「标记语言」, 花半个小时看看很容易就上手了.
```
---
layout:     post                   # 使用的布局（不需要改）
title:      Myself常用软件汇总      # 标题 
subtitle:   Software.              # 副标题
date:       2025-04-01             # 时间
author:     QING-XIAO              # 作者
header-img: img/18mon2_06.jpg      # 这篇文章标题背景图片
catalog:    true                   # 是否归档
tags:                              # 标签
    - Windows
    - 碎碎念
---

```

### 本地调试
> 将仓库clone到本地后cd到目录输入如下命令构建sever. 
```
jekyll s
```
> 访问如下端口即可进行本地实时预览, 省的一遍一遍提交.
```
http://127.0.0.1:4000/
```
> 输入如下命令停止运行.
```
Ctrl + C
```

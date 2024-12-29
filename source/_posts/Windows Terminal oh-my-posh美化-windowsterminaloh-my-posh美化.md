---
title: Windows Terminal oh-my-posh美化
date: 2022-10-31 22:36:52.8
updated: 2022-10-31 22:42:30.205
url: /archives/windowsterminaloh-my-posh美化
categories: 
- windows
tags: 
---

1. 微软商店搜索安装on my posh
1.  打开Windows Terminal JSON设置
1. 在defaults配置添加以下内容

```
"useAcrylic" : true,
"acrylicOpacity" : 0.4,
"font": 
{
	"face": "MesloLGS Nerd Font Mono",
	"size": 12
},
"backgroundImage": "背景图片路径", 
"backgroundImageOpacity": 0.4
````

4. 在power shell中输入

```
notepad $PROFILE
```
5.  添加以下内容到打开的文件
```
oh-my-posh init pwsh --config $env:POSH_THEMES_PATH\montys.omp.json | Invoke-Expression
```
如果出现乱码安装Nerd字体， 可以从[这里](https://github.com/ryanoasis/nerd-fonts/blob/master/readme.md)挑选一款喜欢的字体
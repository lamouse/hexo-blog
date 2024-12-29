---
title: vscode clangd 提示配置
date: 2023-04-04 20:41:13.694
updated: 2023-04-04 20:42:21.9
url: /archives/vscodeclangd提示配置
categories: 
- 工具
tags: 
---

config.yaml
该配置表示只打开c++自动推导的类型例如auto声明，关闭参数名称
```
InlayHints:
  Enabled: Yes
  ParameterNames: No
  DeducedTypes: Yes
```
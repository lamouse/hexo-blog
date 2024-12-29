---
title: macos intel调试rust的问题
date: 2024-01-20 16:23:25.173
updated: 2024-01-20 16:23:25.173
url: /archives/macosinteldebugrust
categories: 
- 工具
tags: 
---

[地址](https://stackoverflow.com/questions/77218022/why-is-my-debugger-in-vscode-not-working-with-rust-after-mac-update-to-sonoma-14)
方法：删除
```
~/.vscode/extensions/vadimcn.vscode-lldb-1.10.0/lldb/bin/debugserver
```
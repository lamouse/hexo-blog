---
title: macos系统在glfw下使用vkCreateMetalSurfaceEXT创建vksurface
date: 2024-12-29 14:18:51.216
updated: 2024-12-29 14:25:00.647
url: /archives/macos系统下glfw使用vkcreatemetalsurfaceext创建vksurface
categories: 
- mac
tags: 
---

 ### 踩了一天的坑，记录下，网上相关资料也很少，主要问题在macos上windows的资料网上全
 #### 首先包含必要的头文件
 ```cpp
#if defined(__APPLE__)
#define GLFW_EXPOSE_NATIVE_COCOA
#include <QuartzCore/CAMetalLayer.h>
#include <objc/message.h>
#include <objc/objc.h>
#include <objc/runtime.h>  
#endif
```
 #### 接着需要获取CAMetalLayer，这里就很关键了
  ```cpp
// 获取 NSWindow 对象
id cocoaWindow = glfwGetCocoaWindow(window);
if (!cocoaWindow) {
    return nullptr;
}

// 获取 contentView
id contentView = reinterpret_cast<id (*)(id, SEL)>(objc_msgSend)(cocoaWindow, sel_getUid("contentView"));
if (!contentView) {
    return nullptr;
}

// 获取 layer
id layer = reinterpret_cast<id (*)(id, SEL)>(objc_msgSend)(contentView, sel_registerName("layer"));
using ObjcMsgSendFunc = BOOL (*)(id, SEL, Class);
auto objcMsgSendFunc = reinterpret_cast<ObjcMsgSendFunc>(objc_msgSend);
bool isCAMetalLayer = objcMsgSendFunc(layer, sel_registerName("isKindOfClass:"),
                                    static_cast<Class>(objc_getClass("CAMetalLayer")));
if (!isCAMetalLayer) {
    // 创建 CAMetalLayer 这里创建CAMetalLayer是必须的，
    //因为glfw并没有默认创建CAMetalLayer
    //相关代码可以在glfw的代码中找到代码位置在_glfwCreateWindowSurfaceCocoa
    //https://github.com/glfw/glfw/blob/master/src/cocoa_window.m
    //按照glfw的流程完成的CAMetalLayer的获取
    //幸好现在又ai辅助，将代码转为为c++版本，要不然还得学习苹果系统的开发
    id metalLayer = reinterpret_cast<id (*)(Class, SEL)>(objc_msgSend)(objc_getClass("CAMetalLayer"),
                                                                    sel_getUid("alloc"));
    metalLayer = reinterpret_cast<id (*)(id, SEL)>(objc_msgSend)(metalLayer, sel_getUid("init"));

    // 设置 contentView 的 layer
    reinterpret_cast<void (*)(id, SEL, id)>(objc_msgSend)(contentView, sel_getUid("setLayer:"), metalLayer);
    reinterpret_cast<void (*)(id, SEL, BOOL)>(objc_msgSend)(contentView, sel_getUid("setWantsLayer:"), YES);

    layer = metalLayer;
}

// 检测并设置 contentsScale
//这里主要是设Scale，直接默认开启就好
// if (glfwGetWindowAttrib(window, GLFW_SCALE_TO_MONITOR)) {
reinterpret_cast<void (*)(id, SEL, CGFloat)>(objc_msgSend)(
    layer, sel_getUid("setContentsScale:"),
    reinterpret_cast<CGFloat (*)(id, SEL)>(objc_msgSend)(cocoaWindow, sel_getUid("backingScaleFactor")));
//}

return layer;
```

 #### 最后一步，创建vkSurface
 ```cpp
 //wsi.get_surfac就是刚才返回的layer，只不过被转换成了void*
const VkMetalSurfaceCreateInfoEXT macos_ci = {
    .sType = VK_STRUCTURE_TYPE_METAL_SURFACE_CREATE_INFO_EXT,
    .pNext = nullptr,
    .pLayer = static_cast<const CAMetalLayer*>(wsi.get_surface),
};
auto result = vkCreateMetalSurfaceEXT(instance, &macos_ci, nullptr, &unsafe_surface);
if (result != VK_SUCCESS) {
    throw std::runtime_error("Failed to create Metal surface");
}
 ```

 #### 相关代码
 https://github.com/lamouse/graphics

 #### 想法来源
[suzu](https://git.suyu.dev/suyu/suyu)
[glfw](https://github.com/glfw/glfw)

    
---
title: vulkan在mac上的ErrorIncompatibleDriver问题解决方法
date: 2023-03-04 16:21:37.052
updated: 2023-06-11 22:47:05.335
categories: 
  - macOS
tags: 
 - Vulkan
 - macOS
---

启用VK_KHR_portability_enumeration 实例扩展
为您的实例创建信息添加（或设置）VK_INSTANCE_CREATE_ENUMERATE_PORTABILITY_BIT_KHR 标志
启用VK_KHR_portability_subset 设备扩展

```cpp
vk::Instance Context::createInstance(const std::vector<const char*>& instanceExtends)
{
    ::std::vector<const char*> layers{"VK_LAYER_KHRONOS_validation"};
    ::std::vector<const char*> externs = {instanceExtends.begin(), instanceExtends.end()};
#if defined(VK_USE_PLATFORM_MACOS_MVK)
    externs.push_back("VK_KHR_portability_enumeration");
    ::vk::InstanceCreateFlags flags{VK_INSTANCE_CREATE_ENUMERATE_PORTABILITY_BIT_KHR};
#endif
 
    ::vk::InstanceCreateInfo createInfo;
    ::vk::ApplicationInfo appInfo;
     appInfo.setApiVersion(VK_API_VERSION_1_3);
     createInfo.setPEnabledLayerNames(layers)
                .setPApplicationInfo(&appInfo)
#if defined(VK_USE_PLATFORM_MACOS_MVK)
                .setFlags(flags)
#endif
                .setPEnabledExtensionNames(externs);
    return ::vk::createInstance(createInfo);
}

void Device::createDevice()
{
    queryQueueFamilyIndices();
    ::vk::DeviceCreateInfo createInfo;
    ::std::vector<::vk::DeviceQueueCreateInfo> queueInfos;
    // "VK_KHR_portability_subset" macos
    
#if defined(VK_USE_PLATFORM_MACOS_MVK)
   ::std::vector<const char*> extends{VK_KHR_SWAPCHAIN_EXTENSION_NAME, "VK_KHR_portability_subset"};
#else
    ::std::vector<const char*> extends{VK_KHR_SWAPCHAIN_EXTENSION_NAME};
#endif

    float priorities = 0.5;
    uint32_t queueCount = 1;
    ::vk::DeviceQueueCreateInfo queueInfo;
    queueInfo.setPQueuePriorities(&priorities)
            .setQueueCount(1)
            .setQueueFamilyIndex(queueFamilyIndices.graphicsQueue.value());
    queueInfos.push_back(::std::move(queueInfo));

    if(queueFamilyIndices.graphicsQueue.value() != queueFamilyIndices.presentQueue.value()){
        ::vk::DeviceQueueCreateInfo queueInfo;
        queueInfo.setPQueuePriorities(&priorities)
                .setQueueCount(queueCount)
                .setQueueFamilyIndex(queueFamilyIndices.presentQueue.value());
        queueInfos.push_back(::std::move(queueInfo));
    }


    createInfo.setQueueCreateInfos(queueInfos)
                .setPEnabledExtensionNames(extends);

    device = phyDevice.createDevice(createInfo);
}

```
编译的时候加上宏定义VK_USE_PLATFORM_MACOS_MVK即可
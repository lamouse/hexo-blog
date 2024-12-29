---
title: c++ shader_ptr的一个内存泄漏问题
date: 2023-04-14 19:31:32.083
updated: 2023-04-14 19:45:35.84
url: /archives/shaderptrmemoryleak
categories: 
- c/c++
tags: 
---

不要以为使用 shader_ptr可以避免内存泄漏。下面是一个泄漏的例子

```
#include <memory>
#include <iostream>

class Swapchain
{
public:
    ~Swapchain(){::std::cout << "destroy" << ::std::endl;};
    Swapchain(sampleCount, ::std::shared_ptr<Swapchain> oldSwapchain = nullptr)
    {
    	this->oldSwapchain = oldSwapchain;
        oldSwapchain = nullptr;
    };
    

private:
    ::std::shared_ptr<Swapchain> oldSwapchain;
    int menory[100];
};

int main()
{
   ::std::unique_prt ptr = ::std::make_unique<Swapchain>();
    
    for(int i = 0; i < 1000; i++}
    {
    	ptr = ::std::make_unique<Swapchain>(ptr);
    }
}

```
由于参数名和成员名一样， 构造函数只是将参数oldSwapchain设置为null，但是成员oldSwapchain依旧保留shared_ptr的引用，参数传入进来的Swapchain会像列表一样存在，他们将会保存到成员的oldSwapchain中，这样就完成了一个隐式内存泄漏，valgrind根本没办法检测出这种内存泄漏，使用shared_ptr切记要注意这些问题，Java也有可能遇到这种问题
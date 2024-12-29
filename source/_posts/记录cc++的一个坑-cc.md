---
title: 记录c/c++的一个坑
date: 2023-03-11 22:40:30.122
updated: 2023-03-11 22:40:30.122
url: /archives/cc
categories: 
- c/c++
tags: 
---

先上代码
```
#include <iostream>
#include <memory>
class t{

    private:
        static std::unique_ptr<t> instance;
        t() = default;
    public:
        static void init(){instance.reset(new t());}
        static void quit(){instance.reset();}
        static t& getInstance(){return *instance;}
        ~t(){std::cout << "~t()" << std::endl;}
};

std::unique_ptr<t> t::instance = nullptr;

int main(){
    t::init();
    if(true){
        auto a = t::getInstance();
    }
    t::quit();
}
// output 
// ~t()
// ~t()
```

这里有一个严重的bug那就是会析构函数会调用两次，解决方法就是将auto a修改为auto &a，写auto进行类型推导的时候一定要注意这些
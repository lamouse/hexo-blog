---
title: c和cpp的一个问题
date: 2020-12-25 16:35:02
tags:
---

#### 先上代码

```c
#include <iostream>
int a(){} //none return 
int main()
{
    auto r = a();
    std::cout << r << std::endl;
}
```

1. 这个代码在(Homebrew gcc 10.2)不开启-Wall -Werror是可以编译的
1. r的值每次执行都不一样
1. [一些解释](https://stackoverflow.com/questions/32513793/c-and-c-functions-without-a-return-statement)

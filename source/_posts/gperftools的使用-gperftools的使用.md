---
title: gperftools的使用
date: 2020-09-15 17:27:43.0
updated: 2022-09-05 23:50:52.602
url: /archives/gperftools的使用
categories: 
- 笔记
tags: 
---



#### github地址
```
https://github.com/gperftools/gperftools
```

<!-- more -->

```
git clone https://github.com/gperftools/gperftools.git
cd gperftools
./autogen.sh
make
```

#### HEAP PROFILER
```
1) Link your executable with -ltcmalloc
2) Run your executable with the HEAPPROFILE environment var set:
     $ export HEAPPROFILE=/tmp/heapprof <path/to/binary> [binary args]
3) Run pprof to analyze the heap usage
     $ pprof <path/to/binary> /tmp/heapprof.0045.heap  # run 'ls' to see options
     $ pprof --gv <path/to/binary> /tmp/heapprof.0045.heap
```

#### CPU PROFILER
```
1) Link your executable with -lprofiler
2) Run your executable with the CPUPROFILE environment var set:
     $ export CPUPROFILE=/tmp/prof.out <path/to/binary> [binary args]
3) Run pprof to analyze the CPU usage
     $ pprof <path/to/binary> /tmp/prof.out      # -pg-like text output
     $ pprof --gv <path/to/binary> /tmp/prof.out # really cool graphical output
```

#### 生成PDF文件
```
pprof --pdf ./executable pprof.out > pprof.pdf
```
---
title: 跟着游戏学中文，学编程
date: 2022-12-30 17:48:24.033
updated: 2022-12-30 17:48:24.033
url: /archives/gen-zhe-you-xi-xue-zhong-wen--xue-bian-cheng
categories: 
- 笔记
tags: 
---

#### “只”
有些游戏有几种buff，比如在指定概率内只出现指定的材料，装备，但是你的代码太老了牵一发动全身，那么这个“只”就有意思了，比如你这么实现：拦截或者修改装备或材料出现的接口，加入一个判断，是对应buff的就返回，不是就返回没有出现装备或材料，这样达到了低耦合代码，避免修改原始代码。完成了任务，避免修改出bug。不需要的时候可以直接删除不要。是不是很完美。反正没有客服，即使有我们也可以嘴硬。反正玩家好欺负。

#### “概率”
很多人对概率有很大的误解，以为40%的概率就是10次成4次，100次成40次，成本应该比较固定的，那你的想法就错了，因为可以操作总数，比如你只强化一次装备概率是40，但是是100万的40，1000万的40，想要达成这个40的成本就不一样了，自己可已想象以下，失败的范围变大了，更容易出现，而且一旦涉及的单独概率更容易出现。这也是某些游戏看着概率提升，但是成功成本也提升的原因。只要样本数量足够多，能保证概率就是40，你又如何说概率不是40呢。

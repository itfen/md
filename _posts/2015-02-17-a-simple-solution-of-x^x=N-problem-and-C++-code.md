---
layout: post
title:  "关于x^x=N（x的x次方等于N）已知N求x的方法及C++语言实现"
categories:
comments: true
share: true
---

对于方程 x^x-N=0 ，没有求根公式，所以考虑使用牛顿法迭代求解。牛顿法（Newton’s method）又称为牛顿-拉弗森方法（Newton-Raphson method），它是一种在实数域和复数域上近似求解方程的方法。方法使用函数 f(x) 的泰勒级数的前面几项来寻找方程 f(x)=0 的根。

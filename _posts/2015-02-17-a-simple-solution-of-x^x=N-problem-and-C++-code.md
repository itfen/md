---
layout: post
title:  "关于x^x=N（x的x次方等于N）已知N求x的方法及C++语言实现"
categories:
comments: true
share: true
---

对于方程 x^x-N=0 ，没有求根公式，所以考虑使用牛顿法迭代求解。[牛顿法](http://zh.wikipedia.org/wiki/%E7%89%9B%E9%A1%BF%E6%B3%95)（Newton’s method）又称为牛顿-拉弗森方法（Newton-Raphson method），它是一种在实数域和复数域上近似求解方程的方法。方法使用函数 f(x) 的泰勒级数的前面几项来寻找方程 f(x)=0 的根。

首先，选择一个接近函数f(x)零点的x_0，计算相应的f(x_0)和切线斜率f'(x_0)（这里f'表示函数f的导数）。然后我们计算穿过点(x_0, f(x_0))并且斜率为f'(x_0)的直线和x轴的交点的x坐标，也就是求如下方程的解：

f(x_0)= (x_0-x)cdot f'(x_0)
我们将新求得的点的x坐标命名为x_1，通常x_1会比x_0更接近方程f(x)=0的解。因此我们现在可以利用x_1开始下一轮迭代。迭代公式可化简为如下所示：

x_{n+1} = x_n - frac{f(x_n)}{f'(x_n)}
已经证明，如果f'是连续的，并且待求的零点x是孤立的，那么在零点x周围存在一个区域，只要初始值x_0位于这个邻近区域内，那么牛顿法必定收敛。 并且，如果f'(x)不为0, 那么牛顿法将具有平方收敛的性能. 粗略的说，这意味着每迭代一次，牛顿法结果的有效数字将增加一倍。

图示

![Image](http://zh.wikipedia.org/wiki/File:NewtonIteration_Ani.gif)

蓝线表示方程f而红线表示切线. 可以看出xn+1比xn更靠近f所要求的根x.
由此可见，对于f(x)=x^x-N，要求其图像与x轴的交点，可以多次迭代

f(x)的导函数为f'(x) = x^x*(lnx+1)，迭代的通项公式为

Xn+1 = Xn – f(Xn)/f'(Xn)

= Xn – ( Xn^Xn – N) / ( Xn^Xn * ( lnXn + 1 ) )

= Xn – ( 1 – N/(Xn^Xn) ) /  ( lnXn + 1 )

使用这个公式实际程序测试时发现要循环很多次（如100次）的结果才能比较精确，所以考虑对原函数做一些处理。

在 x^x = N 的两边同时取对数得 xlnx = lnN，这时f(x) = xlnx – lnN，f'(x) = (lnx – 1)，迭代的通项公式为

Xn+1 = Xn – ( Xn*lnXn – lnN ) / ( lnXn – 1 )

=  ( Xn + lnN ) / ( lnXn + 1)

使用此公式效率比之前高多了，只需要5次左右的循环就能得到比较精确的结果。 下面贴出C++语言的实现：

{% highlight c++%}
#include <stdio.h>
#include <math.h>
#include <iostream>

using namespace std;

int main(int argc, char* argv[])
{
	double Xn = 1.0;
	double N = 0.0;

	cin >> N;
	for (int i = 0; i < 5; i++)
	{
		//Xn = Xn - ((1 - N / (pow(Xn, Xn))) / (log(Xn) + 1));
		Xn = (Xn + log(N)) / (log(Xn) + 1);
	}
	cout << Xn << "n";

	system("pause");
	return 0;
}
{% endhighlight %}

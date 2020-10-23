---
title: Romberg
date: 2016-04-22 14:39:47 
tags:
cover: https://cdn-images-1.medium.com/max/904/1*UfN9jeY-NN6niP2Rl7rDWw.png
---



![Image result for Romberginterg](https://cdn-images-1.medium.com/max/904/1*UfN9jeY-NN6niP2Rl7rDWw.png)

龙贝格数值积分算法，以复化梯形公式为基础，用查理森加速外推方法把低精度的积分线性组合成高精度的积分，减少了运算量。

下面是matlab代码

```matlab
function I=Romberginterg(fun,a,b,npanel,tol,flag)
%fun函数的表达式
%a,b下界，上界
%npanel分段数 默认25
%tol 误差上限，默认5e-9
%flag 默认为0 为1的时候打印出递推数表
if nargin<4
 npanel=25;
end
if nargin<5
 tol=5e-9;
end
if nargin<6
 flag=0;
T(1,1)=Trapezoidinteg(fun,a,b,npanel);
err=1; %初始化误差
m=2; %计算行号 开始第一行T(1,1)就是普通的复化梯形积分，从第二行开始
while err>=tol
 T(m,1)=Trapezoidinteg(fun,a,b,2^m*npanel); %第一列仍然是复化梯形公式，每段再分成两段，分成2^m段
 T(m,m)=0;
 for n=2:m %这一行从左向右递推，使用龙贝格积分递推式
 T(m,n)=(4^(n-1)*T(m,n-1))/(4^(n-1)-1);
 end
 err=abs(T(m,m)-T(m-1,m-1)); %计算误差
 m=m+1; %下一行
end
I=T(m-1,m-1); %最后输出
if flag~=0 %打印数表T
 disp(T);
end
end

```

```matlab
function I=Trapezoidinteg(fun,a,b,npanel)
% 复化梯形公式求积分
% fun 函数表达式
% a,b 下界上界
% npanel 分段数
if nargin<4
 npanel=25
end
nnode=npanel+1; %节点数=段数+1
h=(b-a)/(nnode-1); %每段的步长
x=a:h:b; %生成所有x
f=feval(fun,x); %求出对应的y
I=h*(0.5*f(1)+sum(f(2:nnode-1))+0.5*f(nnode)); %两端点各0.5权重，中间节点全部求和，权重为1 最后乘步长
end
```


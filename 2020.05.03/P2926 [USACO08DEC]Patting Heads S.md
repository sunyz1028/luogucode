# [P2926 [USACO08DEC]Patting Heads S](https://www.luogu.com.cn/problem/P2926)

## 题目描述

It's Bessie's birthday and time for party games! Bessie has instructed the N (1 <= N <= 100,000) cows conveniently numbered 1..N to sit in a circle (so that cow i [except at the ends] sits next to cows i-1 and i+1; cow N sits next to cow 1). Meanwhile, Farmer John fills a barrel with one billion slips of paper, each containing some integer in the range 1..1,000,000.

Each cow i then draws a number A_i (1 <= A_i <= 1,000,000) (which is not necessarily unique, of course) from the giant barrel. Taking turns, each cow i then takes a walk around the circle and pats the heads of all other cows j such that her number A_i is exactly

divisible by cow j's number A_j; she then sits again back in her original position.

The cows would like you to help them determine, for each cow, the number of other cows she should pat.

## 输入格式

\* Line 1: A single integer: N

\* Lines 2..N+1: Line i+1 contains a single integer: A_i

## 输出格式

\* Lines 1..N: On line i, print a single integer that is the number of other cows patted by cow i.

## 题意翻译

今天是贝茜的生日，为了庆祝自己的生日，贝茜邀你来玩一个游戏。

贝茜让 N*N* (1\leq N\leq 10^51≤*N*≤105) 头奶牛坐成一个圈。除了 11 号与 N*N* 号奶牛外，i*i* 号奶牛与 i-1*i*−1 号和 i+1*i*+1 号奶牛相邻。N*N* 号奶牛与 11 号奶牛相邻。农夫约翰用很多纸条装满了一个桶，每一张包含了一个不一定是独一无二的 11 到 10^6106 的数字。

接着每一头奶牛 i*i* 从柄中取出一张纸条 A_i*A**i*。每头奶牛轮流走上一圈，同时拍打所有手上数字能整除在自己纸条上的数字的牛的头，然后做回到原来的位置。牛们希望你帮助他们确定，每一头奶牛需要拍打的牛。

## 输入输出样例

**输入 #1**复制

```
5 
2 
1 
2 
3 
4 
```

**输出 #1**复制

```
2 
0 
2 
1 
3 
```

## 说明/提示

The 5 cows are given the numbers 2, 1, 2, 3, and 4, respectively.

The first cow pats the second and third cows; the second cows pats no cows; etc.



***

题目翻译有个错误，输出的是拍的次数

10^6直接暴力会超时，所以记录出现的次数，然后预处理打表。

最后直接输出。

***



```c++
#include<bits/stdc++.h>
using namespace std;
int n,a[10000010],b[10000010],cnt[10000010];
void fun(){
    for (int i=1;i<=10000000;i++){
    	if(b[i]==0) continue;
    	for (int j=1;i*j<=10000000;j++){
    		 if(b[i*j]) cnt[i*j]+=b[i];
        }   	
    } 
}
int main(){
    scanf("%d",&n);
    for(int i=1;i<=n;i++){
        scanf("%d",&a[i]);
        b[a[i]]++;
    }
    fun();
    for(int i=1;i<=n;i++)
    	printf("%d\n",cnt[a[i]]-1);
}
```


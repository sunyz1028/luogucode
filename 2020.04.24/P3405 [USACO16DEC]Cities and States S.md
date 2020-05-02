# [P3405 [USACO16DEC]Cities and States S](https://www.luogu.com.cn/problem/P3405)

## 题目描述

To keep his cows intellectually stimulated, Farmer John has placed a large map of the USA on the wall of his barn. Since the cows spend many hours in the barn staring at this map, they start to notice several curious patterns. For example, the cities of Flint, MI and Miami, FL share a very special relationship: the first two letters of "Flint" give the state code ("FL") for Miami, and the first two letters of "Miami" give the state code ("MI") for Flint.

Let us say that two cities are a "special pair" if they satisfy this property and come from different states. The cows are wondering how many special pairs of cities exist. Please help them solve this amusing geographical puzzle!

为了让奶牛在智力上受到刺激，农夫约翰在谷仓的墙上放了一张美国地图。由于奶牛在谷仓里花了很多时间盯着这张地图，他们开始注意到一些奇怪的关系。例如，城市Flint，在MI省，或者Miami在FL省，他们有一种特殊的关系：“Flint”市前两个字母就是“FL”省，迈阿密前两个字母是“MI”省。

让我们说，两个城市是一个“特殊的一对”，如果他们满足这个属性，来自不同的省。奶牛想知道有多少特殊的城市存在。请帮助他们解决这个有趣的地理难题！

## 输入格式

The first line of input contains N*N* (1 \leq N \leq 200,0001≤*N*≤200,000), the number ofcities on the map.

The next N*N* lines each contain two strings: the name of a city (a string of at least 2 and at most 10 uppercase letters), and its two-letter state code (a string of 2 uppercase letters). Note that the state code may be something like ZQ, which is not an actual USA state. Multiple cities with the same name can exist, but they will be in different states.

输入的第一行包含（），地图上的城市数量。

下一行包含两个字符串：一个城市的名称（字符串至少2个最多10个大写字母），和它的两个字母的州代码（一串2个大写字母）。注意状态代码可能像ZQ，这并不是一个真正的美国。同一名称的多个城市可以存在，但它们将处于不同的州。

## 输出格式

Please output the number of special pairs of cities.

请输出特殊城市对数。

## 输入输出样例

**输入 #1**复制

```
6
MIAMI FL
DALLAS TX
FLINT MI
CLEMSON SC
BOSTON MA
ORLANDO FL
```

**输出 #1**复制

```
1
```

## 说明/提示

感谢@何炜华8864 的翻译，并经过kkksc03的修改



***

把前两个字符串前两个字符反过来相加，比较是否有符合条件的，再把记录正序。

**注意如果两字符串前两个字符相等则不符合条件**

***



```c++
#include<bits/stdc++.h>
using namespace std;

int main(){
    int n,ans=0;
    string a,b;
    map<string,int>m;
    scanf("%d",&n);
    while(n--){
    	cin>>a>>b;
    	a=a.substr(0,2);
    	b=b.substr(0,2);
		string ta,tb;
		ta=a+b;
		tb=b+a;
    	if(a!=b){
    		ans+=m[tb];
    		m[ta]++;
		}
	}
	printf("%d",ans);
    return 0;
}
```


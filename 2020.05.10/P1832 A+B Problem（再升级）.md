# [P1832 A+B Problem（再升级）](https://www.luogu.com.cn/problem/P1832)

## 题目背景

·题目名称是吸引你点进来的

·实际上该题还是很水的

## 题目描述

·1+1=? 显然是2

·a+b=? 1001回看不谢

·哥德巴赫猜想 似乎已呈泛滥趋势

·以上纯属个人吐槽

·给定一个正整数n，求将其分解成若干个素数之和的方案总数。

## 输入格式

一行：一个正整数n

## 输出格式

一行：一个整数表示方案总数

## 输入输出样例

**输入 #1**复制

```
7
```

**输出 #1**复制

```
3
```

## 说明/提示

【样例解释】

7=7 7=2+5

7=2+2+3

【福利数据】

【输入】 20

【输出】 26

【数据范围及约定】

对于30%的数据 1<=n<=10

对于100%的数据，1<=n<=10^3



***

先筛选出小于n的质数。

然后根据` rst[j]+=rst[j-prime[i]]` 递推关系计算，注意`rst[0]=1！！！初始化。

***



```c++
#include <bits/stdc++.h>
using namespace std;
int nums[1010],prime[1010],n;
long long rst[1010];
void isprime(int n){
	for(int i=2;i<=n;i++){
		if(nums[i]==0)	prime[++prime[0]]=i;
		for(int j=1;j<=prime[0]&&i*prime[j]<=n;j++){
			nums[i*prime[j]]=1;
			if(i%prime[j]==0)	break;
		}
	}
}
int main(){
	scanf("%d",&n);
	isprime(n);
	rst[0]=1;
	for(int i=1;i<=prime[0];i++){
		for(int j=prime[i];j<=n;j++)
			rst[j]+=rst[j-prime[i]];
	}
	printf("%lld",rst[n]);
	return 0;
}
```


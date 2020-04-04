## [P1182 数列分段 Section II](https://www.luogu.com.cn/problem/P1182)

## 题目描述

对于给定的一个长度为N的正整数数列 A1-AN，现要将其分成 M(M≤N）段，并要求每段连续，且每段和的最大值最小。

关于最大值最小：

例如一数列 4 2 4 5 1 要分成 3 段。

将其如下分段：

​			(4 2) (4 5) (1)

第一段和为 6，第 2 段和为 9，第 3 段和为 1，和最大值为 9。

将其如下分段：

​			(4) (2 4) (5 1)

第一段和为 4，第 2 段和为 6，第 3 段和为 6，和最大值为 6。

并且无论如何分段，最大值不会小于 6。

所以可以得到要将数列 4 2 4 5 1 要分成 3 段，每段和的最大值最小为 6。

## 输入格式

第 1 行包含两个正整数 N*,*M。

第 2 行包含 N个空格隔开的非负整数 Ai，含义如题目所述。

## 输出格式

一个正整数，即每段和最大值最小为多少。

## 输入输出样例

**输入 #1**复制

```
5 3
4 2 4 5 1
```

**输出 #1**复制

```
6
```

## 说明/提示

对于 20% 的数据，N ≤10。

对于 40% 的数据，N ≤1000。

对于 100% 的数据，1≤*N*≤10^5，M ≤ N，Ai <108， 答案不超过 10^9。



***

简单二分答案法，但要注意两点。

1. 初始值左端为最长的长度，右端为总长度
2. **分组最后有剩下来的单独为一组！！**

***



```c++
#include<bits/stdc++.h>
#define ll long long
using namespace std;

int main() {
	ll n,m,a[110000]={0},cot=0,maxn=0,ans;
	scanf("%lld %lld",&n,&m);
	for(ll i=0;i<n;i++){
		scanf("%lld",&a[i]);
		cot+=a[i];
		maxn=max(a[i],maxn);
	}
	ll l=maxn,r=cot;
	while(l<=r){
		ll mid=(l+r)/2,t=0,sum=0;
		for(int i=0;i<n;i++){
			if(sum+a[i]>mid){
				sum=a[i];
				t++;
			}else if(sum+a[i]==mid){
				sum=0;
				t++;
			}else if(sum+a[i]<mid){
				sum+=a[i];
			}
		}
		if(sum>0)	t++;
		if(t<=m){
			ans=mid;
			r=mid-1;
		}	
		else if(t>m)	l=mid+1;
	}
	printf("%lld",ans);
	return 0;
}
```


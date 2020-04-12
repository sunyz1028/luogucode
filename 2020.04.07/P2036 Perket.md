# [P2036 Perket](https://www.luogu.com.cn/problem/P2036)

## 题目描述

Perket 是一种流行的美食。为了做好 Perket，厨师们必须小心选择配料，以便达到更好的口感。你有N种可支配的配料。对于每一种配料，我们知道它们各自的酸度 S 和甜度 B。当我们添加配料时，总的酸度为每一种配料的酸度总乘积；总的甜度为每一种配料的甜度的总和。

众所周知，美食应该口感适中；所以我们希望选取配料，以使得酸度和甜度的绝对差最小。

另外，我们必须添加至少一种配料，因为没有美食是以白水为主要配料的。

## 输入格式

第一行包括整数 N，表示可支配的配料数。

接下来 N行，每一行为用空格隔开的两个整数，表示每一种配料的酸度和甜度。

输入数据保证，如果我们添加所有配料，总的酸度和甜度都不会超过 10^9。

## 输出格式

输出酸度和甜度的最小的绝对差。

## 输入输出样例

**输入 #1**复制

```
1
3 10
```

**输出 #1**复制

```
7
```

**输入 #2**复制

```
4
1 7
2 6
3 8
4 9
```

**输出 #2**复制

```
1
```

## 说明/提示

1 ≤ N ≤ 10。



***

简单DFS题。没什么好说的。。。



***



```c++
#include<bits/stdc++.h>
#define ll long long
using namespace std;
ll n,s[11],b[11],ans=0x7fffffff;
void dfs(ll ss,ll bb,ll nn){
	if(nn==n){
		if(ss==1&&bb==0)	return;
		ans=min(ans,abs(ss-bb));
		return;
	}
	dfs(ss*s[nn],bb+b[nn],nn+1);
	dfs(ss,bb,nn+1);
}
int main(){
	scanf("%lld",&n);
	for(int i=0;i<n;i++){
		scanf("%lld %lld",&s[i],&b[i]);
	}
	dfs(1,0,0);
	printf("%lld",ans);
    return 0;
}
```


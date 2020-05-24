# [P2853 [USACO06DEC]Cow Picnic S](https://www.luogu.com.cn/problem/P2853)

## 题目描述

The cows are having a picnic! Each of Farmer John's K (1 ≤ K ≤ 100) cows is grazing in one of N (1 ≤ N ≤ 1,000) pastures, conveniently numbered 1...N. The pastures are connected by M (1 ≤ M ≤ 10,000) one-way paths (no path connects a pasture to itself).

The cows want to gather in the same pasture for their picnic, but (because of the one-way paths) some cows may only be able to get to some pastures. Help the cows out by figuring out how many pastures are reachable by all cows, and hence are possible picnic locations.

K(1≤K≤100)只奶牛分散在N(1≤N≤1000)个牧场．现在她们要集中起来进餐．牧场之间有M(1≤M≤10000)条有向路连接，而且不存在起点和终点相同的有向路．她们进餐的地点必须是所有奶牛都可到达的地方．那么，有多少这样的牧场呢？

## 输入格式

Line 1: Three space-separated integers, respectively: K, N, and M

Lines 2..K+1: Line i+1 contains a single integer (1..N) which is the number of the pasture in which cow i is grazing.

Lines K+2..M+K+1: Each line contains two space-separated integers, respectively A and B (both 1..N and A != B), representing a one-way path from pasture A to pasture B.

## 输出格式

Line 1: The single integer that is the number of pastures that are reachable by all cows via the one-way paths.

## 输入输出样例

**输入 #1**复制

```
2 4 4
2
3
1 2
1 4
2 3
3 4
```

**输出 #1**复制

```
2
```

## 说明/提示

The cows can meet in pastures 3 or 4.



***

简单图的搜索，由于数字不大直接搜索即可，用bfs。



但是要注意有可能会出现环，要判断出现的次数。

***



```c++
#include <bits/stdc++.h>
using namespace std;
int cow[100],k,n,m,flag[1001],muchang[1001],rst=0;
vector<int> f[1001];
int main(){
	scanf("%d %d %d",&k,&n,&m);
	for(int i=0;i<k;i++)	scanf("%d",&cow[i]);
	while(m--){
		int t1,t2;
		scanf("%d %d",&t1,&t2);
		f[t1].push_back(t2);
	}
	for(int i=0;i<k;i++){
		memset(flag,0,sizeof(flag));
		queue<int> q;
		q.push(cow[i]);
		while(!q.empty()){
			int top=q.front();
			q.pop();
			if(flag[top]==0){
				muchang[top]++;
				flag[top]=1;
			}else	continue;
			for(int j=0;j<f[top].size();j++){
				int t=f[top][j];
				if(flag[t]==0)	q.push(t);
			}
		}
	}
	for(int i=1;i<=n;i++){
		if(muchang[i]==k)	rst++;
	}
	printf("%d",rst);
	return 0;
}
```


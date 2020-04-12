

# [P2895 [USACO08FEB]Meteor Shower S](https://www.luogu.com.cn/problem/P2895)

## 题目描述

Bessie hears that an extraordinary meteor shower is coming; reports say that these meteors will crash into earth and destroy anything they hit. Anxious for her safety, she vows to find her way to a safe location (one that is never destroyed by a meteor) . She is currently grazing at the origin in the coordinate plane and wants to move to a new, safer location while avoiding being destroyed by meteors along her way.

The reports say that M meteors (1 ≤ M ≤ 50,000) will strike, with meteor i will striking point (Xi, Yi) (0 ≤ Xi ≤ 300; 0 ≤ Yi ≤ 300) at time Ti (0 ≤ Ti ≤ 1,000). Each meteor destroys the point that it strikes and also the four rectilinearly adjacent lattice points.

Bessie leaves the origin at time 0 and can travel in the first quadrant and parallel to the axes at the rate of one distance unit per second to any of the (often 4) adjacent rectilinear points that are not yet destroyed by a meteor. She cannot be located on a point at any time greater than or equal to the time it is destroyed).

Determine the minimum time it takes Bessie to get to a safe place.

牛去看流星雨，不料流星掉下来会砸毁上下左右中五个点。每个流星掉下的位置和时间都不同，求牛能否活命，如果能活命，最短的逃跑时间是多少？

## 输入格式

\* Line 1: A single integer: M

\* Lines 2..M+1: Line i+1 contains three space-separated integers: Xi, Yi, and Ti

## 输出格式

\* Line 1: The minimum time it takes Bessie to get to a safe place or -1 if it is impossible.

## 题意翻译

贝茜听说了一个骇人听闻的消息：一场流星雨即将袭击整个农场，由于流星体积过大，它们无法在撞击到地面前燃烧殆尽，届时将会对它撞到的一切东西造成毁灭性的打击。很自然地，贝茜开始担心自己的安全问题。以FJ牧场中最聪明的奶牛的名誉起誓，她一定要在被流星砸到前，到达一个安全的地方（也就是说，一块不会被任何流星砸到的土地）。如果将牧场放入一个直角坐标系中，贝茜现在的位置是原点，并且，贝茜不能踏上一块被流星砸过的土地。 根据预报，一共有M颗流星(1 <= M <= 50,000)会坠落在农场上，其中第i颗流星会在时刻Ti (0 <= Ti <= 1,000)砸在坐标为(Xi, Yi) (0 <= Xi <= 300；0 <= Yi <= 300)的格子里。流星的力量会将它所在的格子，以及周围4个相邻的格子都化为焦土，当然贝茜也无法再在这些格子上行走。

贝茜在时刻0开始行动，它只能在第一象限中，平行于坐标轴行动，每1个时刻中，她能移动到相邻的（一般是4个）格子中的任意一个，当然目标格子要没有被烧焦才行。如果一个格子在时刻t被流星撞击或烧焦，那么贝茜只能在t之前的时刻在这个格子里出现。

请你计算一下，贝茜最少需要多少时间才能到达一个安全的格子。

Translated by @跪下叫哥

## 输入输出样例

**输入 #1**复制

```
4
0 0 2
2 1 2
1 1 2
0 3 5
```

**输出 #1**复制

```
5
```



***

简单的BFS题，注意判断条件就行了

***



```c++
#include<bits/stdc++.h>
#define ll long long
using namespace std;
int n,boom[310][310]={0},bb[310][310]={0};
struct Step{
	int x;
	int y;
	int n;
}stp;
void bfs(int x,int y){
	int cot=0,rst;
	queue<Step> q; 
	Step p;
	p.x=x;p.y=y;p.n=cot;
	q.push(p);bb[0][0]=1;
	while(!q.empty()){
		int flag=0;
		x=q.front().x; y=q.front().y;
		if(boom[x][y]==-1){
			printf("%d",q.front().n);
			return;
		}
		if(x-1>=0&&(boom[x-1][y]>q.front().n+1||boom[x-1][y]==-1)&&bb[x-1][y]==0){
			p.x=x-1;p.y=y;p.n=q.front().n+1;
			q.push(p);flag=1;bb[x-1][y]=1;
		}
		if((boom[x][y+1]>q.front().n+1||boom[x][y+1]==-1)&&bb[x][y+1]==0){
			p.x=x; p.y=y+1; p.n=q.front().n+1;
			q.push(p);flag=1;bb[x][y+1]=1;
		}
		if(y-1>=0&&(boom[x][y-1]>q.front().n+1||boom[x][y-1]==-1)&&bb[x][y-1]==0){
			p.x=x; p.y=y-1; p.n=q.front().n+1;
			q.push(p);flag=1;bb[x][y-1]=1;
		}
		if((boom[x+1][y]>q.front().n+1||boom[x+1][y]==-1)&&bb[x+1][y]==0){
			p.x=x+1; p.y=y; p.n=q.front().n+1;
			q.push(p);flag=1;bb[x+1][y]=1;
		}
		q.pop();
	}
	printf("-1");
	return;
}
int main(){
	scanf("%d",&n); 
	memset(boom,-1,sizeof(boom));
	for(int i=0;i<n;i++){
		int x,y,t;
		scanf("%d %d %d",&x,&y,&t);
		if(boom[x][y]==-1) boom[x][y]=t; else boom[x][y]=min(boom[x][y],t);
		if(x-1>=0&&boom[x-1][y]==-1) boom[x-1][y]=t; else if(x-1>=0)boom[x-1][y]=min(boom[x-1][y],t);
		if(boom[x+1][y]==-1) boom[x+1][y]=t; else boom[x+1][y]=min(boom[x+1][y],t);
		if(y-1>=0&&boom[x][y-1]==-1) boom[x][y-1]=t; else if(y-1>=0)boom[x][y-1]=min(boom[x][y-1],t);
		if(boom[x][y+1]==-1) boom[x][y+1]=t; else boom[x][y+1]=min(boom[x][y+1],t);
	}
	bfs(0,0);
    return 0;
}
```


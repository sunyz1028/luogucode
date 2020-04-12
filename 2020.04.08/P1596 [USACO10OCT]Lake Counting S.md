# [P1596 [USACO10OCT]Lake Counting S](https://www.luogu.com.cn/problem/P1596)

## 题目描述

Due to recent rains, water has pooled in various places in Farmer John's field, which is represented by a rectangle of N x M (1 <= N <= 100; 1 <= M <= 100) squares. Each square contains either water ('W') or dry land ('.'). Farmer John would like to figure out how many ponds have formed in his field. A pond is a connected set of squares with water in them, where a square is considered adjacent to all eight of its neighbors. Given a diagram of Farmer John's field, determine how many ponds he has.

由于近期的降雨，雨水汇集在农民约翰的田地不同的地方。我们用一个NxM(1<=N<=100;1<=M<=100)网格图表示。每个网格中有水('W') 或是旱地('.')。一个网格与其周围的八个网格相连，而一组相连的网格视为一个水坑。约翰想弄清楚他的田地已经形成了多少水坑。给出约翰田地的示意图，确定当中有多少水坑。

## 输入格式

Line 1: Two space-separated integers: N and M * Lines 2..N+1: M characters per line representing one row of Farmer John's field. Each character is either 'W' or '.'. The characters do not have spaces between them.

第1行：两个空格隔开的整数：N 和 M 第2行到第N+1行：每行M个字符，每个字符是'W'或'.'，它们表示网格图中的一排。字符之间没有空格。

## 输出格式

Line 1: The number of ponds in Farmer John's field.

一行：水坑的数量

## 输入输出样例

**输入 #1**复制

```
10 12
W........WW.
.WWW.....WWW
....WW...WW.
.........WW.
.........W..
..W......W..
.W.W.....WW.
W.W.W.....W.
.W.W......W.
..W.......W.
```

**输出 #1**复制

```
3
```

## 说明/提示

OUTPUT DETAILS: There are three ponds: one in the upper left, one in the lower left, and one along the right side.



***

DFS判断题

***



```c++
#include<iostream>
#include<cstdio>
using namespace std;
int fxx[9]={0,-1,-1,-1,0,0,1,1,1};//x方向
int fxy[9]={0,-1,0,1,-1,1,-1,0,1};//y方向
int n,m,ans;
char a[105][105];
void dfs(int x,int y)
{
    int r,c;
    a[x][y]='.';
    for (int i=1;i<=8;i++)
    {
        r=x+fxx[i];
        c=y+fxy[i];
        if (r<1||r>n||c<1||c>m||a[r][c]=='.')//判断是否出界
            continue;
        a[r][c]='.';
        dfs(r,c);
    }
}
int main()
{
    scanf("%d %d\n",&n,&m);
    for (int i=1;i<=n;i++)
    {
        for (int j=1;j<=m;j++)
            cin>>a[i][j];
    }
    ans=0;
    for (int i=1;i<=n;i++)
    {
        for (int j=1;j<=m;j++)
        {
            if (a[i][j]=='W')
            {
                ans++;
                dfs(i,j);
            }
        }
    }
    printf("%d\n",ans);
    return 0;
}
```

未AC

```c++
#include <bits/stdc++.h>
using namespace std;
char farm[110][110];
int x,y,cot=0,dir[4][2]={0,1,1,-1,1,0,1,1};
void dfs(int tx,int ty){
	if(farm[tx][ty]=='W'){
		farm[tx][ty]='.';
		for(int i=0;i<4;i++){
			if(tx+dir[i][0]>=0&&tx+dir[i][0]<x&&ty+dir[i][1]>=0&&ty+dir[i][1]<y)
				dfs(tx+dir[i][0],ty+dir[i][1]);
		}
	}
	return;
}
int main(){
	scanf("%d %d",&x,&y);
	getchar();
	for(int i=0;i<x;i++){
		scanf("%s",farm[i]);
	}
	for(int i=0;i<x;i++)
		for(int j=0;j<y;j++)
			if(farm[i][j]=='W'){
				cot++;
				dfs(i,j);
			}
	printf("%d",cot);
	return 0;
}

```


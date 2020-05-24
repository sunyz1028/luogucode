# [P1203 [USACO1.1]坏掉的项链Broken Necklace](https://www.luogu.com.cn/problem/P1203)

## 题目描述

你有一条由 n*n* 个红色的，白色的，或蓝色的珠子组成的项链，珠子是随意安排的。 这里是 n=29*n*=29 的两个例子:

![img](https://cdn.luogu.com.cn/upload/pic/56.png)

第一和第二个珠子在图片中已经被作记号。

图片 A 中的项链可以用下面的字符串表示：

```
brbrrrbbbrrrrrbrrbbrbbbbrrrrb
```

假如你要在一些点打破项链，展开成一条直线，然后从一端开始收集同颜色的珠子直到你遇到一个不同的颜色珠子，在另一端做同样的事(颜色可能与在这之前收集的不同)。 确定应该在哪里打破项链来收集到最大数目的珠子。

例如，在图片 A 中的项链中，在珠子 99 和珠子 1010 或珠子 2424 和珠子 2525 之间打断项链可以收集到 88 个珠子。

白色珠子什么意思?

在一些项链中还包括白色的珠子(如图片B) 所示。

当收集珠子的时候，一个被遇到的白色珠子可以被当做红色也可以被当做蓝色。

表现含有白珠项链的字符串将会包括三个符号 `r`，`b`，`w` 。

写一个程序来确定从一条被给出的项链可以收集到的珠子最大数目。

## 输入格式

第一行一个正整数 n*n* ，表示珠子数目。 第二行一串长度为 n*n* 的字符串, 每个字符是 `r` ， `b` 或 `w`。

## 输出格式

输出一行一个整数，表示从给出的项链中可以收集到的珠子的最大数量。

## 输入输出样例

**输入 #1**复制

```
29 
wwwbbrwrbrbrrbrbrwrwwrbwrwrrb
```

**输出 #1**复制

```
11
```

## 说明/提示

【数据范围】
对于 100\%100% 的数据，3\le n \le 3503≤*n*≤350

题目翻译来自NOCOW。

USACO Training Section 1.1



***

先处理出每一段的数论，再根据规律找出最长的那一段。

***



```c++
#include <bits/stdc++.h>
using namespace std;
int main(){
	string s;
	int n,r[400]={0},flag[400]={0},start=0,maxlen=0;
	fill(r,r+400,1);
	scanf("%d",&n);
	cin >> s;
	for(int i=0;i<s.length();i++){
		if(s[i]=='w'){
			int t1=i,cot=0;
			while(s[t1]=='w'){
				t1--,cot++;
				if(t1<0)	t1+=n;
				if(cot==n)	break;
			}
			cot=0;
			while(s[i%n]=='w'){
				i++,cot++;
				if(cot==n)	break;
			}
			if(s[t1]==s[i%n]){
				for(int j=t1;;){
					j++;
					if(j>n)	j=0;
					s[j]=s[t1];
					if(j==i) break;
				}
			}
		}
	}
	char t1=s[0];
	for(int i=0;i<s.length();i++){
		if(s[i]!=t1){
			start=i;
			break;
		}
	}
	t1=s[start];
	int cot=0,zz=0;
	for(int i=start;;){
		if(t1=='w')	flag[r[0]]=1;
		i++;
		if(i==s.length())	i-=s.length();
		if(cot==s.length())	break;
		if(s[i]==t1){
			r[r[0]]++;
		}else{
			r[0]++;
			t1=s[i];
		}
		cot++;
	}
	if(r[0]==1){
		printf("%d",s.length());
		return 0;
	}else if(r[0]==2){
		for(int i=1;i<r[0];i++)	maxlen+=r[i];
		printf("%d",maxlen);
	}else{
		for(int i=1;i<r[0];i++){
			int a=i+1,b=i+2,c=i+3,d=i-1;
			if(d<=0)	d=r[0]-1;
			if(a>=r[0])	a=a-r[0]+1;
			if(b>=r[0])	b=b-r[0]+1;
			if(c>=r[0])	c=c-r[0]+1;
			int t=r[i]+r[a];
			zz=0;
			if(flag[i]==1||flag[a]==1&&r[0]>3){
				t+=r[b];zz++;
				if(flag[c]==1&&r[0]>3+zz){
					t+=r[c];
					zz++;
				}	
			}
			if(r[0]>3+zz&&flag[d]==1){
				t+=r[d];
			}
			maxlen=max(t,maxlen);
		}
	}
	printf("%d",maxlen);
	return 0;
}
```


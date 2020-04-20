# [P1827 [USACO3.4]美国血统 American Heritage](https://www.luogu.com.cn/problem/P1827)

## 题目描述

农夫约翰非常认真地对待他的奶牛们的血统。然而他不是一个真正优秀的记帐员。他把他的奶牛 们的家谱作成二叉树，并且把二叉树以更线性的“树的中序遍历”和“树的前序遍历”的符号加以记录而 不是用图形的方法。

你的任务是在被给予奶牛家谱的“树中序遍历”和“树前序遍历”的符号后，创建奶牛家谱的“树的 后序遍历”的符号。每一头奶牛的姓名被译为一个唯一的字母。（你可能已经知道你可以在知道树的两 种遍历以后可以经常地重建这棵树。）显然，这里的树不会有多于 26 个的顶点。 这是在样例输入和 样例输出中的树的图形表达方式：

```
　　　　　　　　 C
　　　　　　   /  \
　　　　　　  /　　\
　　　　　　 B　　  G
　　　　　　/ \　　/
　　　　   A   D  H
　　　　　　  / \
　　　　　　 E   F
```

树的中序遍历是按照左子树，根，右子树的顺序访问节点。

树的前序遍历是按照根，左子树，右子树的顺序访问节点。

树的后序遍历是按照左子树，右子树，根的顺序访问节点。

## 输入格式

第一行： 树的中序遍历

第二行： 同样的树的前序遍历

## 输出格式

单独的一行表示该树的后序遍历。

## 输入输出样例

**输入 #1**复制

```
ABEDFCHG
CBADEFGH 
```

**输出 #1**复制

```
AEFDBHGC
```

## 说明/提示

题目翻译来自NOCOW。

USACO Training Section 3.4



***

简单递归。找规律，分成三部分。

注意最后的空格可能出错。

***



```c++
#include <bits/stdc++.h>
using namespace std;
char ch[50];
void fun(int start,string a,string b){
	if(a.length()==1){
		ch[start]=a[0];
		return;
	}else if(a.length()==0)	return;
	char z=b[0];
	int t=a.find(b[0]);
	ch[start+a.length()-1]=b[0];
	fun(start,a.substr(0,t),b.substr(1,t));
	fun(start+t,a.substr(t+1),b.substr(t+1));
	return;
}
int main(){
    string a,b;
    getline(cin,a);
    getline(cin,b);
    fun(0,a,b);
    for(int i=0;i<a.length();i++)
        if(ch[i]>='A'&&ch[i]<='Z')
		    printf("%c",ch[i]);
    return 0;
}
```


# [[P1825 [USACO11OPEN]Corn Maze S](https://www.luogu.com.cn/problem/P1825)

## 题目描述

This past fall, Farmer John took the cows to visit a corn maze. But this wasn't just any corn maze: it featured several gravity-powered teleporter slides, which cause cows to teleport instantly from one point in the maze to another. The slides work in both directions: a cow can slide from the slide's start to the end instantly, or from the end to the start. If a cow steps on a space that hosts either end of a slide, she must use the slide.

The outside of the corn maze is entirely corn except for a single exit.

The maze can be represented by an N x M (2 <= N <= 300; 2 <= M <= 300) grid. Each grid element contains one of these items:

\* Corn (corn grid elements are impassable)

\* Grass (easy to pass through!)

\* A slide endpoint (which will transport a cow to the other endpoint)

\* The exit

A cow can only move from one space to the next if they are adjacent and neither contains corn. Each grassy space has four potential neighbors to which a cow can travel. It takes 1 unit of time to move from a grassy space to an adjacent space; it takes 0 units of time to move from one slide endpoint to the other.

Corn-filled spaces are denoted with an octothorpe (#). Grassy spaces are denoted with a period (.). Pairs of slide endpoints are denoted with the same uppercase letter (A-Z), and no two different slides have endpoints denoted with the same letter. The exit is denoted with the equals sign (=).

Bessie got lost. She knows where she is on the grid, and marked her current grassy space with the 'at' symbol (@). What is the minimum time she needs to move to the exit space?

去年秋天，奶牛们去参观了一个玉米迷宫，迷宫里有一些传送装置，可以将奶牛从一点到另一点进行瞬间转移。这些装置可以双向使用：一头奶牛可以从这个装置的起点立即到此装置的终点，同时也可以从终点出发，到达这个装置的起点。如果一头奶牛处在这个装置的起点或者终点，这头奶牛就必须使用这个装置。

玉米迷宫的外部完全被玉米田包围，除了唯一的一个出口。

这个迷宫可以表示为N×M的矩阵(2 ≤ N ≤ 300; 2 ≤ M ≤ 300)，矩阵中的每个元素都由以下项目中的一项组成：

 玉米，这些格子是不可以通过的。

 草地，可以简单的通过。

 一个装置的结点，可以将一头奶牛传送到相对应的另一个结点。

 出口

奶牛仅可以在相邻两个格子之间移动，要在这两个格子不是由玉米组成的前提下才可以移动。奶牛能在一格草地上可能存在的四个相邻的格子移动。从草地移动到相邻的一个格子需要花费一个单位的时间，从装置的一个结点到另一个结点需要花费0个单位时间。

被填充为玉米的格子用“#”表示，草地用“.”表示，每一对装置的结点由相同的大写字母组成“A-Z”，且没有两个不同装置的结点用同一个字母表示，出口用“=”表示。

Bessie在这个迷宫中迷路了，她知道她在矩阵中的位置，将Bessie所在的那一块草地用“@”表示。求出Bessie需要移动到出口处的最短时间。

例如以下矩阵，N=5，M=6：

```
###=##
#.W.##
#.####
#.@W##
######
```

唯一的一个装置的结点用大写字母W表示。

最优方案为：先向右走到装置的结点，花费一个单位时间，再到装置的另一个结点上，花费0个单位时间，然后再向右走一个，再向上走一个，到达出口处，总共花费了3个单位时间。

## 输入格式

第一行：两个用空格隔开的整数N和M；

第2-N+1行：第i+1行描述了迷宫中的第i行的情况（共有M个字符，每个字符中间没有空格。）

## 输出格式

一个整数，表示Bessie到达终点所需的最短时间。

## 输入输出样例

**输入 #1**复制

```
5 6
###=##
#.W.##
#.####
#.@W##
######
```

**输出 #1**复制

```
3
```



***



***



```C++

```


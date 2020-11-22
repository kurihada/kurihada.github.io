---
title: 2020-11-21-Educational Codeforces Round 98 (Rated for Div. 2)
tags: ACM
renderNumberedHeading: true
grammar_cjkRuby: true
---
###### [题目传送门](https://codeforces.com/contest/1452)
## A. Robot Program
#### 题目大意
给你一个（x，y）的点，你需要从（0,0）到该点，你可以执行的操作为：
move north from cell `(i,j)` to `(i,j+1)`;
move east from cell `(i,j)` to `(i+1,j)`;
move south from cell` (i,j)` to `(i,j−1)`;
move west from cell `(i,j)` to` (i−1,j)`;
stay in cell `(i,j)`.
不能连续两次以上进行同一操作
求从`(0,0)`到`(x,y)`的最小操作数
#### 思路
可以将x和y轴的移动分离，走x的时候可以选择向右走后停一次或者向上走，即可使得走到的x耗费`2\*n-`，并且可以到达小于x的任意位y
所以得出公式为
$$ f(x)=\left\{
\begin{aligned}
x\*y & = & x==y \\
2\*min(x,y)-1 & else xy
\end{aligned}
\right.
$$

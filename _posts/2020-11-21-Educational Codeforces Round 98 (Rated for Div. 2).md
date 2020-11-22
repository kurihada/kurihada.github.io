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
$$f{(x)}=\left\{
\begin{aligned}
&2*x&&x=y\\
&2*max(x,y)-1&&x!=y\\
\end{aligned} \right.
$$
#### AC Code

``` cpp
#pragma GCC optimize("-Ofast","-funroll-all-loops")
#include<cstdio>
#include<algorithm>
#include<iostream>
#include<cstring>
#include<math.h>
using namespace std;
#define endl '\n'
#define INF 0x3f3f3f3f
// #define int long long
#define debug(a) cout<<#a<<"="<<a<<endl;
typedef long long ll;
const double PI=acos(-1.0);
const double e=exp(1.0);
const int M=1e9+7;
const int N=2e5+7;
inline int mymax(int x,int y){return x>y?x:y;}
inline int mymin(int x,int y){return x<y?x:y;}
int x, y;
void solve(){
    cin>>x>>y;
    if(x==y) cout<<2*x<<endl;
    else{
        cout<<2*mymax(x,y)-1<<endl;
    }
    return ;
}
signed main(){
    int T;
    cin>>T;
    while(T--) solve();
    return 0;
}
```
## B. Toy Blocks
#### 题目大意
给你n个盒子，每个盒子中有$a_i$个积木
你可以将任意个积木放到n个盒子中，使得任意选中一个i，将$a_i$中的所有积木放到其他n-1个盒子中，存在一种方案能够使n-1个盒子中的积木数量相等。
问你需要放入的最小的积木数
#### 思路
一般需要保证$sum\ \ mod\ \ (n-1)=0$保证积木在$n-1$个盒子中能相等
在不选择最大时需要保证$n-1$个盒子中的数量均为$max$
所以最终在放完后，每个盒子的积木数量应该为$max(max,⌈sumn−1⌉)$
#### AC Code

``` cpp
#pragma GCC optimize("-Ofast","-funroll-all-loops")
#include<cstdio>
#include<algorithm>
#include<iostream>
#include<cstring>
#include<math.h>
using namespace std;
#define endl '\n'
#define INF 0x3f3f3f3f
#define int long long
#define debug(a) cout<<#a<<"="<<a<<endl;
typedef long long ll;
const double PI=acos(-1.0);
const double e=exp(1.0);
const int M=1e9+7;
const int N=2e5+7;
inline int mymax(int x,int y){return x>y?x:y;}
inline int mymin(int x,int y){return x<y?x:y;}
int n, x;
int mx, sum;
void solve(){
	mx=sum=0;
	cin>>n;
	for(int i=1; i<=n; i++){
		cin>>x;
		sum+=x;
		mx=mymax(mx,x);
	}
	int h=mymax(mx,(sum+n-2)/(n-1));	// 求出最终放完后每个盒子的积木
	cout<<h*(n-1) - sum<<endl;			// 算出需要添加的积木数
	return ;
}
signed main(){
	int T;
	cin>>T;
	while(T--) solve();
	return 0;
}
```
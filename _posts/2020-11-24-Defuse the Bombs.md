---
title: 2020-11-24-Defuse the Bombs
tags: 新建,模板,小书匠
renderNumberedHeading: true
grammar_cjkRuby: true
---
## [Defuse the Bombs（二分答案）](https://codeforces.ml/gym/102822/problem/D)
#### 题目大意
给你一个长度为n的序列代表炸弹时长，你需要按顺序执行以下操作：
1、选择一个炸弹，使其时长增加1。
2、其余所有的炸弹时长减少1。
3、如果至少一个炸弹时长低于0，则爆炸。 否则，请返回步骤1。
问最多可以执行多少次步骤1
#### 思路
二分答案，二分最多的不爆炸时间
计算小于当前二分的最大时间的炸弹的时长的和$sum$
判断$sum$的值是否小于当前二分的最大时间，如果小于则$l$右移，因为在二分的最大时间中可以操作的次数大于爆炸的时间，即炸弹不会爆炸，所以$l$右移，否则$r$左移
会爆$int$
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
#define debug(a) cout<<#a<<"="<<a<<endl;
typedef long long ll;
const double PI=acos(-1.0);
const double e=exp(1.0);
const int M=1e9+7;
const int N=2e5+7;
inline int mymax(int x,int y){return x>y?x:y;}
inline int mymin(int x,int y){return x<y?x:y;}
int n, k, a[N];
ll l, r, mid;

bool check(ll now){
	ll sum=0;
	for(int i=1; i<=n; i++) if(a[i]<now) sum+=now-a[i];
	if(sum<=now) return false;
	return true;
}

void solve(){
	cin>>n;
	for(int i=1; i<=n; i++) cin>>a[i];
	ll ans=1;
	l=0, r=2e9;
	while(l<=r)
	{
		mid=(l+r)>>1;
		if(check(mid)) 	r=mid-1;
		else 			ans=mid+1, l=mid+1;
	}
	printf("Case #%d: %lld\n", ++k, ans);
	return ;
}
signed main(){
	int T;
	cin>>T;
	while(T--) solve();
	return 0;
}
```
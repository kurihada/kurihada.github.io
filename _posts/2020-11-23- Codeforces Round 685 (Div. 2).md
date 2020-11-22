---
title: 2020-11-23- Codeforces Round 685 (Div. 2)
tags: ACM,codeforces
renderNumberedHeading: true
grammar_cjkRuby: true
---
###### [题目传送门](https://codeforces.ml/contest/1451)
## A. Subtract or Divide
#### 题目大意
给你一数n，你可以进行下列操作
用n除以其适当除数之一
如果n大于1，则从n中减去1
适当除数（数字的除数，不包括其本身）
求最小操作数使得n变成1
#### 思路
特判1,2,3的操作次数，分别为0,1,2
当一个数字为奇数时先减一，再变成2，再减一即可变成1，操作3次
偶数直接变成2，再减一即可变成1，操作两次
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
int n;
void solve(){
    cin>>n;
    if(n==1) {cout<<"0"<<endl; return ;}
    if(n==2) {cout<<"1"<<endl; return ;}
    if(n==3) {cout<<"2"<<endl; return ;}
    if(n&1) cout<<"3"<<endl;
    else    cout<<"2"<<endl;
    return ;
}
signed main(){
    int T;
    cin>>T;
    while(T--) solve();
    return 0;
}
```
---
title: 2020-11-22- Codeforces Round 684 (Div. 2)
tags: ACM,codeforces
renderNumberedHeading: true
grammar_cjkRuby: true
---
###### [题目传送门](https://codeforces.com/contest/1440)
## A. Buy the String
#### 题目大意
给你n个零件和和购买零件1和0分别需要的钱，以及将一个零件转换成另外一种零件对应的钱
给你一个01序列代表零件的情况，问买下n个零件所需的最小值
#### 思路
先统计01序列中0和1分别的个数，考虑不转化直接求花费和转化1求花费和转化0求花费后取三者最小即可
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
int n, c0, c1, num0, num1, h;
int sum1, sum2, sum3;
string s;
void solve(){
    cin>>n>>c0>>c1>>h;
    cin>>s;
    num0=num1=0;
    for(int i=0; i<s.length(); i++){
        if(s[i]=='1') num1++;
        else          num0++;
    }
    sum1=num0*c0+num1*c1;
    sum2=h*num0+num0*c1+num1*c1;
    sum3=h*num1+num1*c0+num0*c0;
    cout<<mymin(sum1,mymin(sum2,sum3))<<endl;
    return ;
}
signed main(){
    int T;
    cin>>T;
    while(T--) solve();
    return 0;
}
```

## B. Sum of Medians
#### 题目大意
给你一个长度为n\*k的序列a，求将字符串分成k组后每组的中位数的和最大的值
#### 思路
题目给的序列有序就不需要排序了
显然想要构造一个较大的中位数之和，需要将序列a前面的数放在每个组的前面的部分，然取中位数然后每隔n/2就跳到下一个组
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
int n, k, a[N];
void solve(){
    cin>>n>>k;
    for(int i=1; i<=n*k; i++) cin>>a[i];
    int l=1,r=n*k;
    int ans=0;
    int m=(n+1)/2;
    while(l<=r)
    {
        r-=n-m;
        ans+=a[r];
        r--;
        l+=m-1;
    }
    cout<<ans<<endl;
    return ;
}
signed main(){
    int T;
    cin>>T;
    while(T--) solve();
    return 0;
}
```
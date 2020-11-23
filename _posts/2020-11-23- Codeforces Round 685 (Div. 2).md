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
## B. Non-Substring Subsequence
#### 题目大意
给你一个长度为$n$的$01$字符串和$m$次询问。
每个询问一个区间$l,r$，为一个子串
问在原字符串是否存在一个子串与询问的区间子串相等
#### 思路
只需要考虑询问的区间$l,r$的左边是否存在与$s[l]$相同的字符，右边是否存在与$s[r]$相同的字符，有其一即可
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
int n, q, l, r;
string s;
void solve(){
    cin>>n>>q;
    cin>>s;
    for(int k=1; k<=q; k++){
        int flag=1;
        cin>>l>>r; l--, r--;
        if(l==r) {cout<<"NO"<<endl; continue;}
        for(int i=0; i<l; i++) if(s[i]==s[l]) {cout<<"YES"<<endl; flag=0; break;}
        if(flag) for(int i=r+1; i<s.length(); i++) if(s[r]==s[i]) {cout<<"YES"<<endl; flag=0; break;}
        if(flag) cout<<"NO"<<endl;
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
## C. String Equality
#### 题目大意
给你两个长度为n的字符串a，b，你可以执行下列操作：
选择索引$i（1≤i≤n-1)$并交换$a_i$和$a_i + 1$
选择索引$i（1≤i≤n-k+1)$，如果$a_i，a_{i+1}，...，a_{i-k+1}$都等于某个字符$c（c≠z）$，将每个字符替换为下一个字符$c + 1$，即$a$替换为$b$，$b$替换为$c$，依此类推。
求是否可以将字符串a变成b
#### 思路
分别记录字符串a和b中每个字母出现的次数
用a的当前字符匹配对应的b的位置，a当前字符的数量必须大于等于b，因为每次字符替换必须操作k个数，所以匹配完后剩下的字符数目必须为k的整数倍
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
int n, k;
string a, b;
int suma[30], sumb[30];
void solve(){
	cin>>n>>k;
	cin>>a>>b;
	memset(suma,0,sizeof(suma));
	memset(sumb,0,sizeof(sumb));
	for(int i=0; i<a.length(); i++) ++suma[a[i]-'a'], ++sumb[b[i]-'a'];
	for(int i=0; i<26; i++){
		if(suma[i]<sumb[i]) {cout<<"NO"<<endl; return ;}
		suma[i]-=sumb[i];
		if(suma[i]%k) {cout<<"NO"<<endl; return ;}
		suma[i+1]+=suma[i];
	}
	cout<<"YES"<<endl;
	return ;
}
signed main(){
	int T;
	cin>>T;
	while(T--) solve();
	return 0;
}
```
## D. Circle Game（对称博弈）
#### 题目大意
给你一个半径d和步数k
你从原点$(0,0)$开始走，每次选择让x坐标增加k，或者y坐标增加k
假设走后坐标为$(p,q)$，需要保证$p^2+q^2≤d^2$
两人轮流走，最后不能走的人输， Ashish先手
#### 思路
对称博弈，每次后手都可以抵消先手的操作，先手右后手上，先手上后手右，使得坐标一直维持$(z,z)$
所以我们可以求得最远的$(z,z)$，如果还能继续走即$(z,z+k)$是可达的，$z^2+(z+k)^2<=d^2$满足，则先手必胜，可以先手可以反过来抵消后手的操作，使得他一直可达$(z,z+k)$，否则后手必胜
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
int d, k;
void solve(){
	cin>>d>>k;
	int z=0;
	while (2*(z+k)*(z+k)<=d*d)	z+=k;
	if((z+k)*(z+k) + z*z <= d*d) cout<<"Ashish"<<endl;
	else 						 cout<<"Utkarsh"<<endl;
	return ;
}
signed main(){
	int T;
	cin>>T;
	while(T--) solve();
	return 0;
}
```
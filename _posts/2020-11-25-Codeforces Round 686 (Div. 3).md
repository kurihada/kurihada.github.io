---
title: 2020-11-25-Codeforces Round 686 (Div. 3)
tags: ACM,codeforces
renderNumberedHeading: true
grammar_cjkRuby: true
---

###### [题目传送门](https://codeforces.ml/contest/1454)
## A. Special Permutation
#### 题目大意
给你一个n，构造一个长度为n的序列，满足$p_i≠i(1<=i<=n)$
#### 思路
1~n整体右移一位即可
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
void solve(){
    int n;
    cin>>n;
    cout<<n<<" ";
    for(int i=1; i<n; i++) cout<<i<<" ";
    cout<<endl;
    return ;
}
signed main(){
    int T;
    cin>>T;
    while(T--) solve();
    return 0;
}
```
## B. Unique Bid Auction
#### 题目大意
给你一个长度为n的序列a，求其中只出现了一次并且最小的值
#### 思路
开个map容器记录当前元素出现次数和下标即可（可以用pair存）
#### AC Code
```cpp
#pragma GCC optimize("-Ofast","-funroll-all-loops")
#include<cstdio>
#include<algorithm>
#include<iostream>
#include<cstring>
#include<math.h>
#include<map>
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
inline int read(){
    register int x=0, f=0;
    register char ch=getchar();
    while(ch<'0'||ch>'9') f|=ch=='-',ch=getchar();
    while(ch>='0'&&ch<='9') x=(x<<3)+(x<<1)+(ch^48),ch=getchar();
    return f?-x:x;
}
map<int,pair<int,int>>mp;
int n, x;
void solve(){  
    mp.clear();
    n=read();
    for(int i=1; i<=n; i++){
        x=read();
        mp[x].first++; mp[x].second=i;
    }
    for(auto v:mp) if(v.second.first==1) {cout<<v.second.second<<endl; return ;}
    cout<<"-1"<<endl;
    return ;
}
signed main(){
    int T;
    T=read();
    while(T--) solve();
    return 0;
}
```
## C. Sequence Transformation
#### 题目大意
给你一个长度为n的序列a，你可以选择序列中任意一个数
删除除了选中的数以外的数，每次删除的区间不能包含选中数
求最小删除的次数
#### 思路
首先对序列进行去重
然后统计每个数字出现的次数，因为每出现一次需要多一次删除操作，操作次数初始化为1，最后特殊处理一下头尾，即--
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
int n, x, a[N], b[N];
void solve(){
	cin>>n;
	for(int i=1; i<=n; i++) cin>>a[i];
	b[1]=a[1];
	int k=1;
	for(int i=2; i<=n; i++) if(a[i]!=b[k]) b[++k]=a[i];
	if(k==1) {cout<<"0"<<endl; return ;}
	for(int i=1; i<=n; i++) a[i]=1;
	for(int i=1; i<=k; i++) a[b[i]]++;
	a[b[1]]--; a[b[k]]--;
	int mn=INF;
	for(int i=1; i<=k; i++) mn=mymin(mn,a[b[i]]);
	cout<<mn<<endl;
	return ;
}
signed main(){
	int T;
	cin>>T;
	while(T--) solve();
	return 0;
}
```
vector版本：

``` cpp
#pragma GCC optimize("-Ofast","-funroll-all-loops")
#include<cstdio>
#include<algorithm>
#include<iostream>
#include<cstring>
#include<math.h>
#include<vector>
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
	vector<int>a(n);
	vector<int>ans(n+1,1);
	for(int i=0; i<n; i++) cin>>a[i];
	n=unique(a.begin(), a.end()) - a.begin();
	a.resize(n);
	for(int i=0; i<n; i++) ans[a[i]]++;
	ans[a[0]]--; ans[a[n-1]]--;
	int mn=INF;
	for(int i=0; i<n; i++) mn=mymin(mn,ans[a[i]]);
	cout<<mn<<endl;
	return ;
}
signed main(){
	int T;
	cin>>T;
	while(T--) solve();
	return 0;
}
```
## D. Number into Sequence
#### 题目大意
给你一个数$n(2≤n≤10^{10})$，求满足下列条件的最长序列
每个$a_i$都严格大于$1$；
$a_1⋅a_2⋅...⋅a_k=n$（即此序列的乘积为n）;
对于每个$i$，$a_i + 1$可被$a_i$整除，从$1$到$k-1$；
$k$是最大可能值（即此序列的长度是最大可能值）
#### 思路
素数筛打表$1e5$，判断n对其中素数是否能整除，求出对于该数的最大倍数，答案即为最长的倍数的素数的，个数为可以除的次数
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

bool vis[N];
ll prime[N], p[N], x;
void oulasai(int n)
{
    vis[1]=1;
    for(int i=2;i<=n;i++)
    {
        if(!vis[i]) prime[x++]=i, p[i]=i;
        for(int j=0;j<x;j++)
        {
            if(i*prime[j]>n) break;
            vis[i*prime[j]]=true;
            p[i*prime[j]]=prime[j];
            if(i%prime[j]==0) break;
        }
    }
} 
ll n;
void solve(){
    cin>>n;
    ll mx=1, idx=-1;
    for(int i=0; i<x; i++){
        if(n%prime[i]==0){
            ll ans=0, now=n;
            while(now%prime[i]==0){
                ++ans;
                now/=prime[i];
            }
            if(ans>mx){
                mx=ans;
                idx=prime[i];
            }
        }
    }
    cout<<mx<<endl;
    for(int i=1; i<=mx-1; i++){
        cout<<idx<<" ";
        n/=idx;
    }
    cout<<n<<endl;
    return ;
}
signed main(){
    oulasai(1e5);
    int T;
    cin>>T;
    while(T--) solve();
    return 0;
}
```
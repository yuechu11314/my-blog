---
author: yuechuchu_11
pubDatetime: 2026-10-15T12:00:00Z
title: Codeforces edu195c 题解：前缀和，数论
description: 日常补题
tags:
  - cf
  - 算法竞赛
---

## 题目链接:https://codeforces.com/contest/2276/problem/C

## 题目大意
给定大小为n的数组a与整数k(k<n),求满足以下条件子串:

1.[l,r]子串中所有元素和能被k整除.

2.[l,r]字串长度严格大于k.

数据范围为1<=k<n<=2*10^5,1<=t<=10^4,1<=a_i<=10^9.


## 解题思路
通过1可推导得到(sum[r]-sum[l-1])%k = 0继续推导得到sum[r]%k = sum[l-1]%k

注意到数据范围最多可容纳o(n)解法，双指针全扫一遍的复杂度是o(n^2)

从推导公式可以想到我们只关心子串和对k取模的余数

那我们不妨这样想：把双指针的余数进行匹配，也就是说把l指针的已经对k取模的前缀和和后面r指针的前缀和进行匹配


## 代码实现
```cpp
#include<bits/stdc++.h>
#define int long long
using namespace std;

void solve(){
	int n,k;
	cin>>n>>k;
	vector<int>a(n+1);
	vector<int>sum(n+1);
	sum[0] = 0;
	for(int i = 1;i<=n;i++){
		cin>>a[i];
		sum[i] = (sum[i-1] + a[i])%k;
	}
	vector<int>cnt(k,0);
	int ans = 0;
	for(int r = k+1;r<=n;r++){
		int new_l = r-k-1;
		cnt[sum[new_l]]++;
		ans += cnt[sum[r]];
	}
	cout<<ans<<endl;
}

signed main(){
	int t;
	cin>>t;
	while(t--){
		solve();
	}
}

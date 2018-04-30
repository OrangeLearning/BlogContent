---
title: Codeforce-501E
date: 2018-04-22 22:28:43
tags: [algorithm,binary_search]
---
来源：CF501E

突然觉的CF的题真的可以学到不少东西。

题意，就是对于一个数字组成的串，我们可以改变l,r之间的所有数的顺序，使得整个串是回文串，问l和r各有多少种取法

```cpp    
    #include <iostream>
    #include <cstdio>
    #include <cstring>
    #include <algorithm>
    #include <cmath>
    
    using namespace std;
    const int MAXN = 1e5+10;
    int n;
    int a[MAXN];
    int has[MAXN],hasout[MAXN];
    deque<int>Q;
    inline bool in(int p,int l,int r){//判断p是否在一个区间中
    	if(l<=p&&p<=r) return true;
    	else return false;
    }
    bool judge(int l,int r){
    	for(int i=1;i<=n;i++) hasout[i] = 0;//初始化
    	for(int i=l;i<=r;i++) hasout[a[i]]++;//记录所有的个数
    	for(int i=1;i<=n;i++){
    		if(!in(i,l,r) && !in(n+1-i,l,r)) {
    			if(a[i]!=a[n+1-i]) return false;//如果在我无法调整的地方有不回文的，那就不用说了
    		}
    		if(!in(i,l,r) && in(n-i+1,l,r)) hasout[a[i]]--;//不在里面，但是对应在里面，我们就需要调整里面一个给它
    	}
    	for(int i=1;i<=n;i++) if(hasout[a[i]]<0) return false;//如果有一个小于0，说明我们的有一个调整不起来
    	return true;
    }
    int main(){
    	long long ans = 0;
    	scanf("%d",&n);
    	for(int i=1;i<=n;i++){
    		scanf("%d",a+i);
    		has[a[i]]++;//记录所有的个数
    	}
    
    	int du = 0,flag=1;
    	for(int i=1;i<=n;i++) {
    		if(a[i]!=a[n-i+1]) flag=0;//如果本身串不是回文串
    		du += (has[i]&1);
    	}
    	if(du>1) {//如果奇数有多个，那必然不成立
    		puts("0");
    		return 0;
    	}
    	if(flag){//如果本身是回文串，那么任意两个数构成的区间都一定是结果，因为我完全不调整就对了
    		cout<<(long long)n*(n+1)/2<<endl;
    		return 0;
    	}
    
    	du = 1;
    	while(a[du]==a[n+1-du]) ++du;
    	//不需要调整的个数，两边已经成立了
    
    	//下面就是最关键的东西
    	int l=du,r=n,mid=0,res;
    	//我们来看一下下面是二分的是什么意思
    	//取出了一个满足的最小的l
    	while(l<=r){
    		mid = (l+r)>>1;
    		if(judge(du,mid)) {
    			r=mid-1;
    			res = mid;
    		}
    		else l =mid+1;
    	}
    
    	ans=(long long) du*(n-res+1);
    	//n+1-res就是一个求出的最小的位置满足du到res的位置是满足的位置的逆反位置
    	//所以du是l所有方法数，n-res+1是所有r的方法数
    	//同理，反转之后就取出了最大的满足题意的位置
    	reverse(a+1,a+n+1);
    	l=du;r=n;
    
    	while(l<=r) {
    	   mid = (l+r)>>1;
    	   if(judge(du,mid)){
    	 		r=mid-1;
    	 		res = mid;
    	   }
    	   else l=mid+1;
    	}
    	ans+=(long long) du*(n-du-res+1);
    	cout<<ans<<endl;
    	return 0;
    }
```

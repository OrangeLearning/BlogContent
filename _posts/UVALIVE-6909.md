---
title: UVALIVE-6909
date: 2018-04-22 22:29:01
tags: [algorithm,math]
---
来源：UVALIVE6909

组合数学裸题

注意最后一个取模

代码：

```cpp    
    #include <iostream>
    #include <cstdio>
    #include <cstring>
    #include <algorithm>
    using namespace std;
    typedef long long LL;
    LL n,m,p;
    const LL MAXN = 1010;
    const LL MOD = 1000000007;
    LL fac[MAXN];
    LL a[MAXN][MAXN];
    void ini(){
    	fac[0] = 1;
    	fac[1] = 1;
    	for(LL i=2;i<MAXN;i++){
    		fac[i] = fac[i-1]*i%MOD;
    	}
    }
    void init(){
    	memset(a,0,sizeof(a));
    	a[0][0] = 1;
    	for(int i=1;i<MAXN;i++){
    		a[i][0] = 1;
    		for(int j=1;j<=i;j++)
    			a[i][j] = (a[i-1][j-1]+a[i-1][j])%MOD;
    	}
    }
    int main(){
    	int T,nc=1;
    	ini();
    	init();
    	scanf("%d",&T);
    	while(T--){
    		scanf("%lld%lld%lld",&n,&m,&p);
    		LL ans = 0;
    		ans = (n-p)*fac[n-2]%MOD;
    		for(LL i=m+2;i<=n;i++){
    			for(LL j=p+1;j<=n;j++){
    				ans += (fac[n-(i-m+1)]%MOD)*(a[j-2][i-m-1]%MOD)%MOD;
    			}
    		}
    		ans += (a[p-1][n-m]%MOD)*(fac[m-1]%MOD)%MOD;
    		printf("Case #%d: %lld\n",nc++,ans%MOD);
    	}
    	return 0;
    }

```

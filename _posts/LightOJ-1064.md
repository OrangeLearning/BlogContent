---
title: LightOJ-1064
date: 2018-04-22 22:29:25
tags: [algorithm,DP]
---

来源：lightOJ1064

很水的DP

代码：

```cpp    
    #include <iostream>
    #include <cstdio>
    #include <cstring>
    #include <algorithm>
    using namespace std;
    typedef long long LL;
    int n,x;
    const int MAXN = 200;
    const int N = 50; 
    LL dp[N][MAXN];
    LL a[N];
    inline LL gcd(LL a,LL b) {
        if(!b) return a;
        else return gcd(b,a%b);
    }
    inline void ini(){
        a[0] = 1;
        a[1] = 6;
        for(int i=2;i<N;i++) a[i] = a[i-1]*6;
        return ;
    }
    inline void DP(){
        memset(dp,0,sizeof dp);
        for(int i=1;i<=6;i++) dp[1][i] = 1;
        for(int i=1;i<=26;i++) {
            for(int j=1;j<=i*6;j++){
                if(!dp[i][j]) continue;
                for(int k=1;k<=6;k++){
                    dp[i+1][j+k] += dp[i][j];
                }
            }
        }
    }
    int main(){
        int T,nc = 1;
        ini();
        DP();
        scanf("%d",&T);
        while(T--){
            scanf("%d%d",&n,&x);
            LL sum = 0,ans = 0;
            int maxn = n*6;
            printf("Case %d: ",nc++);
            if(x>maxn) {
                puts("0");
                continue;
            }
            for(int i=x;i<=maxn;i++) {
                ans += dp[n][i];
            }
            sum = a[n];
            if(sum == ans ){
                puts("1");
                continue;
            }
            LL tmp = gcd(ans,sum);
            printf("%lld/%lld\n",ans/tmp,sum/tmp);
        }
    
        return 0;
    }
```
---
title: LightOJ-1028
date: 2018-04-22 22:29:34
tags: [algorithm,math]
---
来源：lightOJ1028

为了节约时间，先处理处所有的素数，但是注意不要进行素因子分解，因为没有必要，而且这个步骤浪费时间，直接不断的去除就好了

代码：

    
```cpp 
    #include <iostream>
    #include <cstdio>
    #include <cstring>
    #include <algorithm>
    #include <cmath>
    using namespace std;
    typedef long long LL;
    const int N = 1e6+10;
    const int MAXN = 1e6+10;
    LL n;
    LL p[MAXN];
    bool vis[N];
    //int nn[MAXN];
    int cnt;
    void init(){
        cnt = 0;
        memset(vis,false,sizeof vis);
        for(int i=2;i<N;i++) {
    //        cout<<"i = "<<i<<endl;
            if(!vis[i]) p[cnt++] = i;
            for(int j=0;j<cnt && p[j]*i<N ; j++){
    //            cout<<"j = "<<j<<endl;
                vis[i*p[j]] = 1;
                if(i % p[j] == 0) break;
            }
        }
    }
    int main(){
        init();
        int T,nc = 1;
        scanf("%d",&T);
        while(T--){
            scanf("%lld",&n);
            int ans = 1;
            for(int i=0;i < cnt && p[i] * p[i] <= n;i++) {
                if(n%p[i]==0){
                    int nn = 0;
                    while(n%p[i] == 0){
                        nn ++;
                        n /= p[i];
                    }
                    ans *= (1+nn);
                }
            }
            if(n>1) ans *= 2;
            printf("Case %d: %d\n",nc++,ans-1);
        }
        return 0;
    }
    
```

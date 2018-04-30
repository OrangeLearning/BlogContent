---
title: LightOJ-1199
date: 2018-04-22 22:29:23
tags: [algorithm,NIM]
---
来源：lightOJ1199

博弈水题啊

代码：

    
```cpp
    #include <iostream>
    #include <cstdio>
    #include <cstring>
    #include <algorithm>
    using namespace std;
    int n,m;
    int x;
    int main(){
        int T,nc = 1;
        scanf("%d",&T);
        while(T--){
            scanf("%d%d",&n,&m);
            int ans = 0;
            for(int i=1;i<=n;i++){
                for(int j=1;j<=m;j++){
                    scanf("%d",&x);
                    if((i+j)%2 != (n+m)%2) {
                        ans ^= x;
                    }
                }
            }
            printf("Case %d: ",nc++);
            if(!ans) puts("lose");
            else puts("win");
        }
        return 0;
    }
    
```

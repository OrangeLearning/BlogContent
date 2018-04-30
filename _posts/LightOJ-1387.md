---
title: LightOJ-1387
date: 2018-04-22 22:31:33
tags: [algorithm,simple]
---
来源：lightOJ 1387

代码：

    
```cpp
    #include <iostream>
    #include <cstdio>
    #include <cstring>
    #include <algorithm>
    using namespace std;
    typedef long long LL;
    int main(){
        int T,nc = 1;
        scanf("%d",&T);
        while(T--)
        {
            int n;
            scanf("%d",&n);
            LL ans = 0;
            char op[20];
            printf("Case %d:\n",nc++);
            while(n--){
                scanf("%s",op);
                if(op[0] == 'd') {
                    LL d;
                    scanf("%lld",&d);
                    ans += d;
                }
                else if(op[0] == 'r'){
                    printf("%lld\n",ans);
                }
            }
        }
        return 0;
    }

```

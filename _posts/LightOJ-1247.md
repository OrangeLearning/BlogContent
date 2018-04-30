---
title: LightOJ-1247
date: 2018-04-22 22:29:07
tags: [algorithm,NIM]
---
来源：lightoj1247

代码：

```cpp    
    #include <iostream>
    #include <cstdio>
    #include <cstring>
    #include <algorithm>
    using namespace std;
    int n,m;
    const int MAXN = 55;
    int mp[MAXN][MAXN];
    int main(){
        int T,nc=1;
        scanf("%d",&T);
        while(T--){
            scanf("%d%d",&n,&m);
            int ans = 0;
            for(int i=1;i<=n;i++){
                int sum = 0;
                for(int j=1;j<=m;j++){
                    scanf("%d",&mp[i][j]);
                    sum += mp[i][j];
                }
                ans ^= sum;
            }
            printf("Case %d: ",nc++);
            if(ans) puts("Alice");
            else puts("Bob");
    
        }
        return 0;
    }

```
  


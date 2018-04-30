---
title: LightOj-1047
date: 2018-04-22 22:29:19
tags: [algorithm,DP]
---
来源：lightOJ 1047

简单DP

代码：

    
```cpp
    #include <iostream>
    #include <cstdio>
    #include <cstring>
    #include <algorithm>
    using namespace std;
    int n;
    const int MAXN = 25;
    const int INF = 0x3f3f3f3f;
    int mp[MAXN][3];
    int dp[MAXN][3];
    int DP(){
        for(int i=0;i<=n+2;i++){
            for(int j=0;j<3;j++){
                dp[i][j] = INF;
            }
        }
        for(int i=0;i<3;i++) dp[1][i] = mp[1][i];
        for(int i=2;i<=n;i++){
            for(int newcol=0;newcol<3;newcol++){
                for(int col=0;col<3;col++){
                    if(newcol == col) continue;
                    dp[i][newcol] = min(dp[i][newcol],dp[i-1][col]+mp[i][newcol]);
                }
            }
        }
        int ans = INF;
        for(int i=0;i<3;i++) ans = min(ans,dp[n][i]);
        return ans;
    }
    int main(){
        int T,nc = 1;
        scanf("%d",&T);
        while(T--){
            scanf("%d",&n);
            for(int i=1;i<=n;i++){
                for(int j=0;j<3;j++) {
                    scanf("%d",&mp[i][j]);
                }
            }
            printf("Case %d: %d\n",nc++,DP());
        }
        return 0;
    }
    
```


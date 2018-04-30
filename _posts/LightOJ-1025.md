---
title: LightOJ-1025
date: 2018-04-22 22:29:13
tags: [algorithm,DP]
---
来源：lightOJ 1025

区间DP，构造回文串，还是比较简单的，注意longlong

代码：

    
```cpp 
    #include <iostream>
    #include <cstdio>
    #include <cstring>
    #include <algorithm>
    using namespace std;
    const int MAXN = 70;
    char ch[MAXN];
    long long dp[MAXN][MAXN];
    int main(){
        int T,nc = 1;
        scanf("%d",&T);
        getchar();
        while(T--){
            gets(ch);
            int n = strlen(ch);
            memset(dp,0,sizeof dp);
           // for(int i=0;i<n;i++) dp[i][i] = 1;
            for(int l=1;l<=n;l++){
    //            cout<<"len = "<<l<<endl;
                for(int i=0;i+l-1<n;i++){
                    int j = i+l-1;
    //                cout<<i<<" "<<j<<" ";
                    dp[i][j] += dp[i+1][j];
                    dp[i][j] += dp[i][j-1];
                    if(ch[i] == ch[j]) dp[i][j] ++;
                    else dp[i][j] -= dp[i+1][j-1];
    //                cout<<dp[i][j]<<endl;
                }
            }
            printf("Case %d: %lld\n",nc++,dp[0][n-1]);
        }
    
        return 0;
    }
    
```

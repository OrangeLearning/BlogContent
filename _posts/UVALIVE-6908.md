---
title: UVALIVE-6908
date: 2018-04-22 22:29:03
tags: [algorithm,DP]
---
来源：UVALIVE6908

dp水题

代码：

    
```cpp
    #include <iostream>
    #include <cstdio>
    #include <cstring>
    #include <algorithm>
    using namespace std;
    int n,K,E;
    const int MAXN = 1010;
    int a[MAXN];
    const int INF = 0x3f3f3f3f;
    int dp[MAXN][55][12][5];
    int en[]= {0,4,8,11};
    int main(){
    	int T,nc = 1;
    	scanf("%d",&T);
    	while(T--){
    		scanf("%d%d%d",&n,&K,&E);
    		memset(a,0,sizeof(a));
    		for(int i=1;i<=n;i++){
    			scanf("%d",&a[i]);
    		}
    		for(int i=0;i<=n;i++){
    			for(int j=0;j<=E;j++){
    				for(int k=0;k<=K;k++){
    					for(int flag=0;flag<4;flag++){
    						dp[i][j][k][flag] = INF;
    					}
    				}
    			}
            }
            dp[0][E][K][0]   = 0;
            dp[0][E][K-1][1] = 0;
            dp[0][E][K-1][2] = 0;
            dp[0][E][K-1][3] = 0;
            for(int i=0;i<n;i++){
    			for(int j=0;j<=E;j++){
    				for(int k=0;k<=K;k++){
    					for(int flag=0;flag<4;flag++){
                            if(dp[i][j][k][flag] == INF) continue;
                            if(k==0){
    							if(j<flag){
    								dp[i+1][0][k][flag] = min(dp[i][j][k][flag]+a[i+1],dp[i+1][0][k][flag]);
    							}
    							else{
    								if(a[i+1]>=en[flag]){
    									dp[i+1][j-flag][k][flag] = min(dp[i+1][j-flag][k][flag],dp[i][j][k][flag]+a[i+1]-en[flag]);
    								}
    								else{
    									dp[i+1][j-flag][k][flag] = min(dp[i+1][j-flag][k][flag],dp[i][j][k][flag]);
    								}
    							}
                            }
                            else if(k>=1){
    							if(j<flag){
    								dp[i+1][0][k][flag] = min(dp[i][j][k][flag]+a[i+1],dp[i+1][0][k][flag]);
    							}
    							else{
    								if(a[i+1]>=en[flag]){
    									dp[i+1][j-flag][k][flag] = min(dp[i+1][j-flag][k][flag],dp[i][j][k][flag]+a[i+1]-en[flag]);
    								}
    								else{
    									dp[i+1][j-flag][k][flag] = min(dp[i+1][j-flag][k][flag],dp[i][j][k][flag]);
    								}
    							}
    							for(int now=0;now<4;now++){
    								if(now == flag) continue;
    								if(j-now<0){
    									dp[i+1][0][k][now] = min(dp[i][j][k][flag]+a[i+1],dp[i+1][0][k][now]);
    								}
    								else{
    									if(en[now]>=a[i+1]){
    										dp[i+1][j-now][k-1][now] = min(dp[i+1][j-now][k-1][now],dp[i][j][k][flag]);
    									}
    									else{
    										dp[i+1][j-now][k-1][now] = min(dp[i+1][j-now][k-1][now],dp[i][j][k][flag]+a[i+1]-en[now]);
    									}
    								}
    							}
                            }
    					}
    				}
    			}
            }
    		int ans = INF;
    		for(int i=0;i<=E;i++){
    			for(int j=0;j<=K;j++){
    				for(int flag=0;flag<4;flag++){
                        ans = min(ans,dp[n][i][j][flag]);
    				}
    			}
    		}
    		printf("Case #%d: %d\n",nc++,ans);
    	}
    	return 0;
    }
    
```

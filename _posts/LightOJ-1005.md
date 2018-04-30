---
title: LightOJ-1005
date: 2018-04-22 22:25:53
tags: [algorithm,DP]
---

来源：lightoj1005

分析数据只有30，所以以为long long 可以放心大胆的存下来，这样直接组合计数就行。。。注意n和k的大小关系*/  
n^2*(n-1)^2 ……*(n-k+1)^2 然后排除重复的k!中情况，这样就是有公式n^2*(n-1)^2
……*(n-k+1)^2/(k!)。但是这个有个问题，就是实现起来需要连乘，然后连除，由于  
不能判断是否可以除，所以只能连乘，溢出，WA  
于是还是要用DP的思想，打表，递推  
dp[n,k]=dp[n,k]*n^2/k;上面那个式子展开就行了，很简单。  
代码，其中因为输出long long 没用lld,WA了5次。。。雾草。。。教训教训

```cpp
    #include <iostream>
    #include <cstdio>
    #include <cstring>
    using namespace std;
    const int MAXN=40;
    long long dp[MAXN][MAXN];
    void ini(){
        memset(dp,0,sizeof(dp));
        for(int i=1;i<35;i++){
            dp[i][0]=1;
            dp[i][1]=i*i;
        }
        for(int i=2;i<35;i++){
            for(int j=2;j<=i;j++){
                dp[i][j]=dp[i-1][j-1]*i*i/j;
            }
        }
    }
    int main(){
    	int T,nc(1);
    	scanf("%d",&T);
    	long long ans;
    	int n,k;
    	ini();
    	while(T--){
            scanf("%d%d",&n,&k);
            if(k>n) {//显然不可能放起来
                ans=0;
            }
            else{
                ans=dp[n][k];
            }
            printf("Case %d: %lld\n",nc++,ans);
    	}
    	return 0;
    }
```
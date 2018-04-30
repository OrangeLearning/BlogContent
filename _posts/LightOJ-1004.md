---
title: LightOJ-1004
date: 2018-04-22 22:25:51
tags: [algorithm,DP]
---
来源：lightoj1004

DP水题，正在补前面的题解。

代码：
```cpp
    #include <iostream>
    #include <cstdio>
    #include <cmath>
    #include <cstring>
    #include <algorithm>
    using namespace std;
    const int MAXN=210;
    int a[MAXN][MAXN];
    long long ans[MAXN][MAXN];
    int main(){
    	int T,nc=1,n;
    	scanf("%d",&T);
    	while(T--){
            memset(a,0,sizeof(a));
            memset(ans,0,sizeof(ans));
            scanf("%d",&n);
            int i,j;
            for(i=1;i<=n;i++){
                for(j=1;j<=i;j++)
                    scanf("%d",&a[i][j]);
            }
            //cout<<n<<" : "<<i<<endl;
            for(i=n+1;i<=2*n-1;i++){
                for(j=1;j<=2*n-i;j++)
                    scanf("%d",&a[i][j]);
            }
            for(i=1;i<=n;i++)
            for(j=1;j<=i;j++){
                ans[i][j]=max(ans[i-1][j],ans[i-1][j-1])+a[i][j];//一直到这一步和数字三角形完全一样
            }
            for(i=n+1;i<=2*n-1;i++)
            for(j=1;j<=n*2-i;j++){
                ans[i][j]=max(ans[i-1][j],ans[i-1][j+1])+a[i][j];
            }
            printf("Case %d: %lld\n",nc++,ans[2*n-1][1]);
    	}
    	return 0;
    }
```
---
title: Codeforces-689D
date: 2018-04-22 22:27:28
tags: [algorithm,st_table,binary_search]
---
来源：C.F.689.D

就是一个二分加上ST表的问题，很好理解，参考了题解的二分姿势

代码：


```cpp    
    #include <iostream>
    #include <cstdio>
    #include <string>
    #include <cstring>
    #include <algorithm>
    #include <cmath>
    using namespace std;
    typedef long long LL;
    const int MAXN = 200010;
    int a[MAXN];
    int b[MAXN];
    int n;
    int dp1[MAXN][20];
    int dp2[MAXN][20];
    void ini(){
        for(int i=0;i<n;i++){
            dp1[i][0]=a[i];
            dp2[i][0]=b[i];
        }
        for(int j=1;(1<<j)-1<n;j++){
            for(int i=0;i+(1<<j)-1<n;i++){
                dp1[i][j]=max(dp1[i][j-1],dp1[i+(1<<(j-1))][j-1]);
                dp2[i][j]=min(dp2[i][j-1],dp2[i+(1<<(j-1))][j-1]);
            }
        }
    }
    int RMQmax(int le,int ri){
        int k=0;
        while((1<<(k+1))<=ri-le+1)k++;
        return max(dp1[le][k],dp1[ri-(1<<k)+1][k]);
    }
    int RMQmin(int le,int ri){
        int k=0;
        while((1<<(k+1))<=ri-le+1) k++;
        return min(dp2[le][k],dp2[ri-(1<<k)+1][k]);
    }
    int main(){
    	LL ans=0,le,ri,tmp1,tmp2,va,vi;
    	scanf("%d",&n);
    	for(int i=0;i<n;i++){
            scanf("%d",&a[i]);
    	}
    	for(int i=0;i<n;i++){
            scanf("%d",&b[i]);
    	}
    	ini();
    	for(int i=0;i<n;i++){
            le=i;
            ri=n-1;
            tmp1=-1;
            while(le<=ri){
                int mid=(le+ri)>>1;
                vi=RMQmin(i,mid);
                va=RMQmax(i,mid);
                if(vi==va){
                    ri=mid-1;
                    tmp1=mid;
                }
                else if(vi>va){
                    le=mid+1;
                }
                else{
                    ri=mid-1;
                }
            }
            if(tmp1!=-1){
                le=i;
                ri=n-1;
                while(le<=ri){
                    int mid=(le+ri)>>1;
                    vi=RMQmin(i,mid);
                    va=RMQmax(i,mid);
                    if(vi==va){
                        le=mid+1;
                        tmp2=mid;
                    }
                    else if(vi>va){
                        le=mid+1;
                    }
                    else{
                        ri=mid-1;
                    }
                }
                ans+=tmp2-tmp1+1;
            }
    	}
    	printf("%lld\n",ans);
    	return 0;
    }
```
---
title: LightOJ-1048
date: 2018-04-22 22:25:40
tags: [algorithm,greedy,binary_search]
---
来源：lightoj1048

这个题目竟然在memset上卡时间。。。

无语了。。。其他的还是很好理解的啊，就不赘述了。。。

    
```cpp  
    #include <iostream>
    #include <cstdio>
    #include <string>
    #include <cstring>
    #include <algorithm>
    #include <cmath>
    #include <queue>
    #include <vector>
    using namespace std;
    
    const int MAXN=10010;
    int dis[MAXN];
    int cnt(0);
    int n,k;
    bool judge(int mid){
        int i(0),j(0);
        int sum=0;
        cnt=0;
        //cout<<"chuanru : "<<mid<<endl;
        for(i=1;i<=n;i++){
            if(dis[i]>mid) return 0;
            if(sum+dis[i]<=mid){
                sum+=dis[i];
            }
            else{
                sum=dis[i];
                cnt++;
            }
        }
        return cnt<=k;
    }
    int main(){
    	int T,nc(1);
    	scanf("%d",&T);
    	while(T--){
            //memset(dis,0,sizeof(dis));
            scanf("%d%d",&n,&k);
            int i;
            n++;
            int left(0),right(0),res;
            for(i=1;i<=n;i++){
                scanf("%d",&dis[i]);
                right+=dis[i];
                left=max(left,dis[i]);
            }
            while(left<=right){
                int mid=(left+right)/2;
                if(judge(mid)){
                    right=mid-1;
                    res=mid;
                }
                else{
                    left=mid+1;
                }
            }
            printf("Case %d: %d\n",nc++,res);
            int sum=0;
            int num(0);
            for(i=1;i<=n;i++){
                if(sum+dis[i]>res||n-i<k-num){
                    printf("%d\n",sum);
                    sum=dis[i];
                    num++;
                }
                else
                    sum+=dis[i];
            }
            printf("%d\n",sum);
    	}
    	return 0;
    }
```
---
title: LightOJ-1236
date: 2018-04-22 22:26:37
tags: [algorithm,math]
---
来源：lightOJ1236

这个还是一个比较水的数论题，关键是打表的时候，使用了一点奇异的姿势，使得我们的素数筛可以用更快的速度出现

直接上代码，没什么好解释的

```cpp    
    #include <iostream>
    #include <cstdio>
    #include <cstring>
    using namespace std;
    const int MAXN = 1e7+5;
    typedef long long LL;
    LL p[MAXN/10];
    bool vis[MAXN];
    int k=0;
    void ini(){//线性素数筛
    	for(int i=2;i<MAXN;i++){
    		if(!vis[i]) p[k++]=i;
    		for(int j=0;j<k&&p[j]*i<MAXN;j++){
    			vis[p[j]*i]=1;
    			if(i%p[j]==0) break;
    		}
    	}
    	/*for(int i=0;i<100;i++)
    		cout<<p[i]<<" ";
    	cout<<endl;*/
    }
    int main(){
    	int T,nc=1;
    	scanf("%d",&T);
    	ini();
    	while(T--){
    		LL ans=1;
    		LL n;
    		scanf("%lld",&n);
    		for(int i=0;i<k;i++){
    			if(p[i]>n/p[i]) break;
    			LL cnt=0;
    			while(n%p[i]==0){
    				n/=p[i];
    				cnt++;
    			}
    			if(cnt>0) ans*=(cnt*2+1);
    		}
    		if(n>1) ans*=3;
    		cout<<"Case "<<nc++<<": "<<ans/2+1<<endl;
    	}
    	return 0;
    }
```
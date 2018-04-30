---
title: Codeforces-460B
date: 2018-04-22 22:28:41
tags: [algorithm,trick]
---
来源：CF460B

反过来枚举位数和，代码：

    
```cpp
    #include <iostream>
    #include <cstdio>
    #include <cstring>
    using namespace std;
    typedef long long LL;
    const LL INF=1e9;
    LL a,b,c;
    LL ans[100];
    LL pow_m(LL x,LL a){
    	LL ans=1;
    	for(int i=0;i<a;i++)
    		ans*=x;
    	return ans;
    }
    LL fun(LL x,LL a){
    	return b*pow_m(x,a)+c;
    }
    bool judge(LL x,LL i){
    	LL res=0;
    	while(x){
    		res+=x%10;
    		x/=10;
    	}
    	if(i==res) return 1;
    	else return 0;
    }
    int main()
    {
    	int cnt=0;
    	scanf("%lld%lld%lld",&a,&b,&c);
    	for(int i=1;i<=81;i++){
    		LL x=fun(i,a);
    		if(judge(x,i)&&x<INF) {
    			ans[cnt++] = x;
    		}
    	}
    	cout<<cnt<<endl;
    	if(cnt){
    		cout<<ans[0];
    		for(int i=1;i<cnt;i++)
    			cout<<" "<<ans[i];
    		cout<<endl;
    	}
    	return 0;
    }

```

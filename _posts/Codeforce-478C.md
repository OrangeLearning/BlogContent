---
title: Codeforce-478C
date: 2018-04-22 22:28:37
tags: [algorithm,greedy]
---
来源：CF478C

还是比较好理解的一个题目，就是一种搭配，注意其中的贪心策略

```cpp    
    #include <iostream>
    #include <cstdio>
    #include <cstring>
    #include <algorithm>
    #include <cmath>
    using namespace std;
    long long a[3];//
    int main(){
    	int r,g,b;
    	scanf("%lld%lld%lld",&a[0],&a[1],&a[2]);
    	sort(a,a+3);
    	if((a[0]+a[1])*2<a[2]){
    		cout<<a[0]+a[1]<<endl;
    	}
    	else{
    		cout<<(a[0]+a[1]+a[2])/3<<endl;
    	}
    	return 0;
    }

```
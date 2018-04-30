---
title: CodeForce-456A
date: 2018-04-22 22:28:39
tags: [algorithm,sort]
---
来源：CF456A

水题一道,不解释太多

代码：

```cpp
    #include <iostream>
    #include <cstdio>
    #include <cstring>
    #include <algorithm>
    using namespace std;
    const int MAXN = 100010;
    int n;
    struct Node
    {
    	int a,b;
    }p[MAXN];
    int cmp(Node x,Node y){
    	return x.a<y.a;
    }
    int main(){
    	scanf("%d",&n);
    	for(int i=0;i<n;i++){
    		scanf("%d%d",&p[i].a,&p[i].b);
    	}
    	sort(p,p+n,cmp);
    	int flag = 1;
    	for(int i=0;i<n-1;i++){
    		if(p[i].b>p[i+1].b) {
    			flag=0;
    			break;
    		}
    	}
    	if(flag) cout<<"Poor Alex"<<endl;
    	else cout<<"Happy Alex"<<endl;
    	return 0;
    }
```
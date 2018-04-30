---
title: CodeForces-651
date: 2018-04-22 22:25:20
tags: [algorithm,stl]
---

就是用set元素不重复的功能，很简单。
```cpp
    #include <iostream>
    #include <cstdio>
    #include <set>
    using namespace std;
    set<int>s;
    int main(){
    	int n,m;
    	scanf("%d%d",&n,&m);
    	int d;
    	for(int i=0;i<n;i++){
            scanf("%d",&d);
            while(d--)
            {
                int x;
                scanf("%d",&x);
                s.insert(x);
            }
    	}
    	if(s.size()==m)cout<<"YES"<<endl;
    	else cout<<"NO"<<endl;
    	return 0;
    }
```
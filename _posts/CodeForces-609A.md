---
title: CodeForces-609A
date: 2018-04-22 22:25:22
tags: [algorithm,sort,greedy]
---
简单

```cpp
    #include <iostream>
    #include <cstdio>
    #include <algorithm>
    using namespace std;
    const int MAXN=1010;
    int a[MAXN];
    int main(){
    	int n,m;
    	int i;
    	cin>>n;
    	cin>>m;
    	for(i=0;i<n;i++)
            cin>>a[i];
        sort(a,a+n);
        int ans=0;
        for(i=0;i<n;i++){
            m-=a[n-1-i];
            ans++;
            if(m<=0)break;
        }
        cout<<ans<<endl;
    	return 0;
    }
```
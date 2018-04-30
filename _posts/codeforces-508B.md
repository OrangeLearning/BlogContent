---
title: codeforces-508B
date: 2018-04-22 22:25:10
tags: [algorithm,trick]
---

来源：codeforces 508B

很像尺取法，但也不完全是。。。

题意就不说了，直接讲解法

```cpp    
    #include <iostream>
    #include <cstdio>
    #include <algorithm>
    using namespace std;
    const int MAXN=100010;
    pair<long long ,long long>p[MAXN];
    int main(){
    	long long n,d;
    	cin>>n>>d;
    	for(int i=0;i<n;i++){
            cin>>p[i].first>>p[i].second;
    	}
        long long ans=0,m=0;
        sort(p,p+n);
        int r,l;
        r=l=0;
        for(l=0;r<n;){
            if(p[r].first-p[l].first>=d){//这个好理解
                ans-=p[l].second;//说明不满足条件
                l++;//去掉前面的，注意，这个时候我们的状态并没有消失，我们的最大的情况记录在M里面
            }
            else{//满足条件
                ans+=p[r].second;加上一个，这个是可以的
                r++;//向后取
            }
            m=max(ans,m);//比较一次之后的大小，我们只要记录我们的最大就好了
            //cout<<"d"<<endl;
        }
        cout<<m<<endl;结果，这个歌也好理解
    	return 0;
    }
```
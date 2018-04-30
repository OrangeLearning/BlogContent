---
title: LightOJ-1008
date: 2018-04-22 22:29:05
tags: [algorithm,simple]
---

来源：lightOJ1008

水题，注意一个完全平方数的位置

```cpp
    #include <iostream>
    #include <cstdio>
    #include <cstring>
    #include <algorithm>
    #include <cmath>
    using namespace std;
    typedef long long LL;
    LL n;
    int main(){
        int T,nc = 1;
        scanf("%d",&T);
        while(T--){
            LL x,y;
            cin>>n;
            LL k1 = floor(sqrt(n));
            if(k1*k1 == n) k1--;
            LL k2 = k1+1;
            LL mid = (k1*k1+1+k2*k2)>>1;
            //cout<<k1<<" "<<k2<<" "<<mid<<endl;
            printf("Case %d: ",nc++);
            if(k2&1){
                if(n>mid){
                    cout<<k2*k2-n+1<<" "<<k2<<endl;
                }
                else if(n == mid){
                    cout<<k2<<" "<<k2<<endl;
                }
                else {
                    cout<<k2<<" "<<n-k1*k1<<endl;
                }
            }
            else{
                if(n>mid){
                    cout<<k2<<" "<<k2*k2+1-n<<endl;
                }
                else if(n == mid){
                    cout<<k2<<" "<<k2<<endl;
                }
                else {
                    cout<<n-k1*k1<<" "<<k2<<endl;
                }
            }
        }
    
        return 0;
    }
    
```

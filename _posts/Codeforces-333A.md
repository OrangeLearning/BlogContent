---
title: Codeforces-333A
date: 2018-04-22 22:28:49
tags: [algorithm,simple]
---
来源：CF333A

水题一道，注意输入

代码：

```cpp
    #include <iostream>
    #include <cstdio>
    #include <cstring>
    #include <algorithm>
    using namespace std;
    typedef unsigned long long LL;
    
    LL n;
    int main(){
        LL ans = 0;
        scanf("%lld",&n);
        while(n%3==0) n/=3;
        ans = n/3+1;
        printf("%lld\n",ans);
        return 0;
    }

```

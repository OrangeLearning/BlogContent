---
title: lightOJ1179
date: 2018-04-22 22:29:44
tags: [algorithm,Joseph]
---
来源：lightOJ1179

区域赛回来还是太弱啊。。。铜牌滚粗。。。

重头开始搞，先把知识点搞结束

    
```cpp
    #include <iostream>
    #include <cstdio>
    #include <cstring>
    #include <algorithm>
    using namespace std;
    
    int solve(int n,int k){
        int cnt = 1;
        int res = 0;
        while(cnt < n){
            res = (res + k) % (cnt + 1);
            cnt ++;
        }
        return res + 1;
    }
    int main(){
        int T,nc = 1;
        scanf("%d",&T);
        while(T--){
            int n,k;
            scanf("%d%d",&n,&k);
            printf("Case %d: %d\n",nc++,solve(n,k));
        }
    	return 0;
    }
    /**
    解释一下线性的约瑟夫环问题什么原理。
    我们现在是要求最后活下来的那个人，我们设编号为res
    对于还剩下N个人的情况，这一局死掉的是M，那么，下一局死掉的一定是
    (M + K) % (N - 1)
    这样的话，我们现在用现在就可以开始数，由于第一个人报数是1，所以我们
    假定第一个死掉的是0号，下面用我们之前的那个公式就行了。
    也有用链表模拟的，不过那个是比较麻烦的，而且必然会超时
    */
    
```
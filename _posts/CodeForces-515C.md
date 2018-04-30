---
title: CodeForces-515C
date: 2018-04-22 22:25:14
tags: [algorithm,simple]
---
来源：CodeForces 515C

这个题目关键是要知道关键不是转化阶乘，而是说每一位转化为其他位，从而，只要找到所有数字的转化之后的东西就行，用一个数组存下数据，排序输出就行。

代码：
```cpp
    #include <iostream>
    #include <cstdio>
    #include <cstring>
    #include <algorithm>
    using namespace std;
    char str[16];
    int ans[100];
    int main(){
    	int n;
    	scanf("%d",&n);
    	scanf("%s",str);
    	int i,cnt=0;
    	for(i=0;i<strlen(str);i++){
            int k=(int)(str[i]-'0');
            if(k==2||k==3||k==5||k==7) ans[cnt++]=k;//质数改不了
            else if(k==4){//4改为322
                ans[cnt++]=3;
                ans[cnt++]=2;
                ans[cnt++]=2;
            }
            else if(k==6){//6改为53
                ans[cnt++]=5;
                ans[cnt++]=3;
            }
            else if(k==8){//8改为7222
                ans[cnt++]=7;
                ans[cnt++]=2;
                ans[cnt++]=2;
                ans[cnt++]=2;
            }
            else if(k==9){
                ans[cnt++]=7;//9改为7332
                ans[cnt++]=3;
                ans[cnt++]=3;
                ans[cnt++]=2;
            }
            else ;//增强鲁棒性
    	}
    	sort(ans,ans+cnt);
        for(i=cnt-1;i>=0;i--)
            printf("%d",ans[i]);
        cout<<endl;
    	return 0;
    }
```
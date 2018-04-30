---
title: LightOJ-1214
date: 2018-04-22 22:29:46
tags: [algorithm,BigInteger]
---
来源：lightOJ1214

直接Java的大数

其实也可以一位一位算过去

    
```java
    import java.io.*;
    import java.util.*;
    import java.math.*;
    public class F{
        static public void main(String[] args){
            Scanner input = new Scanner(System.in);
            BigInteger a,b;
            int T,nc = 1;
            T = input.nextInt();
            for(nc = 1;nc <= T;++nc){
                a = input.nextBigInteger();
                b = input.nextBigInteger();
                a = a.abs();
                b = b.abs();
                if(a.mod(b) == BigInteger.ZERO) {
                    System.out.println("Case "+nc+": divisible");
                }
                else {
                    System.out.println("Case "+nc+": not divisible");
                }
            }
            input.close();
        }
    }
```

```cpp    
    #include <iostream>
    #include <cstdio>
    #include <cstring>
    #include <algorithm>
    using namespace std;
    const int MAXN = 300;
    char ch[MAXN];
    int main(){
        int T,nc = 1;
        scanf("%d",&T);
        getchar();
        while(T--){
            int flag,len;
            memset(ch,0,sizeof ch);
            long long k;
            scanf("%s %lld",ch,&k);
            k = (k > 0 ? k : -k);
            len = strlen(ch);
            flag = (ch[0] == '-' ? 1 : 0);
            long long ans = 0 ;
            for(int i=flag;i<len;i++){
                ans = (ans * 10 + (long long)(ch[i] - '0')) % k;
            }
            printf("Case %d: ",nc++);
            if(ans){
                puts("not divisible");
            }
            else {
                puts("divisible");
            }
        }
    	return 0;
    }
```
---
title: LightOJ-1331
date: 2018-04-22 22:31:35
tags: [algorithm,math]
---
来源：lightOJ 1331

水题

    
```cpp
    #include <iostream>
    #include <cstdio>
    #include <cstring>
    #include <algorithm>
    #include <cmath>
    using namespace std;
    inline double area(double r,double deg){
        return r * r * deg / 2;
    }
    int main(){
        double r1,r2,r3;
        double a,b,c;
        int T,nc = 1;
    //    cout<<acos(-1.0)<<endl;
        scanf("%d",&T);
        while(T--){
            scanf("%lf%lf%lf",&r1,&r2,&r3);
            a = r1 + r2;
            b = r2 + r3;
            c = r1 + r3;
    //        cout<<"a = "<<a<<" b = "<<b<<" c = "<<c<<endl;
            double dega,degb,degc;
            degc = acos((a*a+b*b-c*c)/(2*a*b));
            dega = acos((b*b+c*c-a*a)/(2*b*c));
            degb = acos((a*a+c*c-b*b)/(2*a*c));
    //        cout<<dega<<" "<<degb<<" "<<degc<<" pi / 3 = "<<acos(-1.0)/3<<endl;
            double ans = a * b * sin(degc) / 2.0;
    //        cout<<sqrt(3) / 4.0 * a * a <<endl;
    //        cout<<area(r3,dega)<<endl;
            ans = ans - (area(r3,dega) + area(r1,degb) + area(r2,degc));
            printf("Case %d: %.10lf\n",nc++,ans);
    //        cout<<sqrt(3) / 4.0 * a * a<<endl;
        }
    
        return 0;
    }
```
---
title: CodeForce-257B
date: 2018-04-22 22:25:47
tags: [algorithm,Matrix]
---

来源：CF257B

省赛结束，今天继续训练。

做了一道矩阵快速幂，并且相同了具体特征根方程到底是怎么回事了。。。想想高中真是菜啊。

直接上代码吧，群巨会懂的。。。

代码：

```cpp
    #include <iostream>
    #include <cstdio>
    #include <string>
    #include <cstring>
    #include <algorithm>
    #include <cmath>
    #include <vector>
    using namespace std;
    ///上周才看的。。。以为省赛有这个东西的，结果没有。。。笑crying
    /********************
    就是这个两个数乘以一个
     --         --
    |   1    -1   |
    |             |
    |   1     0   |矩阵。
     --         --
    然后用矩阵快速幂就好
    ********************/
    const long long MOD=1e9+7;
    typedef long long LL;
    typedef vector<LL> VLL;
    typedef vector<VLL> Matrix;
    Matrix m(2,VLL(2));
    Matrix mul(Matrix a,Matrix b){
        Matrix c(2,VLL(2));
        for(int i=0;i<2;i++)
        {
            for(int k=0;k<2;k++)
            {
                for(int j=0;j<2;j++)
                    c[i][j]=(c[i][j]+a[i][k]*b[k][j]);
            }
        }
        return c;
    }
    Matrix M_qmi(int n){
        Matrix b(2,VLL(2));
        b[0][0]=1;
        b[1][1]=1;//E-juzhen
        while(n>0)
        {
            if(n&1) b=mul(b,m);
            m=mul(m,m);
            n>>=1;
        }
        return b;
    }
    int main(){
    	int x,y;
    	int n;
    	scanf("%d%d",&x,&y);
    	scanf("%d",&n);
    	LL sum;
    	if(n==1){
            sum=x;
    	}
    	else if(n==2){
            sum=y;
    	}
    	else{
            m[0][0]=1;m[0][1]=-1;
            m[1][0]=1;m[1][1]=0;
            Matrix ans=M_qmi(n-2);
            /*cout<<ans[0][0]<<" "<<ans[0][1]<<endl;
            cout<<ans[1][0]<<" "<<ans[1][1]<<endl;*/
            sum=(ans[0][0]*y+ans[0][1]*x)%MOD;
    	}
        while(sum<0)sum+=MOD;
        cout<<sum<<endl;
    	return 0;
    }
```
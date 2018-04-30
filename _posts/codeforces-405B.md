---
title: codeforces-405B
date: 2018-04-22 22:25:02
tags: [algorithm,simple]
---
来源：  codeforces  405B

这个题目一开始没有想到有O（n）的解法，有点撒。。。

是这样，我们从后向前看，当然也有向后，先如果我们遇到.，那么用一个数记下来+1，如果我们遇到L，则说明，前面的都是站立的，但是我们遇到一个R，那么需要找前面
是否有过一个L，有的话就可以站立t%2，最后部分，如果前面有一个L，则是全部倒掉的。。。

代码：

```cpp    
    #include <iostream>
    #include <cstdio>
    
    using namespace std;
    const int MAXN=3000+10;
    char ch[MAXN];
    int main(){
    	int n;
    	cin>>n;
    	for(int i=0;i<n;i++){
            cin>>ch[i];
    	}
    	int ans=0;
    	int d=0;
    	char x;
    	for(int i=n-1;i>=0;i--){
            if(ch[i]=='.')d++;
            else if(ch[i]=='L'){
                ans+=d;
                d=0;
                x=ch[i];
            }
            else {
                if(x=='L')
                    ans+=(d%2);
                d=0;
                x='R';
            }
    	}
    	if(x!='L')
            ans+=d;
    	cout<<ans<<endl;
    	return 0;
    }
```
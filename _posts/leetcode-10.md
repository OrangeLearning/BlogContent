---
title: leetcode-10
date: 2018-04-18 20:36:34
tags: [leetcode, algorithm]
---

# leetcode-10 题解

题目意思很简单，正则表达式匹配一个字符串，注意这个*表示前面这个字符串的闭包
思想很好理解，就是如果有* 就从所有可能位置向下递归即可，有下面几个注意点：

1. 注意到要判断模式串结束的时候文本串是否结束，原因是a*可以表示空串
2. 注意到通过判断第二个字符串是否为*来判断是直接向下

代码：
```cpp
class Solution {
public:
    bool isAccept(string s,string p,int ss,int pp){
        if(pp >= p.length() ) return ss == s.length();
        if(p[pp+1] == '*'){
            while(ss < s.length() && (s[ss] == p[pp] || p[pp] == '.')) {
                if(isAccept(s,p,ss,pp+2)) return true;
                ss ++;
            }
            return isAccept(s,p,ss,pp+2);
        }
        else {
            if(p[pp] == '.') return isAccept(s,p,ss+1,pp+1);
            else {
                if(s[ss] != p[pp]) return false;
                else return isAccept(s,p,ss+1,pp+1);
            }
        }
    }
    
    bool isMatch(string s, string p) {
        return isAccept(s,p,0,0);
    }
};
```
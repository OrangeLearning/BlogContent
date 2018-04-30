---
title: quine
date: 2018-04-21 23:51:28
tags: [program]
---
一个有趣的问题：可以输出自己的源程序代码（quine）
UOJ#8

就是看了玩玩的，因为上面的本弱基本都不是很会

还是很有很有趣的问题，要求输出一段代码，这段代码的功能是打印这段代码：

    
```cpp
#include <stdio.h>

char*s="#include <stdio.h>%cchar*s=%c%s%c;%cmain(){printf(s,10,34,s,34,10,10);}%c";

main(){printf(s,10,34,s,34,10,10);}
```
这就是一个例子。。。

注意，这个代码G++会warning，但是还是可以运行的。
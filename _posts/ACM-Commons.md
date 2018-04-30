---
title: ACM-Commons
date: 2018-04-22 22:24:56
tags: [algorithm]
---
#  [ ACM常识小知识 ](https://blog.csdn.net/kissacm/article/details/50807757)

##  1\. 数据表示范围

unsignedint 0～4294967295

int2147483648～2147483647

unsigned long 0～4294967295

long2147483648～2147483647

long long的最大值：9223372036854775807

long long的最小值：-9223372036854775808

unsigned long long的最大值：18446744073709551615

__int64的最大值：9223372036854775807

__int64的最小值：-9223372036854775808

unsigned __int64的最大值：18446744073709551615

##  2\. 1~10^n之间素数个数(1<=n<=9)

n

1

2

3

4

5

6

7

8

9

10^n

4

25

168

1229

9592

78498

664579

5761455

  

50847543

  

##  3\. 无穷大

对于int类型的数据，如果我们想用一个数来表示无穷大，使得它比输入的所有的数都大，可以选择0x3f3f3f3f 或 0x7fffffff

0x3f3f3f3f 数值为 1061109567

0x7fffffff数值为2139062143

负无穷大则可以用 -0x3f3f3f3f 或 -0x7fffffff

-0x3f3f3f3f数值为-1061109567 

-0x7fffffff数值为-2139062143 

在题目中常使用 0x3f3f3f3f，因为0x7fffffff 容易越界，定义全局变量

const int inf = 0x3f3f3f3f;

##  4\. memset()初始化

假设定义了以下数组：

int a[10];

double b[10];

bool ok[10];

memset(a, -1, sizeof(a)); //正确，将int型a数组元素初始化为 -1

memset(b, -1, sizeof(b)); //错误，不可以将double型的b数组初始化为 -1

memset(ok, -1, sizeof(ok));//错误，不可以将bool型的ok数组初始化为-1

memset(a, 0, sizeof(a)); //正确，将int型a数组元素初始化为0

memset(b, 0, sizeof(b)); //正确，将double型b数组初始化为 0

memset(ok, 0, sizeof(ok)); //正确，将bool型的ok数组初始化为0

memset(a, 1, sizeof(a)); //错误，不可以将int型a数组元素初始化为0

memset(b, 1, sizeof(b)); //错误，不可以将double型b数组初始化为 0

memset(ok,1, sizeof(ok)); //正确，可以将bool型的ok数组初始化为0

对于无穷大的初始化：

const int inf = 0x3f3f3f3f;

const int INF = 0x7fffffff;

memset(a, inf, sizeof(a)); //正确

memset(a, INF, sieof(a)); //错误

对于int型数组a可以用0x3f3f3f3f初始化，但不可以用0x7fffffff，如果非要把a数组初始化为0x7ffffff，可以用语句 fill(a,
a+n, INF); //n为元素个数

##  5\. π的表示

方法1：const double PI = 3.1415926535898;

方法2：#define PI acos(-1)

建议使用方法2

##  6\. 随机数

srand(time(0)); //根据 [ 系统 ](http://www.2cto.com/os/) 时间设置随机数种子

int i = rand() % N; //生成区间[0,N)的整数

##  7\. 浮点数比较

f(fabs(tp1-tp2)<=1e-11)

cout<<"="<<endl;< p="">

else if(tp1>tp2)

cout<<">"<<endl;< p="">

else

cout<<"<"<<endl;< p="">

##  8\. 输入输出

###  ①int, double型

int a;

double b;

输入：

cin>>a; 或 scanf("%d",&a);

cin>>b; 或 scanf("%lf",&b);

输出：

cout<<a;

cout<<b;

###  ②char型

char ch;

输入： cin>>ch; 或scanf("%c",&ch);

scanf("%c",&ch); 不常用，容易出错，比如下面的例子：

cin>>ch;

cout<<ch<<endl;

scanf("%c",&ch);

cout<<ch;

上面四句话，运行结果第二个cout输出的不是我们原来输入的字符，因为如果第一次输入字符后，按了回车，那么第二次输入的就是回车，也就是scanf("%c",&
ch);把回车吸收了。所以如果要正确使用，要在中间加上一句getchar();

cin>>ch;

cout<<ch<<endl;< p="">

getchar();

scanf("%c",&ch);

cout<<ch;

对于字符数组 char chs[10];

输入： cin>>chs; 或scanf("%s",chs);

注意：用字符数组存放字符串时，如果一个字符串中存在空格，cin>>chs;不可以存空格

gets(chs);可以存空格.

###  ③string型

string str;

输入：cin>>str; 或getline(cin,str);

前者不可以存放带有空格的字符串，后者可以。

###  ④混合技巧型

011

101

110

输入如上，每一行的三个数是连续的，要想分开存入矩阵中，读入用scanf(“%1d”, &num);

12:08:30

输入如上，假设这是一个时间，那么我们想要在输入的时候就单独获取时分秒，可以用

scanf("%d:%d:%d",&h,&m,&s);

###  ⑤快速读入（正负）

即输入字符转换成数字，效率高，在输入数据量特别大的时候采用快速读入可以避免超时.

inline int read()

{

char ch=getchar();int x=0,f=1;

while(ch>'9'||ch<'0'){if(ch=='-')f=-1;ch=getchar();}

while(ch<='9'&&ch>='0'){x=x*10+ch-'0';ch=getchar();}

return x*f;

}

使用：

int num;

num = read(); //输入num

  
  

  


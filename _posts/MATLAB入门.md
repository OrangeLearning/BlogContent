---
title: MATLAB入门
date: 2018-04-22 22:25:42
tags: [Matlab]
---
#  [ MATLAB入门教程 ](https://blog.csdn.net/kissacm/article/details/51226417)

** MATLAB  入门教程  **

** **

** 1  ．  MATLAB  的基本知识  **

** 1-1、基本运算与函数 **

在MATLAB下进行基本数学运算，只需将运算式直接打入提示号（>>）之後，并按入 ** Enter  ** 键即可。例如：

>> (5*2+1.3-0.8)*10/25

ans =4.2000

MATLAB会将运算结果直接存入一变数ans，代表MATLAB运算後的答案（Answer）并显示其数值於萤幕上。

小提示：
">>"是MATLAB的提示符号（Prompt），但在PC中文视窗系统下，由於编码方式不同，此提示符号常会消失不见，但这并不会影响到MATLAB的运算结果。

我们也可将上述运算式的结果设定给另一个变数x：

x = (5*2+1.3-0.8)*10^2/25

x = 42

此时MATLAB会直接显示x的值。由上例可知，MATLAB认识所有一般常用到的加（+）、减（-）、乘（*）、除（/）的数学运算符号，以及幂次运算（^）。

小提示： MATLAB将所有变数均存成double的形式，所以不需经过变数宣告（Variabledeclaration）。MATLAB同时也会自动进行记忆体
的使用和回收，而不必像C语言,必须由使用者一一指定.这些功能使的MATLAB易学易用，使用者可专心致力於撰写程式，而不必被软体枝节问题所干扰。

若不想让MATLAB每次都显示运算结果，只需在运算式最後加上分号（；）即可，如下例：

y = sin(10)*exp(-0.3*4^2);

若要显示变数y的值，直接键入y即可：

>>y

y =-0.0045

在上例中，sin是正弦函数，exp是指数函数，这些都是MATLAB常用到的数学函数。

下表即为MATLAB常用的基本数学函数及三角函数：

小整理：MATLAB常用的基本数学函数

abs(x)：纯量的绝对值或向量的长度

angle(z)：复 数z的相角(Phase angle)

sqrt(x)：开平方

real(z)：复数z的实部

imag(z)：复数z的虚 部

conj(z)：复数z的共轭复数

round(x)：四舍五入至最近整数

fix(x)：无论正负，舍去小数至最近整数

floor(x)：地板函数，即舍去正小数至最近整数

ceil(x)：天花板函数，即加入正小数至最近整数

rat(x)：将实数x化为分数表示

rats(x)：将实数x化为多项分数展开

sign(x)：符号函数 (Signum function)。

当x<0时，sign(x)=-1；

当x=0时，sign(x)=0;

当x>0时，sign(x)=1。

> 小整理：MATLAB常用的三角函数

sin(x)：正弦函数

cos(x)：馀弦函数

tan(x)：正切函数

asin(x)：反正弦函数

acos(x)：反馀弦函数

atan(x)：反正切函数

atan2(x,y)：四象限的反正切函数

sinh(x)：超越正弦函数

cosh(x)：超越馀弦函数

tanh(x)：超越正切函数

asinh(x)：反超越正弦函数

acosh(x)：反超越馀弦函数

atanh(x)：反超越正切函数

变数也可用来存放向量或矩阵，并进行各种运算，如下例的列向量（Row vector）运算：

x = [1 3 5 2];

y = 2*x+1

y = 3 7 11 5

小提示：变数命名的规则

1.第一个字母必须是英文字母 2.字母间不可留空格 3.最多只能有19个字母，MATLAB会忽略多馀字母

我们可以随意更改、增加或删除向量的元素：

y(3) = 2 % 更改第三个元素

y =3 7 2 5

y(6) = 10 % 加入第六个元素

y = 3 7 2 5 0 10

y(4) = [] % 删除第四个元素，

y = 3 7 2 0 10

在上例中，MATLAB会忽略所有在百分比符号（%）之後的文字，因此百分比之後的文字均可视为程式的注解（Comments）。MATLAB亦可取出向量的一个元素
或一部份来做运算：

x(2)*3+y(4) % 取出x的第二个元素和y的第四个元素来做运算

ans = 9

y(2:4)-1 % 取出y的第二至第四个元素来做运算

ans = 6 1 -1

在上例中，2:4代表一个由2、3、4组成的向量

若对MATLAB函数用法有疑问，可随时使用help来寻求线上支援（on-line help）：helplinspace

小整理：MATLAB的查询命令

help：用来查询已知命令的用法。例如已知inv是用来计算反矩阵，键入help inv即可得知有关inv命令的用法。（键入help
help则显示help的用法，请试看看！） lookfor：用来寻找未知的命令。例如要寻找计算反矩阵的命令，可键入 lookfor
inverse，MATLAB即会列出所有和关键字inverse相关的指令。找到所需的命令後
，即可用help进一步找出其用法。（lookfor事实上是对所有在搜寻路径下的M档案进行关键字对第一注解行的比对，详见後叙。）

将行向量转置（Transpose）後，即可得到列向量（Column vector）：

z = x'

z = 4.0000

5.2000

6.4000

7.6000

8.8000

10.0000

不论是行向量或列向量，我们均可用相同的函数找出其元素个数、最大值、最小值等：

length(z) % z的元素个数

ans = 6

max(z) % z的最大值

ans = 10

min(z) % z的最小值

ans =   4

小整理：适用於向量的常用函数有：

min(x): 向量x的元素的最小值

max(x): 向量x的元素的最大值

mean(x): 向量x的元素的平均值

median(x): 向量x的元素的中位数

std(x): 向量x的元素的标准差

diff(x): 向量x的相邻元素的差

sort(x): 对向量x的元素进行排序（Sorting）

length(x): 向量x的元素个数

norm(x): 向量x的欧氏（Euclidean）长度

sum(x): 向量x的元素总和

prod(x): 向量x的元素总乘积

cumsum(x): 向量x的累计元素总和

cumprod(x): 向量x的累计元素总乘积

dot(x, y): 向量x和y的内 积

cross(x, y): 向量x和y的外积 （大部份的向量函数也可适用於矩阵，详见下述。）

若要输入矩阵，则必须在每一列结尾加上分号（；），如下例：

A = [1 2 3 4; 5 6 7 8; 9 1011 12];

A =

1  2  3 4

5  6  7 8

9  10 11  12

同样地，我们可以对矩阵进行各种处理：

A(2,3) = 5 % 改变位於第二列，第三行的元素值

A =

1  2  3 4

5  6  5 8

9  10 11  12

B = A(2,1:3) % 取出部份矩阵B

B = 5 6 5

A = [A B'] % 将B转置後以列向量并入A

A =

1  2  3  4  5

5  6  5  8  6

9  10 11  12 5

A(:, 2) = [] % 删除第二行（：代表所有列）

A =

1  3  4 5

5  5  8 6

9  11 12  5

A = [A; 4 3 2 1] % 加入第四列

A =

1  3   4  5

5  5   8  6

9  11  12 5

4  3   2  1

A([1 4], :) = [] % 删除第一和第四列（：代表所有行）

A =

5  5   8  6

9  11  12 5

这几种矩阵处理的方式可以相互叠代运用，产生各种意想不到的效果，就看各位的巧思和创意。

小提示：在MATLAB的内部资料结构中,每一个矩阵都是一个以行为主（Column-oriented ）的阵列（Array）因此对於矩阵元素的存取，我们可用一
维或二维的索引（Index）来定址。举例来说，在上述矩阵A中，位於第二列、第三行的元素可写为A(2,3)
（二维索引）或A(6)（一维索引，即将所有直行进行堆叠後的第六个元素）。

此外，若要重新安排矩阵的形状，可用reshape命令：

B = reshape(A, 4, 2) % 4是新矩阵的行数，2是新矩阵的列数

B =

5   8

9   12

5   6

11  5

小提示： A(:)就是将矩阵A每一行堆叠起来，成为一个列向量，而这也是MATLAB变数的内部储存方式。以前例而言，reshape(A, 8,
1)和A(:)同样都会产生一个8x1的矩阵。

MATLAB可在同时执行数个命令，只要以逗号或分号将命令隔开：

x = sin(pi/3); y = x^2; z = y*10,

z =

7.5000

若一个数学运算是太长，可用三个句点将其延伸到下一行：

z = 10*sin(pi/3)* ...

sin(pi/3);

若要检视现存於工作空间（Workspace）的变数，可键入who：

who

Your variables are:

testfile x

这些是由使用者定义的变数。若要知道这些变数的详细资料，可键入：

whos

Name Size Bytes Class

A 2x4 64 double array

B 4x2 64 double array

ans 1x1 8 double array

x 1x1 8 double array

y 1x1 8 double array

z 1x1 8 double array

Grand total is 20 elements using 160 bytes

使用clear可以删除工作空间的变数：

clear A

A

??? Undefined function or variable 'A'.

另外MATLAB有些永久常数（Permanent constants），虽然在工作空间中看不 到，但使用者可直接取用，例如：

pi

ans = 3.1416

下表即为MATLAB常用到的永久常数。

小整理：MATLAB的永久常数 i或j：基本虚数单位

eps：系统的浮点（Floating-point）精确度

inf：无限大， 例如1/0 nan或NaN：非数值（Not a number） ，例如0/0

pi：圆周率 p（= 3.1415926...）

realmax：系统所能表示的最大数值

realmin：系统所能表示的最小数值

nargin: 函数的输入引数个数

nargin: 函数的输出引数个数

** 1-2、重复命令 **

最简单的重复命令是for圈（for-loop），其基本形式为：

for 变数 = 矩阵；

运算式；

end

其中变数的值会被依次设定为矩阵的每一行，来执行介於for和end之间的运算式。因此,若无意外情况，运算式执行的次数会等於矩阵的行数。

举例来说，下列命令会产生一个长度为6的调和数列（Harmonic sequence）：

x = zeros(1,6); % x是一个16的零矩阵

for i = 1:6,

x(i) = 1/i;

end

在上例中，矩阵x最初是一个16的零矩阵，在for圈中，变数i的值依次是1到6，因此矩阵x的第i个元素的值依次被设为1/i。我们可用分数来显示此数列：

format rat % 使用分数来表示数值

disp(x)

1 1/2 1/3 1/4 1/5 1/6

for圈可以是多层的，下例产生一个16的Hilbert矩阵h，其中为於第i列、第j行的元素为

h = zeros(6);

for i = 1:6,

for j = 1:6,

h(i,j) = 1/(i+j-1);

end

end

disp(h)

1 1/2 1/3 1/4 1/5 1/6

1/2 1/3 1/4 1/5 1/6 1/7

1/3 1/4 1/5 1/6 1/7 1/8

1/4 1/5 1/6 1/7 1/8 1/9

1/5 1/6 1/7 1/8 1/9 1/10

1/6 1/7 1/8 1/9 1/10 1/11

小提示：预先配置矩阵 在上面的例子，我们使用zeros来预先配置（Allocate）了一个适当大小的矩阵。若不预先配置矩阵，程式仍可执行，但此时MATLAB
需要动态地增加（或减小）矩阵的大小，因而降低程式的执行效率。所以在使用一个矩阵时，若能在事前知道其大小，则最好先使用zeros或ones等命令来预先配置所需
的记忆体（即矩阵）大小。

在下例中，for圈列出先前产生的Hilbert矩阵的每一行的平方和：

for i = h,

disp(norm(i)^2); % 印出每一行的平方和

end

1299/871

282/551

650/2343

524/2933

559/4431

831/8801

在上例中，每一次i的值就是矩阵h的一行，所以写出来的命令特别简洁。

令一个常用到的重复命令是while圈，其基本形式为：

while 条件式；

运算式；

end

也就是说，只要条件示成立，运算式就会一再被执行。例如先前产生调和数列的例子，我们可用while圈改写如下：

x = zeros(1,6); % x是一个16的零矩阵

i = 1;

while i <= 6,

x(i) = 1/i;

i = i+1;

end

format short

** 1-3、逻辑命令 **

最简单的逻辑命令是if, ..., end，其基本形式为：

if 条件式；

运算式；

end

if rand(1,1) > 0.5,

disp('Given random number is greater than 0.5.');

end

Given random number is greater than 0.5.

** 1-4、集合多个命令於一个M档案 **

若要一次执行大量的MATLAB命令，可将这些命令存放於一个副档名为m的档案，并在 MATLAB提示号下键入此档案的主档名即可。此种包含MATLAB命令的档案
都以m为副档名，因此通称M档案（M-files）。例如一个名为test.m的M档案，包含一连串的MATLAB命令，那麽只要直接键入test，即可执行其所包含
的命令：

pwd % 显示现在的目录

ans =

D:\MATLAB5\bin

cd c:\data\mlbook % 进入test.m所在的目录

type test.m % 显示test.m的内容

% This is my first test M-file.

% Roger Jang, March 3, 1997

fprintf('Start of test.m!\n');

for i = 1:3,

fprintf('i = %d ---> i^3 = %d\n', i, i^3);

end

fprintf('End of test.m!\n');

test % 执行test.m

Start of test.m!

i = 1 ---> i^3 = 1

i = 2 ---> i^3 = 8

i = 3 ---> i^3 = 27

End of test.m!

小提示：第一注解行（H1 help line） test.m的前两行是注解，可以使程式易於了解与管理。特别要说明的是，第一注解行通常用来简短说明此M档案的功
能，以便lookfor能以关键字比对的方式来找出此M档案。举例来说，test.m的第一注解行包含test这个字，因此如果键入lookfor
test，MATLAB即可列出所有在第一注解行包含test的M档案，因而test.m也会被列名在内。

严格来说，M档案可再细分为命令集（Scripts）及函数（Functions）。前述的test.m即为命令集，其效用和将命令逐一输入完全一样，因此若在命令集
可以直接使用工作空间的变数，而且在命令集中设定的变数，也都在工作空间中看得到。函数则需要用到输入引数（Input
arguments）和输出引数（Output
arguments）来传递资讯，这就像是C语言的函数,或是FORTRAN语言的副程序（Subroutines）。举例来说，若要计算一个正整数的阶乘
（Factorial），我们可以写一个如下的MATLAB函数并将之存档於fact.m：

function output = fact(n)

% FACT Calculate factorial of a given positive integer.

output = 1;

for i = 1:n,

output = output*i;

end

其中fact是函数名，n是输入引数，output是输出引数，而i则是此函数用到的暂时变数。要使用此函数，直接键入函数名及适当输入引数值即可：

y = fact(5)

y = 120

（当然，在执行fact之前，你必须先进入fact.m所在的目录。）在执行fact(5)时，

MATLAB会跳入一个下层的暂时工作空间（Temperary workspace），将变数n的值设定为5，然後进行各项函数的内部运算，所有内部运算所产生的变
数（包含输入引数n、暂时变数i，以及输出引数output）都存在此暂时工作空间中。运算完毕後，MATLAB会将最後输出引数output的值设定给上层的变数y
，并将清除此暂时工作空间及其所含的所有变数。换句话说，在呼叫函数时，你只能经由输入引数来控制函数的输入，经由输出引数来得到函数的输出，但所有的暂时变数都会随
着函数的结束而消失，你并无法得到它们的值。

小提示：有关阶乘函数 前面（及後面）用到的阶乘函数只是纯粹用来说明MATLAB的函数观念。若实际要计算一个正整数n的阶乘（即n!）时，可直接写成prod(1
:n)，或是直接呼叫gamma函数：gamma(n-1)。

MATLAB的函数也可以是递式的（Recursive），也就是说，一个函数可以呼叫它本身。

举例来说，n! = n*(n-1)!，因此前面的阶乘函数可以改成递式的写法：

function output = fact(n)

% FACT Calculate factorial of a given positive integerrecursively.

if n == 1, % Terminating condition

output = 1;

return;

end

output = n*fact(n-1);

在写一个递函数时，一定要包含结束条件（Terminating condition），否则此函数将会一再呼叫自己，永远不会停止，直到电脑的记忆体被耗尽为止。以
上例而言，n==1即满足结束条件，此时我们直接将output设为1，而不再呼叫此函数本身。

** 1-5、搜寻路径 **

在前一节中，test.m所在的目录是d:\mlbook。如果不先进入这个目录，MATLAB就找不到你要执行的M档案。如果希望MATLAB不论在何处都能执行t
est.m，那麽就必须将d:\mlbook加入MATLAB的搜寻路径（Search path）上。要检视MATLAB的搜寻路径，键入path即可：

path

MATLABPATH

d:\matlab5\toolbox\matlab\general

d:\matlab5\toolbox\matlab\ops

d:\matlab5\toolbox\matlab\lang

d:\matlab5\toolbox\matlab\elmat

d:\matlab5\toolbox\matlab\elfun

d:\matlab5\toolbox\matlab\specfun

d:\matlab5\toolbox\matlab\matfun

d:\matlab5\toolbox\matlab\datafun

d:\matlab5\toolbox\matlab\polyfun

d:\matlab5\toolbox\matlab\funfun

d:\matlab5\toolbox\matlab\sparfun

d:\matlab5\toolbox\matlab\graph2d

d:\matlab5\toolbox\matlab\graph3d

d:\matlab5\toolbox\matlab\specgraph

d:\matlab5\toolbox\matlab\graphics

d:\matlab5\toolbox\matlab\uitools

d:\matlab5\toolbox\matlab\strfun

d:\matlab5\toolbox\matlab\iofun

d:\matlab5\toolbox\matlab\timefun

d:\matlab5\toolbox\matlab\datatypes

d:\matlab5\toolbox\matlab\dde

d:\matlab5\toolbox\matlab\demos

d:\matlab5\toolbox\tour

d:\matlab5\toolbox\simulink\simulink

d:\matlab5\toolbox\simulink\blocks

d:\matlab5\toolbox\simulink\simdemos

d:\matlab5\toolbox\simulink\dee

d:\matlab5\toolbox\local

此搜寻路径会依已安装的工具箱（Toolboxes）不同而有所不同。要查询某一命令是在搜寻路径的何处，可用which命令：

which expo

d:\matlab5\toolbox\matlab\demos\expo.m

很显然c:\data\mlbook并不在MATLAB的搜寻路径中，因此MATLAB找不到test.m这个M档案：

which test

c:\data\mlbook\test.m

要将d:\mlbook加入MATLAB的搜寻路径，还是使用path命令：

path(path, 'c:\data\mlbook');

此时d:\mlbook已加入MATLAB搜寻路径（键入path试看看），因此MATLAB已经"看"得到

test.m:

which test

c:\data\mlbook\test.m

现在我们就可以直接键入test，而不必先进入test.m所在的目录。

小提示：如何在其启动MATLAB时，自动设定所需的搜寻路径？
如果在每一次启动MATLAB後都要设定所需的搜寻路径，将是一件很麻烦的事。有两种方法，可以使MATLAB启动後 ，即可载入使用者定义的搜寻路径：

1.MATLAB的预设搜寻路径是定义在matlabrc.m（在c:\matlab之下，或是其他安装MATLAB
的主目录下），MATLAB每次启动後，即自动执行此档案。因此你可以直接修改matlabrc.m ，以加入新的目录於搜寻路径之中。

2.MATLAB在执行matlabrc.m时，同时也会在预设搜寻路径中寻找startup.m，若此档案存在，则执行其所含的命令。因此我们可将所有在MATLA
B启动时必须执行的命令（包含更改搜寻路径的命令），放在此档案中。

每次MATLAB遇到一个命令（例如test）时，其处置程序为：

1.将test视为使用者定义的变数。

2.若test不是使用者定义的变数，将其视为永久常数 。

3.若test不是永久常数，检查其是否为目前工作目录下的M档案。

4.若不是，则由搜寻路径寻找是否有test.m的档案。

5.若在搜寻路径中找不到，则MATLAB会发出哔哔声并印出错误讯息。

以下介绍与MATLAB搜寻路径相关的各项命令。

** 1-6、资料的储存与载入 **

有些计算旷日废时，那麽我们通常希望能将计算所得的储存在档案中，以便将来可进行其他处理。MATLAB储存变数的基本命令是save，在不加任何选项（Option
s）时，save会将变数以二进制（Binary）的方式储存至副档名为mat的档案，如下述：

save：将工作空间的所有变数储存到名为matlab.mat的二进制档案。

save filename：将工作空间的所有变数储存到名为filename.mat的二进制档案。 save filename x y z
：将变数x、y、z储存到名为filename.mat的二进制档案。

以下为使用save命令的一个简例：

who % 列出工作空间的变数

Your variables are:

B h j y

ans i x z

save test B y % 将变数B与y储存至test.mat

dir % 列出现在目录中的档案

. 2plotxy.doc fact.m simulink.doc test.m ~$1basic.doc

.. 3plotxyz.doc first.doc temp.doc test.mat

1basic.doc book.dot go.m template.doc testfile.dat

delete test.mat % 删除test.mat

以二进制的方式储存变数，通常档案会比较小，而且在载入时速度较快，但是就无法用普通的文书软体（例如pe2或记事本）看到档案内容。若想看到档案内容，则必须加上-
ascii选项，详见下述：

save filename x -ascii：将变数x以八位数存到名为filename的ASCII档案。

Save filename x -ascii -double：将变数x以十六位数存到名为filename的ASCII档案。

另一个选项是-tab，可将同一列相邻的数目以定位键（Tab）隔开。

小提示：二进制和ASCII档案的比较 在save命令使用-ascii选项後，会有下列现象:save命令就不会在档案名称後加上mat的副档名。

因此以副档名mat结尾的档案通常是MATLAB的二进位资料档。

若非有特殊需要，我们应该尽量以二进制方式储存资料。

load命令可将档案载入以取得储存之变数：

load filename：load会寻找名称为filename.mat的档案，并以二进制格式载入。若找不到filename.mat，则寻找名称为filen
ame的档案，并以ASCII格式载入。load filename-ascii：load会寻找名称为filename的档案，并以ASCII格式载入。

若以ASCII格式载入，则变数名称即为档案名称（但不包含副档名）。若以二进制载入，则可保留原有的变数名称，如下例：

clear all; % 清除工作空间中的变数

x = 1:10;

save testfile.dat x -ascii % 将x以ASCII格式存至名为testfile.dat的档案

load testfile.dat % 载入testfile.dat

who % 列出工作空间中的变数

Your variables are:

testfile x

注意在上述过程中，由於是以ASCII格式储存与载入，所以产生了一个与档案名称相同的变数testfile，此变数的值和原变数x完全相同。

** 1-7、结束MATLAB **

有三种方法可以结束MATLAB：

1.键入exit

2.键入quit

3.直接关闭MATLAB的命令视窗（Command window）

** 2  ．数值分析  **

** 2．1微分 **

diff函数用以演算一函数的微分项，相关的函数语法有下列4个：

diff(f) 传回f对预设独立变数的一次微分值

diff(f,'t') 传回f对独立变数t的一次微分值

diff(f,n) 传回f对预设独立变数的n次微分值

diff(f,'t',n) 传回f对独立变数t的n次微分值

数值微分函数也是用diff，因此这个函数是靠输入的引数决定是以数值或是符号微分，如果引数为向量则执行数值微分，如果引数为符号表示式则执行符号微分。

先定义下列三个方程式，接著再演算其微分项：

>>S1 = '6*x^3-4*x^2+b*x-5';

>>S2 = 'sin(a)';

>>S3 = '(1 - t^3)/(1 + t^4)';

>>diff(S1)

ans=18*x^2-8*x+b

>>diff(S1,2)

ans= 36*x-8

>>diff(S1,'b')

ans= x

>>diff(S2)

ans=

cos(a)

>>diff(S3)

ans=-3*t^2/(1+t^4)-4*(1-t^3)/(1+t^4)^2*t^3

>>simplify(diff(S3))

ans= t^2*(-3+t^4-4*t)/(1+t^4)^2

** 2．2积分 **

int函数用以演算一函数的积分项， 这个函数要找出一符号式 F 使得diff(F)=f。如果积

分式的解析式(analytical form, closed form) 不存在的话或是MATLAB无法找到，则int
传回原输入的符号式。相关的函数语法有下列 4个：

int(f) 传回f对预设独立变数的积分值

int(f,'t') 传回f对独立变数t的积分值

int(f,a,b) 传回f对预设独立变数的积分值，积分区间为[a,b]，a和b为数值式

int(f,'t',a,b) 传回f对独立变数t的积分值，积分区间为[a,b]，a和b为数值式

int(f,'m','n') 传回f对预设变数的积分值，积分区间为[m,n]，m和n为符号式

我们示范几个例子：

>>S1 = '6*x^3-4*x^2+b*x-5';

>>S2 = 'sin(a)';

>>S3 = 'sqrt(x)';

>>int(S1)

ans= 3/2*x^4-4/3*x^3+1/2*b*x^2-5*x

>>int(S2)

ans= -cos(a)

>>int(S3)

ans= 2/3*x^(3/2)

>>int(S3,'a','b')

ans= 2/3*b^(3/2)- 2/3*a^(3/2)

>>int(S3,0.5,0.6)

ans= 2/25*15^(1/2)-1/6*2^(1/2)

>>numeric(int(S3,0.5,0.6)) % 使用numeric函数可以计算积分的数值

ans= 0.0741

** 2．3求解常微分方程式 **

MATLAB解常微分方程式的语法是dsolve('equation','condition')，其中equation代表常微分方程式即y'=g(x,y)，且
须以Dy代表一阶微分项y'　D2y代表二阶微分项y''　，

condition则为初始条件。

假设有以下三个一阶常微分方程式和其初始条件

y'=3x2, y(2)=0.5

y'=2.x.cos(y)2, y(0)=0.25

y'=3y+exp(2x), y(0)=3

对应上述常微分方程式的符号运算式为：

>>soln_1 = dsolve('Dy =3*x^2','y(2)=0.5')

ans= x^3-7.500000000000000

>>ezplot(soln_1,[2,4]) % 看看这个函数的长相

>>soln_2 = dsolve('Dy =2*x*cos(y)^2','y(0) = pi/4')

ans= atan(x^2+1)

>>soln_3 = dsolve('Dy = 3*y +exp(2*x)',' y(0) = 3')

ans= -exp(2*x)+4*exp(3*x)

** 2．4非线性方程式的实根 **

要求任一方程式的根有三步骤：

先定义方程式。要注意必须将方程式安排成 f(x)=0 的形态，例如一方程式为sin(x)=3，

则该方程式应表示为f(x)=sin(x)-3。可以 m-file 定义方程式。

代入适当范围的 x, y(x) 值，将该函数的分布图画出，藉以了解该方程式的「长相」。

由图中决定y(x)在何处附近(x0)与 x 轴相交，以fzero的语法fzero('function',x0)即可求出在 x0附近的根，其中
function 是先前已定义的函数名称。如果从函数分布图看出根不只一个，则须再代入另一个在根附近的 x0，再求出下一个根。

以下分别介绍几数个方程式，来说明如何求解它们的根。

例一、方程式为

sin(x)=0

我们知道上式的根有 ，求根方式如下：

>> r=fzero('sin',3) % 因为sin(x)是内建函数，其名称为sin，因此无须定义它,选择 x=3 附近求根

r=3.1416

>> r=fzero('sin',6) % 选择 x=6 附近求根

r = 6.2832

例二、方程式为MATLAB 内建函数 humps，我们不须要知道这个方程式的形态为何，不过我们可以将它划出来，再找出根的位置。求根方式如下：

>> x=linspace(-2,3);

>> y=humps(x);

>> plot(x,y), grid % 由图中可看出在0和1附近有二个根

![](http://img.my.csdn.net/uploads/201212/10/1355146359_4284.PNG)

>> r=fzero('humps',1.2)

r = 1.2995

例三、方程式为y=x.^3-2*x-5

这个方程式其实是个多项式，我们说明除了用 roots 函数找出它的根外，也可以用这节介绍的方法求根，注意二者的解法及结果有所不同。求根方式如下：

% m-function, f_1.m

function y=f_1(x) % 定义 f_1.m 函数

y=x.^3-2*x-5;

>> x=linspace(-2,3);

>> y=f_1(x);

>> plot(x,y), grid % 由图中可看出在2和-1附近有二个根

![](http://img.my.csdn.net/uploads/201212/10/1355146363_7773.PNG)

>> r=fzero('f_1',2); % 决定在2附近的根

r = 2.0946

>> p=[1 0 -2 -5]

>> r=roots(p) % 以求解多项式根方式验证

r =

2.0946

-1.0473 + 1.1359i 

-1.0473 - 1.1359i ** **

** 2．5线性代数方程（组）求解 **

我们习惯将上组方程式以矩阵方式表示如下

AX=B

其中 A 为等式左边各方程式的系数项，X 为欲求解的未知项，B 代表等式右边之已知项

要解上述的联立方程式，我们可以利用矩阵左除 \ 做运算，即是 X=A\B。

如果将原方程式改写成 XA=B

其中 A 为等式左边各方程式的系数项，X 为欲求解的未知项，B 代表等式右边之已知项

注意上式的 X, B 已改写成列向量，A其实是前一个方程式中 A 的转置矩阵。上式的 X 可以矩阵右除 / 求解，即是 X=B/A。

若以反矩阵运算求解 AX=B, X=B，即是 X=inv(A)*B，或是改写成 XA=B, X=B，即是X=B*inv(A)。

我们直接以下面的例子来说明这三个运算的用法：

>> A=[3 2-1; -1 3 2; 1 -1 -1]; % 将等式的左边系数键入

>> B=[10 5 -1]'; % 将等式右边之已知项键入，B要做转置

>> X=A\B % 先以左除运算求解

X = % 注意X为行向量

-2 

5

6

>> C=A*X % 验算解是否正确

C = % C=B

10

5

-1 

>> A=A'; % 将A先做转置

>> B=[10 5 -1];

>> X=B/A % 以右除运算求解的结果亦同

X = % 注意X为列向量

10 5  -1

>> X=B*inv(A); % 也可以反矩阵运算求解

** 3\.  基本  xy  平面绘图命令  **

MATLAB不但擅长於矩阵相关的数值运算，也适合用在各种科学目视表示（Scientificvisualization）。

本节将介绍MATLAB基本xy平面及xyz空间的各项绘图命令，包含一维曲线及二维曲面的绘制、列印及存档。

** plot  ** 是绘制一维曲线的基本函数，但在使用此函数之前，我们需先定义曲线上每一点的x 及y座标。 

下例可画出一条正弦曲线：

close all;

x=linspace(0, 2*pi, 100); % 100个点的x座标

y=sin(x); % 对应的y座标

plot(x,y);

![](http://img.my.csdn.net/uploads/201212/10/1355146367_2877.PNG)

小整理：MATLAB基本绘图函数

plot: x轴和y轴均为线性刻度（Linear scale）

loglog: x轴和y轴均为对数刻度（Logarithmic scale）

semilogx: x轴为对数刻度，y轴为线性刻度

semilogy: x轴为线性刻度，y轴为对数刻度

若要画出多条曲线，只需将座标对依次放入plot函数即可：

plot(x, sin(x), x, cos(x));

![](http://img.my.csdn.net/uploads/201212/10/1355146371_9498.PNG)

若要改变颜色，在座标对後面加上相关字串即可：

plot(x, sin(x), 'c', x, cos(x), 'g');

![](http://img.my.csdn.net/uploads/201212/10/1355146375_6834.PNG)

若要同时改变颜色及图线型态（Line style），也是在座标对後面加上相关字串即可：

plot(x, sin(x), 'co', x, cos(x), 'g*');

![](http://img.my.csdn.net/uploads/201212/10/1355146380_5276.PNG)

小整理：plot绘图函数的叁数 字元 颜色字元 图线型态y 黄色. 点k 黑色o 圆w 白色x  xb 蓝色+ +g 绿色* *r 红色- 实线c 亮青色:
点线m 锰紫色-. 点虚线-- 虚线

图形完成後，我们可用axis([xmin,xmax,ymin,ymax])函数来调整图轴的范围：

axis([0, 6, -1.2, 1.2]);

![](http://img.my.csdn.net/uploads/201212/10/1355146384_1191.PNG)

此外，MATLAB也可对图形加上各种注解与处理：

xlabel('Input Value'); % x轴注解

ylabel('Function Value'); % y轴注解

title('Two Trigonometric Functions'); % 图形标题

legend('y = sin(x)','y = cos(x)'); % 图形注解

grid on; % 显示格线

![](http://img.my.csdn.net/uploads/201212/10/1355146390_7227.PNG)

我们可用subplot来同时画出数个小图形於同一个视窗之中：

subplot(2,2,1); plot(x, sin(x));

subplot(2,2,2); plot(x, cos(x));

subplot(2,2,3); plot(x, sinh(x));

subplot(2,2,4); plot(x, cosh(x));

![](http://img.my.csdn.net/uploads/201212/10/1355146396_1855.PNG)

MATLAB还有其他各种二维绘图函数，以适合不同的应用，详见下表。

小整理：其他各种二维绘图函数

bar 长条图

errorbar 图形加上误差范围

fplot 较精确的函数图形

polar 极座标图

hist 累计图

rose 极座标累计图

stairs 阶梯图

stem 针状图

fill 实心图

feather 羽毛图

compass 罗盘图

quiver 向量场图

以下我们针对每个函数举例。

当资料点数量不多时，长条图是很适合的表示方式：

close all; % 关闭所有的图形视窗

x=1:10;

y=rand(size(x));

bar(x,y);

![](http://img.my.csdn.net/uploads/201212/10/1355146654_9229.PNG)

如果已知资料的误差量，就可用errorbar来表示。下例以单位标准差来做资的误差量：

x = linspace(0,2*pi,30);

y = sin(x);

e = std(y)*ones(size(x));

errorbar(x,y,e)

![](http://img.my.csdn.net/uploads/201212/10/1355146658_6983.PNG)

对於变化剧烈的函数，可用fplot来进行较精确的绘图，会对剧烈变化处进行较密集的取样，如下例：

fplot('sin(1/x)', [0.02 0.2]); % [0.02 0.2]是绘图范围

![](http://img.my.csdn.net/uploads/201212/10/1355146661_1597.PNG)

若要产生极座标图形，可用polar：

theta=linspace(0, 2*pi);

r=cos(4*theta);

polar(theta, r);

![](http://img.my.csdn.net/uploads/201212/10/1355146665_5511.PNG)

对於大量的资料，我们可用hist来显示资料的分　情况和统计特性。下面几个命令可用来验证randn产生的高斯乱数分　：

x=randn(5000, 1); % 产生5000个 m=0，s=1 的高斯乱数

hist(x,20); % 20代表长条的个数

![](http://img.my.csdn.net/uploads/201212/10/1355146669_6772.PNG)

rose和hist很接近，只不过是将资料大小视为角度，资料个数视为距离，并用极座标绘制

表示：

x=randn(1000, 1);

rose(x);

![](http://img.my.csdn.net/uploads/201212/10/1355146674_2440.PNG)

stairs可画出阶梯图：

x=linspace(0,10,50);

y=sin(x).*exp(-x/3);

stairs(x,y);

![](http://img.my.csdn.net/uploads/201212/10/1355146679_3015.PNG)

stems可产生针状图，常被用来绘制数位讯号：

x=linspace(0,10,50);

y=sin(x).*exp(-x/3);

stem(x,y);

![](http://img.my.csdn.net/uploads/201212/10/1355146683_5392.PNG)

stairs将资料点视为多边行顶点，并将此多边行涂上颜色：

x=linspace(0,10,50);

y=sin(x).*exp(-x/3);

fill(x,y,'b'); % 'b'为蓝色

![](http://img.my.csdn.net/uploads/201212/10/1355146894_9854.PNG)

feather将每一个资料点视复数，并以箭号画出：

theta=linspace(0, 2*pi, 20);

z = cos(theta)+i*sin(theta);

feather(z);

![](http://img.my.csdn.net/uploads/201212/10/1355146898_8771.PNG)

compass和feather很接近，只是每个箭号的起点都在圆点：

theta=linspace(0, 2*pi, 20);

z = cos(theta)+i*sin(theta);

compass(z);

![](http://img.my.csdn.net/uploads/201212/10/1355146901_2559.PNG)

** 4  ．基本  XYZ  立体绘图命令  **

在科学目视表示（Scientific
visualization）中，三度空间的立体图是一个非常重要的技巧。本章将介绍MATLAB基本XYZ三度空间的各项绘图命令。

mesh和plot是三度空间立体绘图的基本命令，mesh可画出立体网状图，plot则可画出立体曲面图，两者产生的图形都会依高度而有不同颜色。

下列命令可画出由函数<图片>形成的立体网状图:

x=linspace(-2, 2, 25); % 在x轴上取25点

y=linspace(-2, 2, 25); % 在y轴上取25点

[xx,yy]=meshgrid(x, y); % xx和yy都是21x21的矩阵

zz=xx.*exp(-xx.^2-yy.^2); % 计算函数值，zz也是21x21的矩阵

mesh(xx, yy, zz); % 画出立体网状图

![](http://img.my.csdn.net/uploads/201212/10/1355146908_3740.PNG)

surf和mesh的用法类似：

x=linspace(-2, 2, 25); % 在x轴上取25点

y=linspace(-2, 2, 25); % 在y轴上取25点

[xx,yy]=meshgrid(x, y); % xx和yy都是21x21的矩阵

zz=xx.*exp(-xx.^2-yy.^2); % 计算函数值，zz也是21x21的矩阵

surf(xx, yy, zz); % 画出立体曲面图

![](http://img.my.csdn.net/uploads/201212/10/1355146913_1127.PNG)

为了方便测试立体绘图，MATLAB提供了一个peaks函数，可产生一个凹凸有致的曲面，包含了三个局部极大点及三个局部极小点

要画出此函数的最快方法即是直接键入peaks：

peaks

![](http://img.my.csdn.net/uploads/201212/10/1355146917_7745.PNG)

z = 3*(1-x).^2.*exp(-(x.^2) - (y+1).^2) ...

\- 10*(x/5 - x.^3 - y.^5).*exp(-x.^2-y.^2) ...

\- 1/3*exp(-(x+1).^2 - y.^2)

我们亦可对peaks函数取点，再以各种不同方法进行绘图。

meshz可将曲面加上围裙：

[x,y,z]=peaks;

meshz(x,y,z);

axis([-inf inf -inf inf -inf inf]);

![](http://img.my.csdn.net/uploads/201212/10/1355146921_1534.PNG)

waterfall可在x方向或y方向产生水流效果：

[x,y,z]=peaks;

waterfall(x,y,z);

axis([-inf inf -inf inf -inf inf]);

![](http://img.my.csdn.net/uploads/201212/10/1355146926_1023.PNG)

下列命令产生在y方向的水流效果：

[x,y,z]=peaks;

waterfall(x',y',z');

axis([-inf inf -inf inf -inf inf]);

![](http://img.my.csdn.net/uploads/201212/10/1355147192_2294.PNG)

meshc同时画出网状图与等高线：

[x,y,z]=peaks;

meshc(x,y,z);

axis([-inf inf -inf inf -inf inf]);

![](http://img.my.csdn.net/uploads/201212/10/1355147196_1383.PNG)

surfc同时画出曲面图与等高线：

[x,y,z]=peaks;

surfc(x,y,z);

axis([-inf inf -inf inf -inf inf]);

![](http://img.my.csdn.net/uploads/201212/10/1355147200_4698.PNG)

contour3画出曲面在三度空间中的等高线：

contour3(peaks, 20);

axis([-inf inf -inf inf -inf inf]);

![](http://img.my.csdn.net/uploads/201212/10/1355147204_3332.PNG)

contour画出曲面等高线在XY平面的投影：

contour(peaks, 20);

![](http://img.my.csdn.net/uploads/201212/10/1355147208_7347.PNG)

plot3可画出三度空间中的曲线：

t=linspace(0,20*pi, 501);

plot3(t.*sin(t), t.*cos(t), t);

![](http://img.my.csdn.net/uploads/201212/10/1355147212_3506.PNG)

亦可同时画出两条三度空间中的曲线：

t=linspace(0, 10*pi, 501);

plot3(t.*sin(t), t.*cos(t), t, t.*sin(t), t.*cos(t), -t);

![](http://img.my.csdn.net/uploads/201212/10/1355147216_8236.PNG)

** 4\.  三维网图的高级处理  **

** 1.      消隐处理 **

例.比较网图消隐前后的图形

z=peaks(50);

subplot(2,1,1);

mesh(z);

title('消隐前的网图')

hidden off

subplot(2,1,2)

mesh(z);

title('消隐后的网图')

hidden on

colormap([0 0 1])

![](http://img.my.csdn.net/uploads/201212/10/1355147220_5581.PNG)

** 2.      裁剪处理 **

利用不定数NaN的特点,可以对网图进行裁剪处理

例.图形裁剪处理

P=peaks(30);

subplot(2,1,1);

mesh(P);

title('裁剪前的网图')

subplot(2,1,2);

P(20:23,9:15)=NaN*ones(4,7);       %剪孔

meshz(P)                        %垂帘网线图

title('裁剪后的网图')

colormap([0 0 1])                  %蓝色网线

![](http://img.my.csdn.net/uploads/201212/10/1355147227_3355.PNG)

注意裁剪时矩阵的对应关系,即大小一定要相同.

** 3.      三维旋转体的绘制 **

为了一些专业用户可以更方便地绘制出三维旋转体,MATLAB专门提供了2个函数:柱面函数cylinder和球面函数sphere

** (1)   柱面图 **

柱面图绘制由函数cylinder实现.

[X,Y,Z]=cylinder(R,N)
此函数以母线向量R生成单位柱面.母线向量R是在单位高度里等分刻度上定义的半径向量.N为旋转圆周上的分格线的条数.可以用surf(X,Y,Z)来表示此柱面.

[X,Y,Z]=cylinder(R)或[X,Y,Z]=cylinder此形式为默认N=20且R=[1 1]

例.柱面函数演示举例

x=0:pi/20:pi*3;

r=5+cos(x);

[a,b,c]=cylinder(r,30);

mesh(a,b,c)

![](http://img.my.csdn.net/uploads/201212/10/1355147232_7826.PNG)

  

  

例.旋转柱面图.

r=abs(exp(-0.25*t).*sin(t));

t=0:pi/12:3*pi;

r=abs(exp(-0.25*t).*sin(t));

[X,Y,Z]=cylinder(r,30);

mesh(X,Y,Z)

colormap([1 0 0])

![](http://img.my.csdn.net/uploads/201212/10/1355147237_4530.PNG)

  

** (2).球面图 **

球面图绘制由函数sphere来实现

[X,Y,Z]=sphere(N)             此函数生成3个(N+1)*(N+1)的矩阵,利用函数        surf(X,Y,Z)
可产生单位球面.

[X,Y,Z]=sphere         此形式使用了默认值N=20.

Sphere(N)             只是绘制了球面图而不返回任何值.

例.绘制地球表面的气温分布示意图.

[a,b,c]=sphere(40);

t=abs(c);

surf(a,b,c,t);

axis('equal')   %此两句控制坐标轴的大小相同.

axis('square')

colormap('hot')

![](http://img.my.csdn.net/uploads/201212/10/1355147242_4894.PNG)

[ http://www.5678520.com/kaiwangdian/130.html
](http://www.5678520.com/kaiwangdian/130.html)

[ http://www.5678520.com/kaiwangdian/129.html
](http://www.5678520.com/kaiwangdian/129.html)

[ http://www.5678520.com/kaiwangdian/128.html
](http://www.5678520.com/kaiwangdian/128.html)

[ http://www.5678520.com/kaiwangdian/127.html
](http://www.5678520.com/kaiwangdian/127.html)

[ http://www.5678520.com/kaiwangdian/126.html
](http://www.5678520.com/kaiwangdian/126.html)

[ http://www.lianzhiwei.com/News/389/20122116.html
](http://www.lianzhiwei.com/News/389/20122116.html)

[ http://www.lianzhiwei.com/News/389/20122115.html
](http://www.lianzhiwei.com/News/389/20122115.html)

[ http://www.lianzhiwei.com/News/389/20122114.html
](http://www.lianzhiwei.com/News/389/20122114.html)

[ http://www.lianzhiwei.com/News/389/20122113.html
](http://www.lianzhiwei.com/News/389/20122113.html)

[ http://www.lianzhiwei.com/News/389/20122112.html
](http://www.lianzhiwei.com/News/389/20122112.html)


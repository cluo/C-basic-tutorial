<h1>“&” 与 “*”</h1>

取地址与指针运算符(取值运算)

“&” 对变量进行取地址运算:
&(变量名)   =>   获取变量的地址
如：
[code lang="c"]
int i;
printf("%d", &i);  // 打印出地址
[/code]

如: 
[code lang="c"]
scanf("%d", &i);  // 传入一个地址
[/code]

而“*”作为指针运算符，当然我更乐意称它为取值运算：
*(变量名)   =>   将变量当做地址,到相应的地址取值

思考：

*(&(变量名)) 是什么？

[code lang="c"]
int i = 6;
printf( "%d", *(&i) );
[/code]

<h1>什么是指针变量？</h1>

指针变量就是用来存储地址的变量

任何变量都它存储的地址，这个地址是随机分配的。如：
[code lang="c"]
int i = 10;
[/code]
i 这个变量的地址，是系统随机分配的。而我们对其进行 “&” 运算之后就可以得到它的地址，并且 (&i) 这个表达式就是一个指向i的指针。

这个指针所指向的地址中存储的值则是：
*(&i)  ==>  i



<h1>声明与初始化</h1>

声明方式：

指针类型 * 指针变量名;

例如：
[code lang="c"]
int *p1;
char *name;
[/code]

初始化：

1)普通写法
[code lang="c"]
int x; 
int *p;
p = &x;
[/code]
2)省略写法
[code lang="c"]
int x;
int *p = &x;
[/code]

上述两种写法都声明了一个指针p,并且这个指针是指向变量 x 的
对于变量 x, (&x) 则是一个指向x的指针 （指针存放的就是地址, 而&运算得到的地址表达式也就是指向其本身的指针）
并且通过 *(指针) 取到这个地址中的值

<h1>常见错误</h1>

请不要人为的指派地址：
[code lang="c"]
// 错误1
int *p;
p = 10010;   

// 错误2
int x = 20;
printf("%d", &(*x) );

// 正确形式：
int i, *p, *t;
p = &i;
t = p;
[/code]
只能通过已有的变量传递

<h2>经典的错误 - Scanf函数</h2>

[code lang="c"]
int score;
printf("请输入你的分数：\n");
scanf("%d", score);
[/code]
上述代码在编译时没有错，运行时会出现严重的错误

错误原因：
scanf() 函数后面的参数应该传入的是指针，而这里直接把 score 的值传了进去。

正确应该是：
[code lang="c"]
int score;
printf("请输入你的分数：\n");
scanf("%d", &score);
[/code]


<h2>Swap交换两个变量</h2>

与第五讲中不同的是,使用指针到某个地址中取访问它的值,就没有了作用域的限制

[code lang="c"]
#include<stdio.h>

void swap(int *x, int *y)
{
    int temp;
    temp = *x;
    *x = *y;
    *y = temp;
    printf("x=%d, y=%d \n", *x, *y);
}

main()
{
    int i = 13, j = 45;
    swap(&i, &j);
    printf("i=%d, j=%d\n", i, j);
}
[/code]


<h1>本讲小结</h1>

1) “&” 和 “*”

取地址与取值运算符   ==>   互为逆运算

2)指针变量是什么?

指针变量就是用来存储地址的变量
如,&i 就是一个指向变量i 的指针
通过*(指针)取值

3)声明

int *p1;
char *name;

4)初始化

普通写法
[code lang="c"]
int x; 
int *p;
p = &x;
[/code]

省略写法
[code lang="c"]
int x;
int *p = &x;
[/code]

5)指针的作用
引用类型，传递地址，减少内存消耗


<h1>课后作业</h1>

现在有一个数组，存储的是一个同学的期中考试成绩。
[code lang="c"]
int score[8] = { 75, 86, 70, 88, 62, 87, 69, 77 };
[/code]
那么现在我们要做的事情是：

1)求总分，求平均分

2)用指针遍历数组，求最大值和最小值

附加题：
用一个二维数组存储八门课的名称，例如：
[code lang="c"]
char course[8][256] = { "chinese", "English", ... }
[/code]
再用二维数组，存储多个人的成绩，用指针遍历求出每门课的平均分


<h1><a href="http://www.lellansin.com/c%e8%af%ad%e8%a8%80%e5%85%a5%e9%97%a8%e6%95%99%e7%a8%8b-%e7%ac%ac9%e8%ae%b2-%e6%8c%87%e9%92%88%e4%b8%8e%e6%95%b0%e7%bb%84.html" title="Permalink to C语言入门教程 第9讲 指针与数组" rel="bookmark">C语言入门教程 第9讲 指针与数组</a></h1>
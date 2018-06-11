---
title: C语言问题记录
date: 2018-06-11 15:40:47
tags: C&C++
---

<!-- more -->

<ol>

##### <li> 原码，反码和补码
http://www.itwendao.com/article/detail/8172.html
https://yq.aliyun.com/wenji/72426
http://blog.csdn.net/liushuijinger/article/details/7429197
https://www.cnblogs.com/zhangziqiu/archive/2011/03/30/ComputerCode.html
http://blog.chinaunix.net/uid-29603939-id-4216336.html
http://blog.sina.com.cn/s/blog_6b87c7eb010186mp.html
```
我们知道在计算机系统中，数值一律用补码来表示（存储）。主要原因是使用补码，可以将符号位和其它位统一处理；同时，减法也可按加法来处理。另外，两个用补码表示的数相加时，如果最高位（符号位）有进位，则进位被舍弃。

补码表示法（two's complement representation）可以防止0的机器数重码，同时又解决了原码和反码无法表示－8的问题，这样就极大的简化了计算机的硬件设计。

什么是数制？用来表示数值的规则，如十进制，二进制．

机器数

用二进制的形式来表示数;最高位为符号位,1表示负数,0表示正数.

如:  1---->00000001;-1---->1000 0001

真值

从上面我们知道了机器数是计算机用来表示数的一种形式，但是用于最高位是符号位。这样就出现这样情况，1000 0001表示的真正数值为1，而不是129.这样我们把一个机器数表示的真正的实际的意义的值称之为真值。

原码、反码、补码

总体上来讲原码反码补码都是计算机本身用来存储数的一种方式。
原码

规则：符号位+真值的绝对值

如：[+1]原码=0000 0001；

[-1]原码=1000 0001；
反码

规则：正数反码为本身

负数反码为原码的取反，但符号位不变

如：[+1]原码=[+1]反码=0000 0001；

[-1]原码=1000 0001=[-1]反码=1111 1110;
补码

规则：正数补码为本身

负数补码为原码的反码的基础之上加1

如：[+1]原码=[+1]补码；

[-1]原码=1000 0001=[-1]反码=1111 1110=[-1]补码=1111 1111；

为何会出现三种表示方式？

通过上面三种我们得到正数1在各种情况下都是一致的：[+1]原\反\补码=0000 00001；

而反码不是一致的。

在计算机内部，为了将运算变得简单。将符号位也投入到运算之中来，这样不需要计算机去分析符号位的作用。但是我们发现

[+1]原码=0000 0001+[-1]原码=1000 0001=0000 00001=1；而不是0，这样一来就出现了错误。如何解决这个问题呢？

为了解决这个问题，反码出现了

[+1]原码+[-1]原码=1000 0001=[+1]反码=0000 0001+[-1]反码=1111 1110=0000 0000（反码）=0000 0000 （原码）=-0；

这样一来解决了原码之间运算的问题，但是问题又出现了-0=1000 0000（原码）；+0=0000 0000 （原码）；这样在计算机看来不一样。是没有意义的。

[+1]原码+[-1]原码=1000 0001=[+1]补码=0000 0001+[-1]补码=1111 1111=0000 0000（补码）=[0000 0000](原码)

这样用[0000 0000](原码)表示0就不会出现问题了。

总的来说，在整数中，原码和补码、反码都是一样的，对于负数反码在符号位不变的情况下各位取反所得；补码为反码基础上加1.而原码补码反码的出现都是为了满足在计算机在运算过程更加简单和便捷而出现的。
```

##### <li> 浮点数在内存中存放格式
http://blog.sina.com.cn/s/blog_77abbf390100qwun.html
https://www.pediy.com/kssd/pediy03/forum669.htm
https://www.2cto.com/kf/201708/672079.html
http://blog.csdn.net/PfanAya/article/details/5770005
https://yq.aliyun.com/ziliao/123603
http://blog.csdn.net/hdutigerkin/article/details/7663454
```
对于大小为32-bit的浮点数（32-bit为单精度，64-bit浮点数为双精度，80-bit为扩展精度浮点数），
1、其第31 bit为符号位，为0则表示正数，反之为复数，其读数值用s表示；
2、第30～23 bit为幂数，其读数值用e表示；
3、第22～0 bit共23 bit作为系数，视为二进制纯小数，假定该小数的十进制值为x；

则按照规定，该浮点数的值用十进制表示为：
＝ (-1)^s  * (1 + x) * 2^(e - 127)

对于49E48E68来说，
1、其第31 bit为0，即s = 0
2、第30～23 bit依次为100 1001 1，读成十进制就是147，即e = 147。
3、第22～0 bit依次为110 0100 1000 1110 0110 1000，也就是二进制的纯小数0.110 0100 1000 1110 0110 1000，其十进制形式为0.78559589385986328125，即x = 0.78559589385986328125。

这样，该浮点数的十进制表示
=　(-1)^s  * (1 + x) * 2^(e - 127)
=　(-1)^0  * (1+ 0.78559589385986328125) * 2^(147-127)
= 1872333


任何数据在内存中都是以二进制的形式存储的，例如一个short型数据1156，其二进制表示形式为00000100 10000100。则在Intel CPU架构的系统中，存放方式为  10000100(低地址单元) 00000100(高地址单元)，因为Intel CPU的架构是小端模式。但是对于浮点数在内存是如何存储的?目前所有的C/C++编译器都是采用IEEE所制定的标准浮点格式，即二进制科学表示法。
在二进制科学表示法中，S=M*2^N 主要由三部分构成：符号位+阶码(N)+尾数(M)。对于float型数据，其二进制有32位，其中符号位1位，阶码8位，尾数23位；对于double型数据，其二进制为64位，符号位1位，阶码11位，尾数52位。
                31        30-23       22-0
float       符号位     阶码        尾数
                63        62-52       51-0
double    符号位     阶码        尾数
符号位：0表示正，1表示负
阶码：这里阶码采用移码表示，对于float型数据其规定偏置量为127,阶码有正有负，对于8位二进制，则其表示范围为-128-127，double型规定为1023，其表示范围为-1024-1023。比如对于float型数据，若阶码的真实值为2，则加上127后为129，其阶码表示形式为10000010
尾数:有效数字位，即部分二进制位(小数点后面的二进制位)，因为规定M的整数部分恒为1，所以这个1就不进行存储了。
下面举例说明：
float型数据125.5转换为标准浮点格式
125二进制表示形式为1111101，小数部分表示为二进制为 1，则125.5二进制表示为1111101.1，由于规定尾数的整数部分恒为1，则表示为1.1111011*2^6，阶码为6，加上127为133，则表示为10000101，而对于尾数将整数部分1去掉，为1111011，在其后面补0使其位数达到23位，则为11110110000000000000000
则其二进制表示形式为
0 10000101 11110110000000000000000，则在内存中存放方式为：
00000000   低地址
00000000
11111011
01000010   高地址
而反过来若要根据二进制形式求算浮点数如0 10000101 11110110000000000000000
由于符号为为0，则为正数。阶码为133-127=6，尾数为11110110000000000000000，则其真实尾数为1.1111011。所以其大小为
1.1111011*2^6，将小数点右移6位，得到1111101.1，而1111101的十进制为125，0.1的十进制为1*2^(-1)=0.5，所以其大小为125.5。
同理若将float型数据0.5转换为二进制形式
0.5的二进制形式为0.1，由于规定正数部分必须为1，将小数点右移1位，则为1.0*2^(-1)，其阶码为-1+127=126，表示为01111110，而尾数1.0去掉整数部分为0，补齐0到23位00000000000000000000000，则其二进制表示形式为
0 01111110 00000000000000000000000
由上分析可知float型数据最大表示范围为1.11111111111111111111111*2^127=3.4*10^38
对于double型数据情况类似，只不过其阶码为11位，偏置量为1023，尾数为52位。

测试程序：
复制代码 代码如下:

/*测试浮点型数据在内存中存放方式  2011.10.2*/
#include <iostream>
using namespace std;
int main(int argc, char *argv[])
{
    float a=125.5;
    char *p=(char *)&a;
    printf("%d\n",*p);
    printf("%d\n",*(p+1));
    printf("%d\n",*(p+2));
    printf("%d\n",*(p+3));
    return 0;
}

输出结果为：
0
0
-5
66

在上面已经知道float型125.5在内存中存放方式为：
00000000   低地址
00000000
11111011
01000010   高地址
因此对于p和p+1指向的单元，其中存储的二进制数表示的十进制整数为0；
而对于p+2指向的单元，由于为char型指针，为带符号的数据类型，因此11111011，符号位为1，则为负数，由于在内存中二进制是以补码存储的，所以其真值为-5.
对于p+3指向的单元，01000010，为正数，则其大小为66。上面程序输出结果验证了其正确性。
```

##### <li> C数组初始化
http://blog.csdn.net/sibylle/article/details/2026915
http://lib.csdn.net/article/c/19784
http://www.cnblogs.com/youxin/p/3235817.html
http://www.cnblogs.com/Harley-Quinn/p/6766705.html
```
int a[100] = {0}; // 第一个元素初始化为0，后面的元素进行默认初始化，为0
int a[100] = {1, 2, 3, 4}; //前四个元素依次初始化为1,2,3,4；后面的所有元素进行默认初始化，为0
int a[] = {1,2,3,4,5}; // 1, 2, 3, 4, 5
int chr[] = {'a', 'b', 'c'}; // a, b, c, \0

初始化值的个数可少于数组元素个数.当初始化值的个数少于数组元素个数时,前面的按序初始化相应值, 后面的初始化为0(全局或静态数组)或为不确定值(局部数组).


一直以为 int a[256]={0};是把a的所有元素初始化为0，int a[256]={1};是把a所有的元素初始化为1.
调试的时查看内存发现不是那么一回事，翻了一下《The C++ Programming Language》总算有定论。PDF的竟然不然复制，就把它这章翻译了，如下

5.2.1   数组初始化
数组可以用一个列值来初始化，例如
         int v1[] ={1,2,3,4};
         char v2[]={'a','b','c',0};
当数组定义时没有指定大小，当初始化采用列表初始化了，那么数组的大小由初始化时列表元素个数决定。所以v1和v2分别为 int[4] 和char[4]类型。如果明确指定了数组大小，当在初始化时指定的元素个数超过这个大小就会产生错误。例如：
         char   v3[2] ={'a','b',0};   //错误：太多的初始化值了
         char   v3[3] ={'a','b',0};   //正确

如果初始化时指定的的元素个数比数组大小少，剩下的元素都回被初始化为   0。例如
         int   v5[8]={1,2,3,4};
等价于
          int   v5[8]={1,2,3,4,0,0,0,0};

注意没有如下形式的数组赋值：
         void f()
         {
             v4={'c','d',0};   //错误：不是数组赋值
         }
如果你想这样的复制的话，请使用 vector(16章第三节) 或者 valarray（22章第四节）。
        字符数组可以方便地采用字符串直接初始化（参考第五章 2.2小节）
         译注： 就是 这样啦   char   alpha []="abcdefghijklmn";

*/
```

##### <li> 结构体成员赋值
```
struct CMUnitTestState {
    const ListNode *check_point; /* Check point of the test if there's a setup function. */
    const struct CMUnitTest *test; /* Point to array element in the tests we get passed */
    void *state; /* State associated with the test */
    const char *error_message; /* The error messages by the test */
    enum CMUnitTestStatus status; /* PASSED, FAILED, ABORT ... */
    double runtime; /* Time calculations */
};

/* Setup cmocka test array */
for (i = 0; i < num_tests; i++) {
    if (tests[i].name != NULL &&
        (tests[i].test_func != NULL
         || tests[i].setup_func != NULL
         || tests[i].teardown_func != NULL)) {
        cm_tests[i] = (struct CMUnitTestState) {
            .test = &tests[i],
            .status = CM_TEST_NOT_STARTED,
            .state = NULL,
        };
        total_tests++;
    }
}
```

##### <li> C语言实现变长数组
```
typedef struct
{
    int data_len;
    char data[];
}data_buf;

typedef struct
{
    int data_len;
    char data[0];
}data_buf;
````

##### <li> 特殊符号"#、##"
```
http://www.cnblogs.com/Anker/p/3418792.html
http://blog.csdn.net/acs713/article/details/6891837
http://www.cnblogs.com/welkinwalker/archive/2012/03/30/2424844.html

（1）#

  When you put a # before an argument in a preprocessor  macro, the preprocessor turns that argument into a character array.

  在一个宏中的参数前面使用一个#,预处理器会把这个参数转换为一个字符数组

  简化理解：#是“字符串化”的意思，出现在宏定义中的#是把跟在后面的参数转换成一个字符串

\#define ERROR_LOG(module)   fprintf(stderr,"error: "#module"\n")

ERROR_LOG("add"); 转换为 fprintf(stderr,"error: "add"\n");

ERROR_LOG(devied =0); 转换为 fprintf(stderr,"error: devied=0\n");

（2）##

  “##”是一种分隔连接方式，它的作用是先分隔，然后进行强制连接。

  在普通的宏定义中，预处理器一般把空格解释成分段标志，对于每一段和前面比较，相同的就被替换。但是这样做的结果是，被替换段之间存在一些空格。如果我们不希望出现这些空格，就可以通过添加一些##来替代空格。

1 #define TYPE1(type,name)   type name_##type##_type
2 #define TYPE2(type,name)   type name##_##type##_type

TYPE1(int, c); 转换为：int 　name_int_type ; (因为##号将后面分为 name_ 、type 、 _type三组，替换后强制连接)
TYPE2(int, d);转换为： int 　d_int_type ; (因为##号将后面分为 name、_、type 、_type四组，替换后强制连接)
```

##### <li> strstr和strchr的区别
http://blog.csdn.net/wusuopubupt/article/details/38741015
```
通过函数的定义来区分：

1.strstr:

[cpp] view plain copy

    char *strstr(const char *haystack, const char *needle)

可见，strstr函数搜索的是一个const char*型的数据，即字符串常量


2.strchr:

[cpp] view plain copy

    char *strchr(const char *str, int c)

而strchr搜索的是一个int型的数据，即字符


3.strrchr

[cpp] view plain copy

    char *strrchr(const char *str, int c)

另外，strrchr返回字符c在字符串str中最后出现的位置
```

##### <li> \_\_FILE\_\_, \_\_LINE\_\_ and \_\_func\_\_
```
https://gcc.gnu.org/onlinedocs/cpp/Standard-Predefined-Macros.html

3.7.1 Standard Predefined Macros

The standard predefined macros are specified by the relevant language standards, so they are available with all compilers that implement those standards. Older compilers may not provide all of them. Their names all start with double underscores.

__FILE__

    This macro expands to the name of the current input file, in the form of a C string constant. This is the path by which the preprocessor opened the file, not the short name specified in ‘#include’ or as the input file name argument. For example, "/usr/local/include/myheader.h" is a possible expansion of this macro.
__LINE__

    This macro expands to the current input line number, in the form of a decimal integer constant. While we call it a predefined macro, it’s a pretty strange macro, since its “definition” changes with each new line of source code.

__FILE__ and __LINE__ are useful in generating an error message to report an inconsistency detected by the program; the message can state the source line at which the inconsistency was detected. For example,

fprintf (stderr, "Internal error: "
                 "negative string length "
                 "%d at %s, line %d.",
         length, __FILE__, __LINE__);

An ‘#include’ directive changes the expansions of __FILE__ and __LINE__ to correspond to the included file. At the end of that file, when processing resumes on the input file that contained the ‘#include’ directive, the expansions of __FILE__ and __LINE__ revert to the values they had before the ‘#include’ (but __LINE__ is then incremented by one as processing moves to the line after the ‘#include’).

A ‘#line’ directive changes __LINE__, and may change __FILE__ as well. See Line Control.

C99 introduced __func__, and GCC has provided __FUNCTION__ for a long time. Both of these are strings containing the name of the current function (there are slight semantic differences; see the GCC manual). Neither of them is a macro; the preprocessor does not know the name of the current function. They tend to be useful in conjunction with __FILE__ and __LINE__, though.

__DATE__

    This macro expands to a string constant that describes the date on which the preprocessor is being run. The string constant contains eleven characters and looks like "Feb 12 1996". If the day of the month is less than 10, it is padded with a space on the left.

    If GCC cannot determine the current date, it will emit a warning message (once per compilation) and __DATE__ will expand to "??? ?? ????".
__TIME__

    This macro expands to a string constant that describes the time at which the preprocessor is being run. The string constant contains eight characters and looks like "23:59:01".

    If GCC cannot determine the current time, it will emit a warning message (once per compilation) and __TIME__ will expand to "??:??:??".
__STDC__

    In normal operation, this macro expands to the constant 1, to signify that this compiler conforms to ISO Standard C. If GNU CPP is used with a compiler other than GCC, this is not necessarily true; however, the preprocessor always conforms to the standard unless the -traditional-cpp option is used.

    This macro is not defined if the -traditional-cpp option is used.

    On some hosts, the system compiler uses a different convention, where __STDC__ is normally 0, but is 1 if the user specifies strict conformance to the C Standard. CPP follows the host convention when processing system header files, but when processing user files __STDC__ is always 1. This has been reported to cause problems; for instance, some versions of Solaris provide X Windows headers that expect __STDC__ to be either undefined or 1. See Invocation.
__STDC_VERSION__

    This macro expands to the C Standard’s version number, a long integer constant of the form yyyymmL where yyyy and mm are the year and month of the Standard version. This signifies which version of the C Standard the compiler conforms to. Like __STDC__, this is not necessarily accurate for the entire implementation, unless GNU CPP is being used with GCC.

    The value 199409L signifies the 1989 C standard as amended in 1994, which is the current default; the value 199901L signifies the 1999 revision of the C standard. Support for the 1999 revision is not yet complete.

    This macro is not defined if the -traditional-cpp option is used, nor when compiling C++ or Objective-C.
__STDC_HOSTED__

    This macro is defined, with value 1, if the compiler’s target is a hosted environment. A hosted environment has the complete facilities of the standard C library available.
__cplusplus

    This macro is defined when the C++ compiler is in use. You can use __cplusplus to test whether a header is compiled by a C compiler or a C++ compiler. This macro is similar to __STDC_VERSION__, in that it expands to a version number. Depending on the language standard selected, the value of the macro is 199711L for the 1998 C++ standard, 201103L for the 2011 C++ standard, 201402L for the 2014 C++ standard, or an unspecified value strictly larger than 201402L for the experimental languages enabled by -std=c++1z and -std=gnu++1z.
__OBJC__

    This macro is defined, with value 1, when the Objective-C compiler is in use. You can use __OBJC__ to test whether a header is compiled by a C compiler or an Objective-C compiler.
__ASSEMBLER__

    This macro is defined with value 1 when preprocessing assembly language.


http://www.oschina.net/question/249672_59411
#ifndef _debug_H_
#define _debug_H_

#include <stdlib.h>
#include <stdio.h>
#include <stdarg.h>

#ifndef UNDEBUG_FILE
#define DEBUG_FLAG 1
#else
#define DEBUG_FLAG 0
#endif

#if (DEBUG_FLAG == 1)

static unsigned int __sdebug_time = 0;
#define  __debug_Msg_Size 1024
static char __pdebug_Msg[__debug_Msg_Size];
//注意下面的__attribute__不是C标准。。。。
static void __debug_info(const char *prefix,const char *fmt, ...) __attribute__((format (printf, 2, 3)));
#define __NEXT_DBG_TIME() do{sdebug_time++;}while(0)
#define __PRINT_POS() do {fprintf(stderr,"%s(%d){%s}",__FILE__,__LINE__,__func__);}while(0)
#define __FUNC_LOG() do{__PRINT_POS();fprintf(stderr,": t = %d ",__sdebug_time++);} while(0)
#define __FUNC_LOGn() do{__FUNC_LOG();fprintf(stderr,"\n");} while(0)
#define __PRINT_POS_exp(exp) do{__PRINT_POS();fprintf(stderr,"| (%s):",#exp);}while(0)
#define __PRINT_POS_P_exp(prefix,exp) do{__PRINT_POS();fprintf(stderr,"|<%s> (%s):",prefix,#exp);}while(0)
#define __PRINT_POS_expn(exp)  do{__PRINT_POS_exp(exp);fprintf(stderr,"\n");}while(0)
#define __PRINT_POS_P_expn(prefix,exp) do{__PRINT_POS_P_exp(prefix,exp);fprintf(stderr,"\n");}while(0)
#define __ASSERT(exp) do{if (exp){}else{__PRINT_POS_P_expn("ASSERT ERROR",exp);}}while (0)
#define __ASSERT_EXIT(exp) do{if (exp){}else{__PRINT_POS_P_expn("ASSERT ERROR",exp);exit(1);}}while (0)

#define __debug_info_LOG(exp,PREFIX,fmt,...) do{if (exp){__PRINT_POS_P_exp(PREFIX,exp);__debug_info(PREFIX,fmt,__VA_ARGS__);}}while (0)

#define __ASSERT_LOG(exp,fmt,...) __debug_info_LOG(exp,"ASSERT!",fmt,__VA_ARGS__)
#define __ERROR_LOG(exp,fmt,...) __debug_info_LOG(exp,"ERROR!",fmt,__VA_ARGS__)
define __BEFORE_LOG(N,fmt,...)  do {__debug_info_LOG((N) < __sdebug_time,"BEFORE!",fmt,__VA_ARGS__);__NEXT_DBG_TIME()}while(0)
#define __AFTER_LOG(N,fmt,...) do {__debug_info_LOG((N) >= __sdebug_time,"AFTER!",fmt,__VA_ARGS__); __NEXT_DBG_TIME();}while(0)
static void __debug_info(const char *prefix,const char *fmt, ...) {
	va_list params;
	va_start(params, fmt);
	__ASSERT_EXIT((__pdebug_Msg) && (__pdebug_Msg_Size ));
	vsnprintf(__pdebug_Msg, __pdebug_Msg_Size, fmt, params);
	if (prefix){
		fprintf(stderr, " %s %s\n", prefix, __pdebug_Msg);
	}else{
		fprintf(stderr, " %s\n", __pdebug_Msg);
	}
	va_end(params);
}
#else
#define __NOP do{}while(0)
#define __NEXT_DEBUG_TIME() __NOP
#define __FUNC_LOGn() __NOP
#define __FUNC_LOG() __NOP
#define __PRINT_POS_Sn(exp)  __NOP
#define __PRINT_POS_S(exp) __NOP
#define __ASSERT(exp) __NOP
#define __ASSERT_EXIT(exp) __NOP
#define __debug_info_LOG(exp,PREFIX,fmt,...) __NOP
#define __ASSERT_LOG(exp,fmt,...) __NOP
#define __ERROR_LOG(exp,fmt,...) __NOP
#define __BEFORE_LOG(N,fmt,...) __NOP
#define __AFTER_LOG(N,fmt,...) __NOP

#endif
#endif
```

##### <li> do{...}while(0)
http://www.cnblogs.com/lizhenghn/p/3674430.html

1. 代码中的do{}while(0)可避免使用goto语句
2. 宏定义中的do{}while(0)可帮助定义复杂的宏以避免错误
3. 避免由空宏引起的警告
```
#define EMPTYMICRO do{}while(0)
```

4. 定义单一的函数块来完成复杂的操作
```
  如果你有一个复杂的函数，变量很多，而且你不想要增加新的函数，可以使用do{...}while(0)，将你的代码写在里面，里面可以定义变量而不用考虑变量名会同函数之前或者之后的重复。

  这种情况应该是指一个变量多处使用（但每处的意义还不同），我们可以在每个do-while中缩小作用域。
int key;
string value;
int func()
{
    int key = GetKey();
    string value = GetValue();
    dosomething for key,value;
    do{
        int key;string value;
        dosomething for this key,value;
    }while(0);
}
```

##### <li> 空语句
```
if (condition)
{
	;
}
```

##### <li>  gcc -Wl option and Link wrap option
https://gcc.gnu.org/onlinedocs/gcc-7.1.0/gcc/Link-Options.html
https://sourceware.org/binutils/docs/ld/Options.html

hogan@hogan:/tmp/chef_wrap$ gcc -o waiter_test_wrap chef.c waiter_test_wrap.c -Wl,--wrap,chef_cook -lcmocka
hogan@hogan:/tmp/chef_wrap$ gcc -o waiter_test_wrap chef.c waiter_test_wrap.c -Wl,--wrap=chef_cook -lcmocka
hogan@hogan:~/share/framework/cmocka/example/chef_wrap$ gcc -o waiter_test_wrap waiter_test_wrap.c chef.c -lcmocka -Wl,--wrap=chef_cook

```
Wl:	 	Link Options

-Wl,option

    Pass option as an option to the linker. If option contains commas, it is split into multiple options at the commas. You can use this syntax to pass an argument to the option. For example, -Wl,-Map,output.map passes -Map output.map to the linker. When using the GNU linker, you can also get the same effect with -Wl,-Map=output.map.


--wrap=symbol
    Use a wrapper function for symbol. Any undefined reference to symbol will be resolved to __wrap_symbol. Any undefined reference to __real_symbol will be resolved to symbol.

    This can be used to provide a wrapper for a system function. The wrapper function should be called __wrap_symbol. If it wishes to call the system function, it should call __real_symbol.

    Here is a trivial example:

    void *
    __wrap_malloc (size_t c)
    {
        printf ("malloc called with %zu\n", c);
        return __real_malloc (c);
    }

    If you link other code with this file using --wrap malloc, then all calls to malloc will call the function __wrap_malloc instead. The call to __real_malloc in __wrap_malloc will call the real malloc function.

    You may wish to provide a __real_malloc function as well, so that links without the --wrap option will succeed. If you do this, you should not put the definition of __real_malloc in the same file as __wrap_malloc; if you do, the assembler may resolve the call before the linker has a chance to wrap it to malloc.
```

##### <li> 大小端转换的宏
```
typedef unsigned short int uint16;
typedef unsigned long int uint32;


#define BigLittleSwap16(A)        ((((uint16)(A) & 0xff00) >> 8) | \
                                   (((uint16)(A) & 0x00ff) << 8))

#define BigLittleSwap32(A)        ((((uint32)(A) & 0xff000000) >> 24) | \
                                   (((uint32)(A) & 0x00ff0000) >> 8) | \
                                   (((uint32)(A) & 0x0000ff00) << 8) | \
                                   (((uint32)(A) & 0x000000ff) << 24))
```

##### <li> 一段代码判断大小端
```
#include <stdio.h>

//通过共用体检测CPU的大小端模式
int checkCPU()
{
    short int test = 0x1234;

    if( *((char *)&test) == 0x12 )     //低地址存放高字节, 则是大端模式
        return 1;
    else
        return 0;
}

int main( int argc, char * argv[] )
{
    /* 1 通过共用体判断大小端模式 */
    if( checkCPU() )
        printf("Big endian.\n\n");
    else
        printf("Little endian.\n\n");

    /* 2 用十六进制整型数据判断大小端模式 */
    short int a = 0x1234;
    char x0 , x1, x2;

    x0 = ( (char *)&a )[0];
    x1 = ( (char *)&a )[1];
    printf( "x0=[%c], x1=[%c]\n", x0, x1 );
    if( x0 == 0x34 && x1 == 0x12 )
        printf("Little endian.\n\n");
    else
        printf("Big endian.\n\n");

    /* 3 用字符数组判断大小端模式 */
    char b[] = "abc";
    x0 = b[0];
    x1 = b[1];
    x2 = b[2];
    printf( "x0=[%c], x1=[%c], x2=[%c]\n", x0, x1, x2 );
    if( x0 == 'a' && x1 == 'b' && x2 == 'c' )
        printf("Little endian.\n");
    else
        printf("Big endian.\n");

    return 0;
}
```

##### <li> GCC编译动态链接库
```
gcc stub.c -fPIC -shared -o libstub.so
```

##### <li> 结构体初始化
```
struct point {
	int x;
	int y;
	int z;
};

struct point p = {.x = 3, .y = 4, .z = 5};
```

##### <li> 数组名取地址
```
在C语言中，对数组名取地址，得到的地址也是数组第一个元素的地址，如果对这个地址执行+1操作，这个+1的步长是整个数组的长度。即对整个数组取地址。可以对比结构体指针理解。


Code:
    #include<stdio.h>
    int main()
    {
        int a[10];

        printf("a:/t%p/n", a);
        printf("&a:/t%p/n", &a);
        printf("a+1:/t%p/n", a+1);
        printf("&a+1:/t%p/n", &a+1);

        return 0;
    }


大家可以编译运行一下，我的输出的结果是：
Code:

    /*
    a:          0012FF20
    &a:         0012FF20
    a+1:        0012FF24
    &a+1:       0012FF48

```
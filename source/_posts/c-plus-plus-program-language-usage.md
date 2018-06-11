---
title: C++语言问题记录
date: 2018-06-11 15:45:46
tags: C&C++
---

<!-- more -->

<ol>

##### <li> 读写文件
http://www.runoob.com/cplusplus/cpp-files-streams.html
http://blog.csdn.net/kingstar158/article/details/6859379
```
到目前为止，我们已经使用了 iostream 标准库，它提供了 cin 和 cout 方法分别用于从标准输入读取流和向标准输出写入流。

本教程介绍如何从文件读取流和向文件写入流。这就需要用到 C++ 中另一个标准库 fstream，它定义了三个新的数据类型：
数据类型 	描述
ofstream 	该数据类型表示输出文件流，用于创建文件并向文件写入信息。
ifstream 	该数据类型表示输入文件流，用于从文件读取信息。
fstream 	该数据类型通常表示文件流，且同时具有 ofstream 和 ifstream 两种功能，这意味着它可以创建文件，向文件写入信息，从文件读取信息。

要在 C++ 中进行文件处理，必须在 C++ 源代码文件中包含头文件 <iostream> 和 <fstream>。
打开文件

在从文件读取信息或者向文件写入信息之前，必须先打开文件。ofstream 和 fstream 对象都可以用来打开文件进行写操作，如果只需要打开文件进行读操作，则使用 ifstream 对象。

下面是 open() 函数的标准语法，open() 函数是 fstream、ifstream 和 ofstream 对象的一个成员。

void open(const char *filename, ios::openmode mode);

在这里，open() 成员函数的第一参数指定要打开的文件的名称和位置，第二个参数定义文件被打开的模式。
模式标志 	描述
ios::app 	追加模式。所有写入都追加到文件末尾。
ios::ate 	文件打开后定位到文件末尾。
ios::in 	打开文件用于读取。
ios::out 	打开文件用于写入。
ios::trunc 	如果该文件已经存在，其内容将在打开文件之前被截断，即把文件长度设为 0。

您可以把以上两种或两种以上的模式结合使用。例如，如果您想要以写入模式打开文件，并希望截断文件，以防文件已存在，那么您可以使用下面的语法：

ofstream outfile;
outfile.open("file.dat", ios::out | ios::trunc );

类似地，您如果想要打开一个文件用于读写，可以使用下面的语法：

fstream  afile;
afile.open("file.dat", ios::out | ios::in );

关闭文件

当 C++ 程序终止时，它会自动关闭刷新所有流，释放所有分配的内存，并关闭所有打开的文件。但程序员应该养成一个好习惯，在程序终止前关闭所有打开的文件。

下面是 close() 函数的标准语法，close() 函数是 fstream、ifstream 和 ofstream 对象的一个成员。

void close();

写入文件

在 C++ 编程中，我们使用流插入运算符（ << ）向文件写入信息，就像使用该运算符输出信息到屏幕上一样。唯一不同的是，在这里您使用的是 ofstream 或 fstream 对象，而不是 cout 对象。
读取文件

在 C++ 编程中，我们使用流提取运算符（ >> ）从文件读取信息，就像使用该运算符从键盘输入信息一样。唯一不同的是，在这里您使用的是 ifstream 或 fstream 对象，而不是 cin 对象。


#include <iostream>
#include <string>
#include <fstream>

using namespace std;

int main()
{
	string str("MS/SAM/NGIS/BV-03-C");
    ofstream logfile;

    while ((pos = str.find('/')) != str.npos)
    {
        str.replace(pos, 1, "_");
    }

    string filename = str.append(".txt");

    // logfile.open(filename.c_str(), ios::app);
    logfile.open(filename.c_str(), ios::trunc);
    logfile << "hello world" << endl;
    logfile.close();

    return 0；
}
```

##### <li> error :"cout " was not declared in this scope
http://blog.csdn.net/easonleelee/article/details/16930995
http://www.jianshu.com/p/cda668a06bee
```
#include <iostream>

int main(int argc, char *argv[])
{
    std::cout << "hello world" << std::endl;
}

or

#include <iostream>

using namespace std;

int main(int argc, char *argv[])
{
     cout << "hello world" << endl;
}
```

##### <li> error: no matching function for call to 'std::basic_ifstream<char>::open(std::string&)
http://blog.csdn.net/alpine_climbing/article/details/51464358
```
原文地址：  http://blog.csdn.net/cs_zlg/article/details/8300124

[cpp] view plain copy


    string filename = "1.txt";
    ifstream fin;
    fin.open(filename);

上述语句会产生如下错误：

error: no matching function for call to 'std::basic_ifstream<char>::open(std::string&)

原因是C++的string类无法作为open的参数。

解决方案：使用C的字符串。

例：

[cpp] view plain copy


    char filename[10];
    strcpy(filename, "1.txt");
    ifstream fin;
    fin.open(filename);
```

##### <li> visual studio读写xml文件
https://support.microsoft.com/zh-cn/help/815658/how-to-read-the-xml-data-from-a-file-by-using-visual-c


##### <li> string操作与char *和CString的转换
http://blog.csdn.net/luoweifu/article/details/20232379

http://www.runoob.com/cplusplus/cpp-strings.html
http://blog.csdn.net/u010142437/article/details/30481123
http://blog.csdn.net/u011974987/article/details/52504486
http://blog.csdn.net/monkeyduck/article/details/23541073
```
    #include <iostream>
    #include <string>
    using std::cout;
    using std::endl;
    using std::string;
    int main(void){
        string str1="We can insert a string";
        string str2="a str into ";
             //在字符串指定位置前面插入指定字符串
        cout <<str1.insert(14,str2)<<endl;
        //在字符串指定位置前面插入指定字符串的子串（从指定索引开始的指定个数的字符）
        cout <<str1.insert(14,str2,2,9)<<endl;
        //插入指定字符串的前n个字符
        cout <<str1.insert(14,"test hello",5)<<endl;
        //插入n个相同字符到字符串中
        cout <<str1.insert(14,6,'*')<<endl;

        //替换指定索引开始的指定长度的子串
        cout <<str1.replace(3,3,"may")<<endl;
        //用给定字符串的指定子串来进行替换
        //如下，实际上使用的是could来进行替换
               cout <<str1.replace(3,3,"can could",4,5)<<endl;
        //使用给定字符串的前n个字符来进行替换：can
        cout <<str1.replace(3,5,"can could",3)<<endl;
        //使用指定个数的重复字符来进行替换
        cout <<str1.replace(3,3,5,'*')<<endl;

        string word="We";
        size_t index=str1.find(word);
        if(index!=string::npos)
        //删除指定索引开始的指定长度的字符
        cout <<str1.erase(index,word.length())<<endl;
        return 0;

    }


    #include <string>
    #include <iostream>
    using namespace std;
    void main()
    {
     ////find函数返回类型 size_type
    string s("1a2b3c4d5e6f7g8h9i1a2b3c4d5e6f7g8ha9i");
    string flag;
    string::size_type position;

    //find 函数 返回jk 在s 中的下标位置
    position = s.find("jk");
     if (position != s.npos)  //如果没找到，返回一个特别的标志c++中用npos表示，我这里npos取值是4294967295，
     {
      cout << "position is : " << position << endl;
     }
     else
     {
      cout << "Not found the flag" + flag;
     }
```

##### <li> c++中类对象作为参数都是值拷贝吗？
https://segmentfault.com/q/1010000004599429
```
++中参数的传递方式是值拷贝(by value)还是引用拷贝(by reference)取决于你的形参命名方式。

示例一：按值传递。

/* function declaration of transferring argument by value */
void func(string s) {
    // operates on string object s
    // note that here s is a copy of the string object you transferred in so any function-scope change will not affect invoker environment.
}

/* example usage of aforementioned function */
string str;
func(str);
// after func call, str will keep the same

示例二：按引用传递。

/* function declaration */
void func(string& s) {
    // operate on string object s
    // local change will be applied to the argument you transferred in
}

/* example usage */
string str;
func(str);
// at this time, str will be changed with the modification func() made to it

示例三：按常量引用传递（在实际的工作中，这种调用方式是最常被使用的，它可以有效减少string拷贝的内存和CPU时间消耗）。

/* function declaration */
void func(const string& s) {
    // transfer in a read-only reference of string object s
    // no copy will be made against s, neither any change allowed upon it
}

/* example usage */
string str;
func(str);
// str is not supposed to be changed after func() invoke.
```

##### <li> String处理函数
https://www.cnblogs.com/xFreedom/archive/2011/05/16/2048037.html
https://www.renfei.org/blog/introduction-to-cpp-string.html
http://www.cnblogs.com/youxin/archive/2012/06/21/2558279.html
https://www.byvoid.com/zhs/blog/cpp-string
http://www.runoob.com/cplusplus/cpp-strings.html
https://zh.wikipedia.org/wiki/String_(C%2B%2B%E6%A0%87%E5%87%86%E5%BA%93)
```
1. 截取子串
s.substr(pos, n)    截取s中从pos开始（包括0）的n个字符的子串，并返回
s.substr(pos)        截取s中从从pos开始（包括0）到末尾的所有字符的子串，并返回

2. 替换子串
s.replace(pos, n, s1)    用s1替换s中从pos开始（包括0）的n个字符的子串

3. 查找子串
s.find(s1)         查找s中第一次出现s1的位置，并返回（包括0）
s.rfind(s1)        查找s中最后次出现s1的位置，并返回（包括0）
s.find_first_of(s1)       查找在s1中任意一个字符在s中第一次出现的位置，并返回（包括0）
s.find_last_of(s1)       查找在s1中任意一个字符在s中最后一次出现的位置，并返回（包括0）
s.fin_first_not_of(s1)         查找s中第一个不属于s1中的字符的位置，并返回（包括0）
s.fin_last_not_of(s1)         查找s中最后一个不属于s1中的字符的位置，并返回（包括0）


C++ string的size()和length()函数没有区别
http://www.cnblogs.com/lakeone/p/4764577.html

 C++标准库中的string中两者的源代码如下：
  size_type   __CLR_OR_THIS_CALL   length()   const
  { //   return   length   of   sequence
  return   (_Mysize);
  }

  size_type   __CLR_OR_THIS_CALL   size()   const
  { //   return   length   of   sequence
  return   (_Mysize);
  }

所以两者没有区别。

length是因为沿用C语言的习惯而保留下来的，string类最初只有length，引入STL之后，为了兼容又加入了size，它是作为STL容器的属性存在的，便于符合STL的接口规则，以便用于STL的算法。

string类的size()/length()方法返回的是字节数，不管是否有汉字。
```

##### <li> CString, LPCWSTR, string, char *等字符串格式的互相转换
http://xionghuilin.com/?p=621
https://www.kancloud.cn/wangshubo1989/string/100983
https://social.msdn.microsoft.com/Forums/vstudio/en-US/901f3217-f667-485b-9bd8-83d6f7fe89d4/how-to-convert-lpcwstr-to-string
http://www.cnblogs.com/foolboy/archive/2005/07/25/199869.html
https://stackoverflow.com/questions/5271461/vc-how-to-convert-a-cstring-into-lpcwstr
https://stackoverflow.com/questions/27220/how-to-convert-stdstring-to-lpcwstr-in-c-unicode
https://blackfs.blogspot.jp/2015/01/convert-stdstring-to-lpcwstr-in-c.html
http://wiki.jikexueyuan.com/project/visual-studio/1.html
http://blog.csdn.net/ezhou_liukai/article/details/13779091
```
CString to string (unicode)
// CString to string
#if 0
		// http://forums.codeguru.com/showthread.php?231155-C-String-How-to-convert-between-CString-and-std-string
		CT2CA tempTestCase(testcase);
		std::string casename(tempTestCase);
#else
		// https://www.codeproject.com/Tips/175043/Cplusplus-Converting-an-MFC-CString-to-a-std-str
		// https://msdn.microsoft.com/en-us/library/awkwbzyc.aspx
		// https://stackoverflow.com/questions/258050/how-to-convert-cstring-and-stdstring-stdwstring-to-each-other
		std::string casename = CW2A(testcase.GetString());
#endif

        CString nodeText((char*)(_bstr_t)pXmlNode->text);
        pixitParamNameStr = CW2A(nodeText.GetString());


CString to char *(unicode)
		// https://social.msdn.microsoft.com/Forums/vstudio/en-US/38c0e07f-853b-45da-aed4-c2ab6972daca/convert-cstring-to-char?forum=vcgeneral
		// http://www.voidcn.com/article/p-ntawqvcn-ox.html
		// http://blog.csdn.net/neverup_/article/details/5664733
		// http://blog.sina.com.cn/s/blog_43eb83b90100gcub.html
		// http://blog.sina.com.cn/s/blog_625eda0b0101a9ii.html
		// http://www.cnblogs.com/junyuz/archive/2011/08/24/2151857.html

		CString nodeText((char*)(_bstr_t)pXmlNode->text);

		wchar_t* wCharString = nodeText.GetBuffer(nodeText.GetLength()+1);
		size_t origsize = wcslen(wCharString) + 1;
		size_t convertedChars = 0;
		char *ncharStr = NULL;
		ncharStr = (char *)malloc(origsize);
		memset(ncharStr, 0, origsize);
		wcstombs_s(&convertedChars, ncharStr, origsize, wCharString , _TRUNCATE);

		sscanf_s(ncharStr, "%x", cmdValue);


string to LPCWSTR(unicode)
// https://stackoverflow.com/questions/27220/how-to-convert-stdstring-to-lpcwstr-in-c-unicode
std::wstring s2ws(const std::string & s)
{
	int len;
	int slength = (int)s.length() + 1;
	len = MultiByteToWideChar(CP_ACP, 0, s.c_str(), slength, 0, 0);
	wchar_t* buf = new wchar_t[len];
	MultiByteToWideChar(CP_ACP, 0, s.c_str(), slength, buf, len);
	std::wstring r(buf);
	delete[] buf;
	return r;
}

	std::string projectName;

	LPCWSTR pszProjectName;
	LPCWSTR pszParamName;
	LPCWSTR pszNewParamValue;

#if 1
    // UNICODE mode
    // https://blackfs.blogspot.jp/2015/01/convert-stdstring-to-lpcwstr-in-c.html
    stemp = s2ws(projectName); // Temporary buffer is required
    pszProjectName = stemp.c_str();
#else
    pszProjectName = projectName.c_str();
#endif


LPCWSTR to string(unicode)
	std::string sDescStr;
	unsigned int cmdValue = 0;
	std::string sValType;

	CString cDescStr(pszDescription);
	wchar_t* wCharString = cDescStr.GetBuffer(cDescStr.GetLength()+1);
	size_t origsize = wcslen(wCharString) + 1;
	size_t convertedChars = 0;
	char *ncharStr = NULL;
	ncharStr = (char *)malloc(origsize);
	memset(ncharStr, 0, origsize);
	wcstombs_s(&convertedChars, ncharStr, origsize, wCharString , _TRUNCATE);

	sDescStr = std::string(ncharStr);
```

##### <li> string to LPCWSTR(C++ unicode)
https://social.msdn.microsoft.com/Forums/fr-FR/0f749fd8-8a43-4580-b54b-fbf964d68375/convert-stdstring-to-lpcwstr-best-way-in-c?forum=Vsexpressvc
http://blackfs.blogspot.jp/2015/01/convert-stdstring-to-lpcwstr-in-c.html
https://stackoverflow.com/questions/27220/how-to-convert-stdstring-to-lpcwstr-in-c-unicode
http://www.cplusplus.com/forum/windows/33029/
```
std::wstring s2ws(const std::string& s)
{
 int len;
 int slength = (int)s.length() + 1;
 len = MultiByteToWideChar(CP_ACP, 0, s.c_str(), slength, 0, 0);
 wchar_t* buf = new wchar_t[len];
 MultiByteToWideChar(CP_ACP, 0, s.c_str(), slength, buf, len);
 std::wstring r(buf);
 delete[] buf;
 return r;
}

std::string s;

#ifdef UNICODE
std::wstring stemp = s2ws(s); // Temporary buffer is required
LPCWSTR result = stemp.c_str();
#else
LPCWSTR result = s.c_str();
#endif


std::wstring s2ws(const std::string& s)
{
    int len;
    int slength = (int)s.length() + 1;
    len = MultiByteToWideChar(CP_ACP, 0, s.c_str(), slength, 0, 0);
    wchar_t* buf = new wchar_t[len];
    MultiByteToWideChar(CP_ACP, 0, s.c_str(), slength, buf, len);
    std::wstring r(buf);
    delete[] buf;
    return r;
}

std::wstring stemp = s2ws(myString);
LPCWSTR result = stemp.c_str();
```

##### <li> unsigned char and signed char区别
http://bbs.chinaunix.net/thread-4291073-1-1.html
https://ask.helplib.com/c++/post_864391
http://www.cnblogs.com/qytan36/archive/2010/09/27/1836569.html
```
pixel_data 是 vector的。

当我做的时候 printf(" 0x%1x", pixel_data[0] ) 我希望看到 0xf5 。

但我得到 0xfffffff5，就好像我正在打印 4字节整数而不是 1字节。

为什么我给了 printf 一个 char 来打印- 它只有 1字节，所以为什么 printf 打印 4？

printf: 实现被封装在第三方API中，但只是想知道这是否是标准 printf的特性？


你可能得到一种良性的未定义的行为,因为 %x 修饰符预计 unsigned int 参数和 char 通常会被提升到一个 int 当传递给 varargs函数。

你应该显式地将char转换为 unsigned int 以获得可以预测的结果：

printf(" 0x%1x", (unsigned)pixel_data[0] );

请注意，一个的宽度不是非常有用。 它只指定要显示的最小位数，在任何情况下都需要至少一个数字。

char 在你的平台上签名时，这里转换将把负 char 值转换为大的unsigned int 值( 比如 。 fffffff5 )。如果你想治疗时就零扩展字节值作为无符号值转换为 pixel_dataunsigned int 你应该使用 unsigned char, 或通过 unsigned char 演员或者使用屏蔽操作后推广。

printf(" 0x%x", (unsigned)(unsigned char)pixel_data[0] );

或者

printf(" 0x%x", (unsigned)pixel_data[0] & 0xffU );
```

##### <li> string比较
http://bbs.csdn.net/topics/40135334
https://www.cnblogs.com/xFreedom/archive/2011/05/16/2048037.html
```
if (0 == sValType.compare("O"))
if (0 == sValType.compare(sValTypeTemp))

http://blog.csdn.net/wisdom605768292/article/details/12076375

string t1 = "helloWorld";
string t2 = "helloWorld";

if (t1 == t2)
{
    printf("***t1 ,t2 是一样的\n");
    printf("这是正确的\n");
}

if (t1.c_str() == t2.c_str())
{
    printf("@@@t1 ,t2 是一样的\n");
}

if (strcmp(t1.c_str(),t2.c_str()) == 0)
{
    printf("###t1 ,t2 是一样的\n");
    printf("这是正确的\n");
}
```

##### <li> Vector使用
http://blog.csdn.net/hancunai0017/article/details/7032383
```
	vector(向量): C++中的一种数据结构,确切的说是一个类.它相当于一个动态的数组,当程序员无法知道自己需要的数组的规模多大时,用其来解决问题可以达到最大节约空间的目的.

用法:

1.文件包含:

首先在程序开头处加上#include<vector>以包含所需要的类文件vector

还有一定要加上using namespace std;


2.变量声明:

   2.1 例:声明一个int向量以替代一维的数组:vector <int> a;(等于声明了一个int数组a[],大小没有指定,可以动态的向里面添加删除)。

   2.2 例:用vector代替二维数组.其实只要声明一个一维数组向量即可,而一个数组的名字其实代表的是它的首地址,所以只要声明一个地址的向量即可,即:vector <int *> a.同理想用向量代替三维数组也是一样,vector <int**>a;再往上面依此类推.


3.具体的用法以及函数调用:

3.1 如何得到向量中的元素?其用法和数组一样:

例如:

vector <int *> a

int b = 5;

a.push_back(b);//该函数下面有详解

cout<<a[0];       //输出结果为5

1.push_back   在数组的最后添加一个数据
2.pop_back    去掉数组的最后一个数据
3.at                得到编号位置的数据
4.begin           得到数组头的指针
5.end             得到数组的最后一个单元+1的指针
6．front        得到数组头的引用
7.back            得到数组的最后一个单元的引用
8.max_size     得到vector最大可以是多大
9.capacity       当前vector分配的大小
10.size           当前使用数据的大小
11.resize         改变当前使用数据的大小，如果它比当前使用的大，者填充默认值
12.reserve      改变当前vecotr所分配空间的大小
13.erase         删除指针指向的数据项
14.clear          清空当前的vector
15.rbegin        将vector反转后的开始指针返回(其实就是原来的end-1)
16.rend          将vector反转构的结束指针返回(其实就是原来的begin-1)
17.empty        判断vector是否为空
18.swap         与另一个vector交换数据
```

##### <li> C++值传递，引用传递和指针传递
http://blog.csdn.net/shhdgl/article/details/50212237
http://www.cnblogs.com/skyseraph/archive/2010/10/25/1860032.html
http://blog.csdn.net/whzhaochao/article/details/12891329
http://www.cnblogs.com/yanlingyin/archive/2011/12/07/2278961.html
https://www.zhihu.com/question/20632080
```
/*
功能：学习 C++ 值传递、引用传递、指针传递
时间：2015/12/7
参考：http://blog.csdn.net/lby978232/article/details/8105688
     http://www.cnblogs.com/skyseraph/archive/2010/10/25/1860032.html
*/


#include <iostream>
#include <stdlib.h>
using namespace std;
//值传递
void swap1(int x,int y)
{
    int temp;
    temp=x;
    x=y;
    y=temp;
    cout<<"do swap1：\t"<<x<<" * "<<y<< "\t值传递" << endl;
}

//引用传递
void swap2(int &x,int &y)
{
    int temp;
    temp=x;
    x=y;
    y=temp;
    cout<<"do swap2\t"<<x<<" * "<<y<< "\t引用传递" << endl;
}

//指针传递：改变指针的间接引用
void swap3(int *x,int *y)
{
    int temp;
    temp=*x;
    *x=*y;
    *y=temp;
    cout<<"do swap3\t"<<*x<<" * "<<*y<< "\t指针传递：改变指针的间接引用" << endl;
}

//指针传递：改变指针本身
void swap4(int *x,int *y)
{
    int *temp;
    temp=x;
    x=y;
    y=temp;
    cout<<"do swap4\t"<<*x<<" * "<<*y<< "\t指针传递：改变指针本身" << endl;
}
int main(int argc, char *argv[])
{
    int a=5,b=10;
    cout<<"before do swap   "<<a<<" * "<<b<<endl;
    swap1(a,b);
    cout<<"after do swap    "<<a<<" * "<<b<<endl;
    cout<<"---------------------------------------------------"<<endl;
    a=5,b=10;
    cout<<"before do swap   "<<a<<" * "<<b<<endl;
    swap2(a,b);
    cout<<"after do swap    "<<a<<" * "<<b<<endl;
    cout<<"---------------------------------------------------"<<endl;
    a=5,b=10;
    cout<<"before do swap   "<<a<<" * "<<b<<endl;
    swap3(&a,&b);
    cout<<"after do swap    "<<a<<" * "<<b<<endl;
    cout<<"---------------------------------------------------"<<endl;
    a=5,b=10;
    cout<<"before do swap   "<<a<<" * "<<b<<endl;
    swap4(&a,&b);
    cout<<"after do swap    "<<a<<" * "<<b<<endl;
    system("PAUSE");
    return 0;
}

一：值传递

//值传递
void swap1(int x,int y)
{
    int temp;
    temp=x;
    x=y;
    y=temp;
    cout<<"do swap1：\t"<<x<<" * "<<y<< "\t值传递" << endl;
}

原因：swap1(int x, int y)函数采用值传递的方式，传入的实参实际上是a和b的副本而非其本身，所以对副本的改变并不会反应到a和b本身上。

二：引用传递

//引用传递
void swap2(int &x,int &y)
{
    int temp;
    temp=x;
    x=y;
    y=temp;
    cout<<"do swap2\t"<<x<<" * "<<y<< "\t引用传递" << endl;
}

原因：swap2(int x, int y)函数采用引用传递的方式，传入的实参实际上是a和b的引用，对引用的改变会直接反应到a和b本身上。

三：指针传递

    改变指针的间接引用

//指针传递：改变指针的间接引用
void swap3(int *x,int *y)
{
    int temp;
    temp=*x;
    *x=*y;
    *y=temp;
    cout<<"do swap3\t"<<*x<<" * "<<*y<< "\t指针传递：改变指针的间接引用" << endl;
}

调用方法：swap3(&a, &b) ;
原因：swap3(int x, int y)函数采用指针传递的方式，传入的实参虽然也是a和b的指针的副本，但是改变的是副本的间接引用，无论是指针本身还是其副本，都指向相同的值，所以这个改变会反应到a和b本身上。

    改变指针的间接引用

//指针传递：改变指针本身
void swap4(int *x,int *y)
{
    int *temp;
    temp=x;
    x=y;
    y=temp;
    cout<<"do swap4\t"<<*x<<" * "<<*y<< "\t指针传递：改变指针本身" << endl;
}

调用方法：swap4(&a, &b) ;
输出结果：

原因：swap4(int x, int y)函数采用指针传递的方式，传入的实参实际上是a和b的指针的副本，而且改变的是副本本身而非其间接引用，所以不会影响的指针所指向的值，即a和b本身上。


 1 #include<iostream>
 2 using namespace std;
 3 //值传递
 4  void change1(int n){
 5     cout<<"值传递--函数操作地址"<<&n<<endl;         //显示的是拷贝的地址而不是源地址
 6     n++;
 7 }
 8
 9 //引用传递
10 void change2(int & n){
11     cout<<"引用传递--函数操作地址"<<&n<<endl;
12     n++;
13 }
14  //指针传递
15 void change3(int *n){
16      cout<<"指针传递--函数操作地址 "<<n<<endl;
17     *n=*n+1;
18  }
19 int     main(){
20     int n=10;
21     cout<<"实参的地址"<<&n<<endl;
22     change1(n);
23     cout<<"after change1() n="<<n<<endl;
24     change2(n);
25     cout<<"after change2() n="<<n<<endl;
26     change3(&n);
27     cout<<"after change3() n="<<n<<endl;
28     return true;
29 }


无论你传值还是传指针，函数都会生成一个临时变量， 但传引用时，不会生成临时变量，


你可以把引用当做语法糖，但传引用主要是它不生成临时变量，不进行返回值copy等，速度快。


以下来自Google C++ Style Guide:All parameters passed by reference must be labeled const.来自: http://google-styleguide.googlecode.com/svn/trunk/cppguide.xml#Reference_Arguments
这样也就有了一些使用倾向，当参数不希望被修改时，使用引用+const；当有可能要修改时，使用指针。


在 C 语言中，所有的参数传递都是值传递，所以如果你需要在一个函数中改变函数外变量值，你需要把函数的参数声明为指针（全局变量另当别论）。但是在 C++ 中存在传递引用，它也可以用来改变变量值。此外引用也同时消除了拷贝对象带来的开销。

既然传递指针和引用都能到达到同样的效果，那么函数声明的时候应该使用引用呢还是指针呢？
More Effective C++ 一书的总结

这本书的第一条就是区分指针和引用。它们两者之间的最大区别是引用必须指向某个对象而指针可以是NULL，此外引用一旦指定不能更改而指针可以。

这两个区别点导致引用有更加安全和高效的特性，但是指针却有无可比拟的灵活性。大部分人出于安全性的考虑会推荐使用引用，这其实也是它设计的主要目的，但是如果你想要灵活的设计，大部分时候你只能选用指针，比如设计模式种的大部分设计都是使用指针而不是使用引用。引用在参数传递的时候用得多一些，而类内部的组合中可能会使用指针来提高设计的灵活性（毕竟一旦设定就无法改变对于灵活性来说是个灾难）。
```

##### <li> CString与LPCWSTR、LPSTR、char*、LPWSTR等类型的转换
http://blog.csdn.net/sl159/article/details/6412171

##### <li> C++ Debug Reference
```
2018.01.05 update

strcpy, strncpy, strncpy_s
http://zh.cppreference.com/w/c/string/byte/strncpy
http://blog.csdn.net/xin_yu_xin/article/details/51577008
http://blog.csdn.net/geekvc/article/details/22578215


unsigned char and signed char
http://bbs.chinaunix.net/thread-4291073-1-1.html
https://ask.helplib.com/c++/post_864391
http://www.cnblogs.com/qytan36/archive/2010/09/27/1836569.html


std::cout and printf
http://blog.csdn.net/witnessai1/article/details/47658283
https://www.cnblogs.com/devymex/archive/2010/09/06/1818754.html


string
https://www.cnblogs.com/xFreedom/archive/2011/05/16/2048037.html
https://www.renfei.org/blog/introduction-to-cpp-string.html
http://www.cnblogs.com/youxin/archive/2012/06/21/2558279.html


string, LPCWSTR, CString
http://xionghuilin.com/?p=621
https://www.kancloud.cn/wangshubo1989/string/100983
https://social.msdn.microsoft.com/Forums/vstudio/en-US/901f3217-f667-485b-9bd8-83d6f7fe89d4/how-to-convert-lpcwstr-to-string
http://www.cnblogs.com/foolboy/archive/2005/07/25/199869.html
https://stackoverflow.com/questions/5271461/vc-how-to-convert-a-cstring-into-lpcwstr
https://stackoverflow.com/questions/27220/how-to-convert-stdstring-to-lpcwstr-in-c-unicode
https://blackfs.blogspot.jp/2015/01/convert-stdstring-to-lpcwstr-in-c.html
http://wiki.jikexueyuan.com/project/visual-studio/1.html
http://blog.csdn.net/ezhou_liukai/article/details/13779091


MSXML2
https://www.bbsmax.com/A/n2d9GR4JDv/
http://www.cnblogs.com/xuandi/p/5719295.html
http://blog.csdn.net/dongdan_002/article/details/41348985
https://msdn.microsoft.com/en-us/library/ms766702(v=vs.85).aspx


2018.01.22 update

char * to string
https://stackoverflow.com/questions/1195675/convert-a-char-to-stdstring


string对象的方法
http://blog.csdn.net/ezhou_liukai/article/details/13779091
http://blog.csdn.net/qq_35040828/article/details/65445241
http://blog.csdn.net/monkeyduck/article/details/23541073
https://www.cnblogs.com/web100/archive/2012/12/02/cpp-string-find-npos.html
http://en.cppreference.com/w/cpp/string/basic_string/size
https://zh.wikipedia.org/wiki/String_(C%2B%2B%E6%A0%87%E5%87%86%E5%BA%93)
https://www.renfei.org/blog/introduction-to-cpp-string.html
https://www.cnblogs.com/xFreedom/archive/2011/05/16/2048037.html


integer to string
http://www.cppblog.com/forLinda/archive/2006/03/17/4298.html
http://www.cnblogs.com/lshguang89/archive/2008/06/09/1216334.html


sprintf
http://www.cnblogs.com/jeekun/archive/2013/01/15/2862051.html


char to wchar
http://www.cnitblog.com/textbox/archive/2010/03/16/64672.aspx
http://www.voidcn.com/article/p-pspenxdm-bcy.html
http://blog.csdn.net/github_35160620/article/details/53687757
https://github.com/isocpp/CppCoreGuidelines/issues/829
https://social.msdn.microsoft.com/Forums/vstudio/en-US/54ea02f7-02df-4726-8fb7-c3660db30739/convert-char-to-wchart?forum=vcgeneral
http://blog.csdn.net/u010476094/article/details/74545823
https://www.codeproject.com/Questions/172037/Convert-char-to-wchar
https://stackoverflow.com/questions/3074776/how-to-convert-char-array-to-wchar-t-array
https://stackoverflow.com/questions/8032080/how-to-convert-char-to-wchar-t


visual studio configure utf-8
http://blog.csdn.net/stelalala/article/details/9635817


cout
http://blog.csdn.net/xijiaoda_liuhao/article/details/8807742
https://www.cnblogs.com/devymex/archive/2010/09/06/1818754.html
```

##### <li> C++ Library API reference
http://en.cppreference.com/w/cpp/string/basic_string/size
http://www.cplusplus.com/reference/string/string/compare/
http://www.howsoftworks.net/cplusplus.api/std/string_compare.html

##### <li> Win32串口编程
http://blog.csdn.net/czc1009/article/details/17118971
http://blog.csdn.net/lingtianyulong/article/details/8477130
http://blog.csdn.net/ypist/article/details/8793037
http://blog.csdn.net/bingcaihuang/article/details/5668474
http://blog.csdn.net/changyourmind/article/details/52161096
http://blog.csdn.net/u013232740/article/details/49871113
http://blog.csdn.net/cancan8538/article/details/7329092
http://www.go-gddq.com/down/2011-06/11060523185438.pdf
http://www.tk4479.net/CaroTong/article/details/41347281

COM10以上串口
http://blog.csdn.net/playboy1/article/details/48316263
http://blog.csdn.net/ccing/article/details/6234050

##### <li> C++正则表达式
https://msdn.microsoft.com/zh-cn/library/bb982727.aspx
http://www.cnblogs.com/pmars/archive/2012/10/24/2736831.html
http://www.cnblogs.com/ittinybird/p/4853532.html
http://blog.csdn.net/mycwq/article/details/18838151

##### <li> strcpy, strncpy, strncpy_s
http://zh.cppreference.com/w/c/string/byte/strncpy
http://blog.csdn.net/xin_yu_xin/article/details/51577008
http://blog.csdn.net/geekvc/article/details/22578215

##### <li> std::cout与printf
std::cout and printf
http://blog.csdn.net/witnessai1/article/details/47658283
https://www.cnblogs.com/devymex/archive/2010/09/06/1818754.html

##### <li> C++操作xml文件
https://www.bbsmax.com/A/n2d9GR4JDv/
https://msdn.microsoft.com/en-us/library/ms756987(v=vs.85).aspx
http://blog.csdn.net/cds27/article/details/5545455
http://www.cnblogs.com/xuandi/p/5719295.html
http://blog.csdn.net/dongdan_002/article/details/41348985
https://msdn.microsoft.com/en-us/library/ms766702(v=vs.85).aspx

##### <li> Win32 API reference
https://stackoverflow.com/questions/4701193/download-windows-api-reference-msdn-for-offline-use
http://laurencejackson.com/win32/
https://www.microsoft.com/zh-CN/download/details.aspx?id=20955

##### <li> 面向对象基本知识
http://coredumper.cn/index.php/2017/05/21/c_plus_plus_booklist/

http://www.cnblogs.com/lrh-xl/p/5252156.html
http://blog.csdn.net/hankai1024/article/details/7948376
http://blog.csdn.net/hankai1024/article/details/7947989

http://www.runoob.com/cplusplus/cpp-static-members.html
http://www.runoob.com/cplusplus/cpp-class-access-modifiers.html
http://www.runoob.com/cplusplus/assignment-operators-overloading.html
https://www.w3cschool.cn/cpp/cpp-polymorphism.html

http://www.cnblogs.com/qlwy/archive/2011/08/25/2153584.html
http://blog.csdn.net/junlon2006/article/details/53066660
http://blog.sina.com.cn/s/blog_5c5bc9070100xmuk.html
http://blog.csdn.net/morewindows/article/details/6721430

http://blog.csdn.net/qsyzb/article/details/9896543
http://blog.csdn.net/gaoxuelin/article/details/9766619

https://www.zhihu.com/question/34018632
https://www.zhihu.com/question/26911239
http://blog.csdn.net/gatieme/article/details/17589981
http://blog.csdn.net/KingCat666/article/details/45048385
http://blog.csdn.net/wuha0/article/details/7084136
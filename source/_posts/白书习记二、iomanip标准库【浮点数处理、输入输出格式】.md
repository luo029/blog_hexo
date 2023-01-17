---
title: 白书习记二、iomanip标准库【浮点数处理、输入输出格式】
abbrlink: 6b47c55d
date: 2021-01-02 05:19:00
---
What's past is prologue.

<!--more--><br>
在输出浮点数小数位数的时候，上baidu搜索发现的一个标准库。（一共也不认识几个来着）
<br>
<br>

> iomanip，在C++程序里面经常见到下面的头文件#include
>
> <iomanip>，io代表输入输出，manip是manipulator（操纵器）的缩写(在c++上只能通过输入缩写才有效）。
<br>
<br>

功能：
---

> 用来对输入输出操作的格式进行更加方便的控制，在ios_base基类的基础上将每一种格式的设置和删除都进行了函数级的同名封装，提供了全局的调用接口函数，支持在运算符“<<”和“>>”上的多次使用，配合ios_base实例的控制。是I/O流控制头文件，就像C里面的格式化输出一样。
> 如果在一次输出过程中需要混杂多种格式，使用ios_base的成员函数来处理就显得很不方便。STL另提供了iomanip库可以满足这种使用方式。
<br>
<br>

接口
--

<br>
    setbase(n)
    设置整数为n进制(n=8,10,16)
    
    setfill(n)
    设置字符填充，c可以是字符常或字符变量
    
    setprecision(n)
    设置浮点数的有效数字为n位
    
    setw(n)
    设置字段宽度为n位
    
    setiosflags(ios::fixed)
    设置浮点数以固定的小数位数显示
    
    setiosflags(ios::scientific)
    设置浮点数以科学计数法表示
    
    setiosflags(ios::left)
    输出左对齐
    
    setiosflags(ios::right)
    输出右对齐
    
    setiosflags(ios::skipws)
    忽略前导空格
<br>
> 上述接口与ios_base的格式控制成员是对应的，可以二者配合进行输出格式的精准控制。其中的精度控制默认是6位有效数字，科学计数法中的指数部分e为默认小写。setw设置的宽度如果小于字段宽度会失效
<br>

实例
--
<br>
    #include <iostream>  
    #include <iomanip>      
    using namespace std;
    int main()
    {  
        double PI=3.141592654;  
        cout<<PI<<endl;  
        cout<<setprecision(2)<<PI<<endl;  
        cout<<fixed<<setprecision(2)<<PI<<endl;   
        cout<<setfill('*')<<setw(20)<<setprecision(10)<<PI<<endl;  
        cout<<setfill('*')<<setw(20)<<setprecision(10)<<left<<PI<<endl;  
        cout<<scientific<<setprecision(10)<<PI<<endl;  
        cout<<scientific<<uppercase<<setprecision(10)<<PI<<endl;    
        return 0 ;  
    }  
    输出结果如下：
    3.141592654 
    3.1 
    3.14
    *******3.1415926540 
    3.1415926540******* 
    3.1415926540e+000 
    3.1415926540E+000
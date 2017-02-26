---
layout: post
title: 深入理解计算机系统--第二章(信息的表示和处理)
date: 2017-02-1
categories: 
tags: [记录]
description: 深入理解计算机系统--第二章(信息的表示和处理)
---
###此系列为读<深入理解计算机系统>的笔记,如有理解错误,望请指正.


##第二章 信息的表示和处理

###现代计算机存储和处理信息是以二进制信号表示,这些微不足道的二进制数字,或称为位(bit)奠定了数字革命的基础

####**2.1 信息存储**
> ####大多数计算机使用的8位的块,或者字节(byte),作为最小的可寻址的存储器单位,而不是存储器中访问单独的位.

> ####机器级程序将存储器视为一个非常大的字节数组,称为虚拟存储器.

> ####存储器的每个字节都由一个唯一的数字来标识,称为它的地址,所有可能地址的集合称为虚拟地址空间.

> ####虚拟地址空间只是一个展现给机器级程序的概念性映像.

####**2.1.1 十六进制表示法**
> ####一个字节由8位组成.二进制表示法中值域是00000000(下角标2)~11111111(下角标2)十六进制使用数字'0'~'9'以及字符'A'~'F'来表示16个可能的值.一个字节的值域为00(下角标16)~FF(下角标16).

####**2.1.2 字**
> ####每台计算机都有一个字长,指明整数和指针数据标称大小.虚拟地址是以一个字来编码的,字长决定的最重要的系统参数就是虚拟地址空间的最大大小,大多数计算机的字长都是32位.64位机器正在普遍起来.

####**2.1.3 数据大小**
>####计算机和编译器支持多种不同方式的编码数字格式.如:整数,浮点数以及其他长度的数字.

####**2.1.4 寻址和字节顺序**
>对于跨越多字节的程序对象,我们必须建立两个规则:
>
> - 1,对象的地址是什么
> - 2,如何排列这些字节

>在几乎所有的机器上,多字节对象都被存储为连续的字节序列,对象地址为所使用字节中最小的地址.

####**2.1.5 表示字符串**
>每个字符都由某个标准编码来表示,最常见的是ASCII字符码.

>ASCII字符集适合编码英文文档.

>基本编码也称为Unicode的"统一字符集",使用32位来表示字符.

>Java编程语言使用Unicode来表示字符串.对于C语言也有支持Unicode的程序库.</font>

####**2.1.6 表示代码**
>不同的机器类型使用不同的且不兼容的指令和编码方式.

>即使处理器一样,运行的系统不一样,也有不同的处理编码的规则,因此二进制代码是不兼容的.

>二进制代码很少能在不同机器和操作系统组合之间移植.

>计算机系统的一个基本概念,就是从机器角度来看,程序仅仅只是字节序列.机器没有关于初始源程序的任何信息,除了可能有些用来帮助调试的辅助表以外.


####**2.1.7 布尔代数简介**
> 二进制值是计算机编码、存储和操作的核心,所以围绕数值0和1的研究已经演化出了丰富的数学知识体系.

> 最简单的布尔代数是在二元集合{0,1}基础上的定义.

####**2.1.8 C语言中的位级运算**
> C语言一个很有用的特性就是它支持按位布尔运算.

> C语言所使用:|就是OR(或),&就是AND(与),~就是NOT(取反),^就是EXCLUSIVE~OR(异或).

> 确定一个位级表达式的结果的最好的方式,就是将十六进制的参数扩展成二进制表示并执行二进制运算,然后转回十六进制.

####**2.1.9 C语言中的逻辑运算.**
> C语言还提供了一组逻辑运算符||(OR)、&&(AND)和!(NOT)

####**2.1.10 C语言中的移位运算**
> C语言还提供了一组移位运算,以便向左或向右移动位模式.右移运算X>>K,左移运算X<<K



####**2.2 整数表示**
> 我们描述用位来编码证书的两种不同的方式:
> 
> 一种只能表示非负数,另一种能够表示负数、零和正数.

####**2.2.1 整型数据类型**
>C语言支持多种整型数据类型-----表示有限范围的整数.
>
>每种类型都能用关键字来指定大小,如:char、short、long或者long long.
>
>不同大小的分配的字节数会根据机器的字长和编译器有所不同.
>
>根据字节分配,不同的大小所能表示的值的范围是不同的.

####**2.2.2 无符号数的编码**
> 无符号的二进制表示有一个很重要的属性,就是每个介于0~2^w-1之间的数都有唯一一个w位的编码值.

####**2.2.3 补码编码**
>最常见的有符号数的计算机表示方式就是补码形式.
>
>在这个定义中,将字的最高有效位解释为负权.
>
>每个介于-2^(w-1)和2^w-1之间的整数都有一个唯一长度为w的位向量二进制表示.

####**2.2.4 有符号数和无符号数之间的转换**
> C语言允许在各种不同的数字数据类型之间做强制类型转换.

####**2.2.5 C语言中的有符号数与无符号数**
> C语言支持所有整型数据类型的有符号和无符号运算.
>
> C语言标注没有指定有符号数要采用某种表示,但是几乎所有的机器都使用补码.
>
> C语言允许无符号数和有符号数之间的转换.转换的原则是底层的位表示保持不变.

####**2.2.6 扩展一个数字的位表示**
> 一种常见的运算是在不同字长的整数之间转换,同时又保持数值不变.

####**2.2.7 截断数字**
> 假设我们不用额外的位来扩展一个数值,而是减少表示一个数字的位数.
>
> 在一台典型32位机器上,当把int X强制类型转换为short时,我们就将32位的int截断为16位的short int.
>
> 这个16位的位模式就是-12345的补码表示.
>
> 当把它强制转换回int时,符号扩展把高16位设置为1,从而生成-12345的32位补码表示.

####**2.2.8 关于有符号与无符号的建议**
>有符号数和无符号数的隐式强制类型转换导致某些非直观的行为

>这些非直观的特性经常导致程序错误,并且隐式强制类型转换细微差别的错误呀不易察觉.

>强制类型转换在代码没有明确指示下发生,程序员经常忽视了它的影响.

####**2.3 整数运算**

>许多刚入门的程序员非常惊奇的发现,两个正数相加会得出一个负数,并且比较表达式x < y和比较表达式x-y<0会产生不同的结果.这些属性是由于计算机运算的有限性造成的.理解计算机的细微之处有助于程序员编写更可靠的代码.

> - 2.3.1 无符号加法
> - 2.3.2 补码加法
> - 2.3.3 补码的非
> - 2.3.4 无符号乘法
> - 2.3.5 补码乘法
> - 2.3.6 乘以常数
> - 2.3.7 除以2的幂

####**2.3.8 关于整数运算的最后思考**

> 正如我们看到的.计算机执行"整数"运算实际上是一种模运算形式.表示数字的有限字长限制了可能的值的取值范围.结果运算可能溢出.我们看到,补码表示提供了一种既能表示负数也能表示正数的灵活方式,同时使用了与执行无符号算术相同的位级实现,这些运算包括加法、减法、乘法,甚至除法.无论运算数是以无符号形式还是以补码形式表示的.都有完全一样或者非常类似的位级行为.

####**2.4 浮点数**

> 浮点数表示对有理数进行编码,它对执行非常大的数字,非常接近于0的数字,以及更普遍地作为实数运算的近似值的计算,是很有用的.

> - 2.4.1 二进制小数
> - 2.4.2 IEEE浮点表示
> - 2.4.3 数字示列
> - 2.4.4 舍入
> - 2.4.5 浮点运算
> - 2.4.6 C语言中的浮点数

####**2.5 小结**

> 计算机将信息按位编码,通常组织成字节序列.用不同的编码方式表示整数,实数和字符串.不同的计算机模型在编码数字和多字节数据中的字节排序时使用不同的约定.

> C语言的设计可以包容多种不同字长和数字编码的实现.虽然高端机器逐渐开始使用64位字长,但是目前大多数机器仍使用32位字长.大多数机器对整数使用补码编码,而对浮点数使用IEEE浮点编码.在位级上理解这些编码,并且理解算术运算的数学特性,对于想使编写程序能在全部数值范围上正确运算的程序员来说,是很重要的.

> 在相同长度的无符号和有符号整数之间进行强制类型转换时,大多数C语言实现遵循的原则是底层位模式不变.

> 由于编码的长度有限,与传统整数和实数运算相比,计算机运算具有完全不同的属性.当超出表示范围时,有限长度能够引起数值溢出.当浮点数非常接近于0.0,从而转换成零时,也会下溢.

> 必须非常小心地使用浮点运算,因为浮点运算只有有限的范围和精度,而且不遵守普遍的算术属性,比如结合性.



####**个人记录:**

> 由于本章涉及大量的数学公式和算法,无法一一进行记录,并且有很多似懂非懂的知识点,但是在学习和记录的过程中,还是学到了很多知识,当记录时又回重新看一遍,重新思考一遍,每次看都会有不同的理解,会一点点的加深印象,以前不太懂的,也在记录的过程中重新思考.因为很多知识并没有深入的研究和学习过,读起来还是有些吃力,但学习的过程总归是痛并快乐着的.记录下来,没事的时候可以翻翻,也可以在哪里懂了之后再次加深印象.

>学习的过程很枯燥,但是也很快乐.个人能力有限,如有理解错误,请君指正,不胜感谢...
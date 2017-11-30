---
layout: post
title: 'pack/unpack详解'
date: 2017-11-30
author: wutong
tags:  php
---

有的时候想把数据打包成按字节传递，比如一些基于TCP/UDP的应用，当接收到的数据
包按照规定格式组装的时候，这个时候pack/unpack就能派上用场了。

## pack函数的用途

> Pack data into binary string

官方文档的描述是“将数据放入到二进制字符串中”。

简单的描述就是：**将每种不同类型的数据（字符串、数字等）转换成二进制字符串并串接在一起**。

## unpack函数的用途

> Unpack data from binary string
> array unpack ( string $format , string $data )

从一个二进制数据中解包，其 $format 参数跟 pack函数的$format参数一样


## pack函数的参数

> string pack ( string $format [, mixed $args [, mixed $... ]] )

#### \$format
\$format 的参数代表了以何种方式将对应的 \$args 的参数值转换成二进制字符串。

*请注意上面的 “对应” 文字，每个 \$format 代码都有对应的 \$args 参数，按顺序对应*

根据文档的描述，在 \$format 使用诸如 “a,A,h,H” 代码的时候，后面可以加一个长度，这个长度代表了对对应的 \$args 参数的前多少字节来进行转换，如果长度为2，则对 \$args 参数前2个字节进行转换，后面忽略。如果长度为"*"，则对对应的 \$args 参数所有字节进行转换

**\$format 有如下参数：**

| 代码 | 描述 |
| --- | --- |
| a | NUL-padded string |
| A | SPACE-padded string |
| h | Hex string, low nibble first |
| H | Hex string, high nibble first |
| c | signed char |
| C | unsigned char |
| s | signed short (always 16 bit, machine byte order) |
| S | unsigned short (always 16 bit, machine byte order) |
| n | unsigned short (always 16 bit, big endian byte order) |
| v | unsigned short (always 16 bit, little endian byte order) |
| i | signed integer (machine dependent size and byte order) |
| I | unsigned integer (machine dependent size and byte order) |
| l | signed long (always 32 bit, machine byte order) |
| L | unsigned long (always 32 bit, machine byte order) |
| N | unsigned long (always 32 bit, big endian byte order) |
| V | unsigned long (always 32 bit, little endian byte order) |
| q | signed long long (always 64 bit, machine byte order) |
| Q | unsigned long long (always 64 bit, machine byte order) |
| J | unsigned long long (always 64 bit, big endian byte order) |
| P | unsigned long long (always 64 bit, little endian byte order) |
| f | float (machine dependent size and representation) |
| g | float (machine dependent size, little endian byte order) |
| G | float (machine dependent size, big endian byte order) |
| d | double (machine dependent size and representation) |
| e | double (machine dependent size, little endian byte order) |
| E | double (machine dependent size, big endian byte order) |
| x | NUL byte |
| X | Back up one byte |
| Z | NUL-padded string (new in PHP 5.5) |
| @ | NUL-fill to absolute position |

#### \$args 

这是一个不限制数量的参数列表，每个参数都要被转换成二进制字符串，可以使用不同类型的数据，如：字符串、数字

## pack函数的用法

\$format 的参数代码不同，转换出来的数据也不同，所以这里我依次讲解不同的 \$format 参数代码如何使用。


#### 代码："a”

官方的说明是：

> NUL-padded string

简单的来说就是将 \$args 当做字符来转换（可以对照ASCII表），那为什么描述上说是 “用NUL来填充“？后面会讲到的。

**为了方便，后面出现的转换结果都用16进制来表示，请知悉**。

常规转换：

```php
pack("a","w");
// 将 "w" 这个字符转换成二进制字符串，直接对照ASCII码表就晓得了
// 对应的二进制字符串的16进制就是：0x77
```

带长度的转换：

```php
pack("a3","abcde");
// 根据文档说明，我们知道只要转换 "abcde" 的前3个字节
// 对照ASCII表得知其转换结果是：0x61 0x62 0x63
```

带长度但是参数值字节长度不够的转换：

```php
pack("a8","abcde");
// 根据文档说明，我们要把 "abcde" 字符串来当做8个字节来转换
// 但是参数值的长度不够怎么办，根据文档说明
// PHP会把不够的字节转换成NUL(解答了上面的疑问)
// 所以对照ASCII表得知其最终转换结果是：
// 0x61 0x62 0x63 0x64 0x65 0x00 0x00 0x00 
```

参数不是字符而是数值型的转换：

```php
pack('a',61);
// 对于10进制的参数而言，直接当做字符处理，即：pack('a',"61");
// 对不是10进制的参数要先转换成10进制
// 转换1个字节，所以ASCII字符6的转换后的结果就是：0x36

pack('a',0x61);
// 即：pack('a','97');
// 结果： 0x39
```


#### 代码："A"

跟 "a" 代码的区别就是，参数值长度不够的话则以空格代替。

```php
pack("A8","abcde");
// 结果：0x61 0x62 0x63 0x64 0x65 0x20 0x20 0x20 
```


#### 代码："h"

官方文档说明：

> Hex string, low nibble first

16进制字符串，低半字节在前。

就是说当做一个16进制符串来处理，我们知道1个字节用16进制来表示的话就是2个16进制字符，如：A3。低半字节在前的意思就是说这个16进制的后4位在前。

常规转换：

```php
pack("h2","A3");
// 读取2个字节当做16进制处理，A是高位，3是低位
// 转换要求是，低位在前，所以结果就是：0x3A

pack("h","A3");
// 读取一个字节当做16进制，不满1个字节后面补0（很奇怪为什么不是前面补0）
// 或者可以理解为不满一个字节则不转换
// A是高位，0是低位，低位在前，结果：0x0A

pack("h3","A3B");
// 结果：0x3A 0x0B
```

数值型转换：

```php
pack("h2",13);
// 跟上面的“a”代码运算方式一样，结果：0x31

pack("h3",0x159);
// 即：pack("h3","345")
// 结果：0x43 0x05
```


#### 代码："H"

跟 "h" 代码的区别就是高半字节在前，不再解释



#### 代码："c" 和 "C"

char类型，范围 -255-255，感觉没有什么差别，超过范围的话则从头算起，如果提供的不是数值则保存 0x00

#### 代码："s" 和 "S"

int类型，只不过是16位的，既范围： -65535-65535，字节序由机器决定

```php
pack("s2",2400,72300);
// 结果 0x60096C1A
// 可以得知我的机器是按照小端来的
// 72300 超过最大范围所以减去 65536 在进行转换
```

#### 代码："n" 和 "v"

同 s 和 S 一样，只不过是无符号的，并且字节序分别变成了 大端 和 小端


#### 代码 "i I l L N V q Q J P"

同上面差不多，只不过字节序、符号类型、长度有所不同

#### 代码 "f" "g" "G"

f，浮点型，有效范围根据机器决定（一般4个字节），字节序根据机器决定

g，浮点型，有效范围根据机器决定（一般4个字节），字节序 小端

G，浮点型，有效范围根据机器决定（一般4个字节），字节序 大端


```php
pack("f",3.1415926);
// 结果 0xDA0F4940

pack("g",3.1415926);
// 结果 0xDA0F4940

pack("G",3.1415926);
// 结果 0x40490FDA
```

#### 代码 "d" "e" "E"

d，双精度浮点型，有效范围根据机器决定（一般8个字节），字节序根据机器决定

e，双精度浮点型，有效范围根据机器决定（一般8个字节），字节序 小端

E，双精度浮点型，有效范围根据机器决定（一般8个字节），字节序 大端


```php
pack("d",3.1415926);
// 结果 0x4AD8124DFB210940

pack("e",3.1415926);
// 结果 0x4AD8124DFB210940

pack("E",3.1415926);
// 结果 0x400921FB4D12D84A
```

#### 代码 "x"

填充1个空字节，即：0x00

```php
pack("x");
// 结果 0x00
pack("xx");
// 结果 0x0000
```

#### 代码 "X"

删除前面1个字节

```php
pack("a4X","haha");
// 结果 0x0686168
```

#### 代码 "Z"

跟 a 差不多，只不过最后一个字节用 0x00填充

```php
pack("a4Z4","lala","haha");
// 结果 0x6C616C6168616800
```

#### 代码 "@"

取之前的打包数据的数据，如 @3，则取之前打包数据的3个字节，如果不提供位置参数则取1个字节

```php
pack("a4a2@","abcdef","ghijklmn");
// 结果 0x61
pack("a4a2@6","abcdef","ghijklmn");
// 结果 0x616263646768
```


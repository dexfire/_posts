---
title: '[C++]C++中字符串格式化的几种方法'
categories: [C++]
tags: [C++]
date: 2020-05-27 00:29:34
keywords:
description:
photos: /img/4d13e10460727926.jpg
---

# {{ post.title }}

1. 使用snprintf格式化字符串
2. 使用boost::format格式化字符串
3. 使用stringstream格式化字符串

## 具体示例
1.  **使用`snprintf`格式化字符串**

```cpp
#include <stdio.h>
using std::string;
// 准备数据
string haha("haha");
int num = 3;
// 准备格式
string fmt("test string: %s. test number: %d");
char targetString[1024];
// 格式化，并获取最终需要的字符串
int realLen = snprintf(targetString, sizeof(targetString),
							fmt.c_str(), haha.c_str(), num);

```

> **参考链接**：[http://www.cplusplus.com/reference/cstdio/snprintf/](http://www.cplusplus.com/reference/cstdio/snprintf/)

2.  **使用`boost::format`格式化字符串**

```cpp
#include "boost/format.hpp"
// 准备数据
string haha("haha");
int num = 3;
// 准备格式
boost::format fmt("test string: %s. test number: %d");
// 格式化
fmt % haha % num;
// 获取最终需要的字符串
string targetString = fmt.str();

```

> **参考链接**：[https://www.boost.org/doc/libs/1\_70\_0/libs/format/example/sample\_formats.cpp](https://www.boost.org/doc/libs/1_70_0/libs/format/example/sample_formats.cpp)

3.  **使用`stringstream`格式化字符串**

```cpp
#include <sstream>
using std::stringstream;
// 准备数据
string haha("haha");
int num = 3;
// 准备根据格式造字符串流
stringstream fmt;                       /* 或者使用 ostringstream */
// 造字符串流
fmt << "test string: " << haha << ". test number: " << num;
// 获取最终需要的字符串
string targetString = fmt.str();

```

> **参考链接**：[http://www.cplusplus.com/reference/ostream/ostream/operator<</](http://www.cplusplus.com/reference/ostream/ostream/operator%3C%3C/)

## string char*互相转换

### 1\. string to char\*

*   [方式1](https://stackoverflow.com/a/42308974/9288778)

```cpp
std::string str = "string";
char* chr = const_cast<char*>(str.c_str())

```

*   [方式2](https://stackoverflow.com/a/16502000)

```cpp
string str = "some string" ;
char *cstr = &str[0];

```

*   [方式3](https://stackoverflow.com/a/7352131/9288778)

```cpp
std::string str = "string";
const char *cstr = str.c_str();

```

Note that it returns a `const char *`; you aren’t allowed to change the C\-style string returned by `c_str()`. If you want to process it you’ll have to copy it first:

```cpp
std::string str = "string";
char *cstr = new char[str.length() + 1];
strcpy(cstr, str.c_str());
// do stuff
delete [] cstr;

```

Or in modern C++:

```cpp
std::vector<char> cstr(str.c_str(), str.c_str() + str.size() + 1);
// use &chars[0] as a char*

```

### 2\. char\* to string

方式1：直接赋值：

```cpp
char c[] = "this is a char array";
const char* t = "const char";
string s = t;
string ss = c;

```

方式2：[https://stackoverflow.com/questions/8438686/convert\-char\-to\-string\-c](https://stackoverflow.com/questions/8438686/convert-char-to-string-c)

同理`const char*`转`string`：

```cpp
const char* cc = "this is a const exp";
string s(cc, cc + strlen(cc));

```

### 3\. char\* 和const char\*

```cpp
const char* src = "this is a const exp";
char* ch = const_cast<char*>(src);
const char* dst = static_cast<const char*>(ch);
cout << ch << endl;
cout << dst << endl;
```

---

theme.post.author: {{ theme.post.author }}
---
layout: post
title: "模仿 Google Test 单元测试框架"
date:   2020-9-25 8:00:00 +0800
---

# 谷歌单元测试框架

# 2020/7/14

学习内容：

1. 单元测试框架的编写与实现，单元测试框架属于测试的一部分，验证程序的某一部分逻辑是否正确。

2. 模仿google test模块的方式，在文件中加入多个TEST函数，然后调用RUN_ALL_TESTS函数就可以执行所有的TEST函数，并且返回结果；

3. TEST函数其实并不是真正意义上的一个函数，而是通过宏定义实现的一个文件头。因为多个TEST函数存在于同一个文件中肯定是不符合c语言的语法的。

   通过以下代码定义TEST

   ``` c
   #define TEST(a, b) void a_##_b()  //定义了一个函数头
   #define EXPECT(a, comp ,b) {\
   	if (!((a) comp (b))) { \
   		test_func_flag = 1; \		//用于标记测试是否出错，全局变量
   		expect_printf(__FILE__, __LINE__, "(" #a ") " #comp " (" #b ")"); \
   	}  \
   }
   #define EXPECT_EQ(a, b) EXPECT(a, ==, b);		//这里使用了一个技巧
   #define EXPECT_NE(a, b) EXPECT(a, !=, b);
   
   //但是这样我们不知道有几个测试用例，如何执行测试用例
   //使用attribute注册函数使函数先于main函数执行
   //将TEST(a, b)改为如下
   #define TEST(a, b) \
   void a##_##b();\		//这一句是声明这个测试函数，不然在注册函数时会出现未声明
   __attribute__((constructor)) \  //先于main函数执行
   void add_##a##_##b() {  \
       add_func(a##_##b, #a "." #b); \
   }\
   void a##_##b()			//原来的函数头放在了这里
     
   //接下来实现一些接口函数和结构
   struct Func_Data {
       void (*func)();
       const char *func_name;
   } func_arr[100];		//真正的工程中是不可以用一个固定大小的数组的
   int func_cnt;  
   
   void add_func(void (*func)(), const char *func_name) {
       func_arr[func_cnt].func = func;
       func_arr[func_cnt].func_name = func_name;
       func_cnt++;
       return;		//礼貌性的返回
   }
   
   int test_func_flag;
   
   void expect_printf(const char *file, int line_on, const char *msg) {
       printf(YELLOW"  %s:%d : Failure\n", file, line_on);
       printf(YELLOW"    Expected: %s\n"NONE, msg);
       return;
   }
   
   int RUN_ALL_TEST() {
       printf(GREEN"[==========]"NONE" Running %d tests\n", func_cnt);
       for (int i = 0; i < func_cnt; i++) {
           printf(GREEN"[   RUN     ] %s\n", func_arr[i].func_name);
           test_func_flag = 0;
           int b = clock();
           func_arr[i].func();
           int e = clock();
           if (test_func_flag) {
               printf(RED"[   FAILED  ]\n"NONE);
           } else {
               printf(GREEN"[      OK   ]\n"NONE);
           }
           printf(" %s (%s ms)\n", func[i].func_name, 1000 * (e - b) / CLOCK_PER_SEC);
       }
       return 0;
   }
   
   
   //将测试函数封装在testcasen.h中
   #ifdef DEBUG
   	#include "testcase.h"
   #endif
   //...
   #ifdef DEBUG
   	return RUN_ALL_TESTS();
   #else
   	return 0;
   #endif
   
   //makefile 的编写
   release:
   debug:  -DDEBUG
   ```

## 最终实现的效果

![](https://img2020.cnblogs.com/blog/1851975/202007/1851975-20200715175857263-842327273.png)

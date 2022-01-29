title: C 标准库
description: C 标准库
categories:
  - C
author: Jade
date: 2021-11-25 19:36:00
---

## 标准输入输出 <stdio.h>
stdio standard input and output

stdin 标准输入
stdout 标准输出
stderr 标准错误输出

|函数|功能|
|-|-|
|int getchar(void)|从标准输入（一般是键盘）中一次读取一个字符|
|int putchar(int)|将字符送至标准输出上|
|int printf(char *format, arg1, ...)|格式化输出|
|int scanf(char *format, ...)|格式化输入|
|int sscanf(char *string, char *format, arg1, ...)|从一个字符串中读取字符序列|
|FILE *fopen(char *name, char *mode)|打开文件|
|int getc(FILE *fp)|从文件中返回下一个字符|
|int putc(int c, FILE *fp)|将字符写入文件中|
|int fscanf(FILE *fp, char *format,...)|文件格式化输入|
|int fprintf(FILE *fp, char *format,...)|文件格式化输出|
|int fclose(FILE *fp)|关闭文件
|int feeor(FILE *fp)|流中出现错误，返回非零值|
|int feof(FILE *fp)|到达文件结尾，返回非零值|
|char *fgets(char *line, int maxline, FILE *fp)|从文件中读取下一个输入行，并放在字符数组中|
|int fput(char *line, FILE *fp)|将字符串写入到文件中|

## 字符串操作 <string.h>

|函数|功能|
|-|-|
|strcat(char *s, char *t)|将t指向的字符串连接到s指向的字符串的末尾|
|strncat(char *s, char *t, int n)|将t指向的字符串中前n个字符连接到s指向的字符串的末尾|
|strcmp(char *s, char *t)|比较字符串大小|
|strncmp(char *s, char *t, int n)|比较字符串前n个字符大小|
|strcpy(char *s, char *t)|将t指向的字符串复制到s指向的位置|
|strlen(char *s)|返回s指向的字符串的长度|
|strchr(char *s, int c)|在s指向的字符串中查找c，返回第一次出现的位置的指针|
|strrchr(char *s, int c)|在s指向的字符串中查找c，返回最后一次出现的位置的指针|

## 字符操作 <ctype.h>
isalpha
isupper
islower
isdigit
isalnum
isspace
toupper
tolower

## 通用 <stdlib.h>
atof
malloc
calloc
free
exit
system
frand

## 数学函数 <math.h>
sin
cos
atan2
exp
log
log10
pow
sqrt
fabs


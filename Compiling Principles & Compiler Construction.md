---
title: Compiling Principles & Compiler Construction
author: Hanxinhu
---

[TOC]

# 1 引论

compiler

source code -> compiler -> target code



interpreter



e.g. 1.1 java 

java -> bytecode 字节码 虚拟机对字节码加以解释执行



preprocessor assembler linker loader

## 1.2 编译器 结构

映射 -》 分析 和 综合

analysis 组成要素 语法结构  ->  源程序的中间表示。

信息存放在符号表 symbol table

综合 synthesis 根据 中间表示 和 符号表 构建 目标程序



字符流 -> 词法分析器 -> 符号流 语法分析 语法树 中间代码生成器 中间表示形式 机器无关代码优化器 中间表示形式 代码生成器 目标机器语言 机器相关代码优化器 目标机器语言

### 1.2.1 词法分析

lexical analysis 或 scanning

读入字符流 组织成有意义的词素 lexeme 

对于每个词素参数 词法单元token 作为输出 <token-name, attribute-name>

token-name:语法分析步骤使用的抽象符号

attribute-name: 符号表中关于词法单元的条目

`position = initial + rate * 60`

1. position -> <id, 1> id是标识符identifier的抽象符号 1指向符号表中position对应的条目。条目应存放 与标识符有关的信息，比如名字 类型
2.  赋值符号 = -> 词法单元 <=>
3. initial -> <id,2>

`<id,1> <=> <id,2> <+><id,3><*><60>`

### 1.2.2 语法分析

syntax analysis 或 解析 parsing

语法树 syntax tree 节点表示运算，结点的子节点表示运算的分量

### 1.2.3 语义分析

语义分析器 semantic analyzer 使用语法树和符号表中的信息检查源程序是否和语言定义的语义一致。 同时也收集类型信息。

类型检查 type checking 检查运算符是否具有匹配的运算分量。 比如数组的下标必须整数

自动类型转换 coercion 比如 Int to float

### 1.2.4 中间代码生成

低级的类机器语言的中间表示

三地址代码 three-addrerss code

### 1.2.5 代码优化

改进中间代码 生成更好的目标代码


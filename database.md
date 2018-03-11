# database

[TOC]

## chapter1 Introduction

### terminology 专业术语

Database Management  System 数据库管理系统

Database 数据库

Intranet 内网



C/S架构 数据库和DBMS运行在数据库服务器中，数据库应用程序运行在客户机中，通过局域网实现数据访问

B/S架构 数据库和DBMS运行在数据库服务器中，数据库应用程序运行在应用服务器（web服务器） 用户客户端只需要安装浏览器，负责接收用户输入和结果展示

pseudocode 伪代码

prototype 原型

### Data Model

* Hierarchical Data Model 层次数据模型 

  a directed tree 有向树

  different kinds of records relate to one another in a hierarchical form

* Network Data Model 网状数据模型

    a directed graph without circuits

   a  generalization of the hierarchical model where a set of records in one layer might have two different containing hierarchies at the next layer up

* Relational Model 关系模型   (Object_Relational Model)

* Object-Orinted Model 面对对象模型 (Object_Relational Model)

### History of Database Systems

* Relational Model 关系模型

  our data will look like tables

* Relational Database

  all information is represented in the form of named tables with labeled columns

* Relational DBMS

**first normal form rule:** in the relational model, a column of a table must contain a single, unstructured value.

## chapter 2 The Relation Model

* Data Model 数据模型
  1. is a set of definitions describing how real-world data is conceptually represented as computerized information
  2. It also describes the types of operation available to access and update this information
* Relation Model
* Object-Relational Model

**Terminology**

* Table (relation) Old: file of records
* Column names(Attributes) Old: field names of records
* Rows(Tuples) Old: records of a file
* Table heading(Schema) Old: set of attributes

| 关系模型         | 关系数据库管理系统（SQL)   | 文件系统            |
| ------------ | ---------------- | --------------- |
| Relation 关系  | Table 表          | File of Records |
| Attribute 属性 | Column 列         | Field           |
| Tuple 元组     | Row 行            | Record          |
| Schema 模式    | Table Heading 表头 | Type of Record  |

**Definition**

* database. a set of named tables, or relations.
* Heading of table(schema) a set of named columns

**Note**

* the number of rows changes frequentlty and rows are not remembered by users
* the columns usually DON'T change in number, many names are remembered, and USED TO POSE QUERIES

**Program-Data Independece** 数据独立性

when asked to make up a query to answer a question, query must still answer the question even if all the data changes.



Column type(Domain, Datatype) : A table is DECLARED in SQL. Columns have certain TYPES as in SQL : integer, char,date..



Problems of Column type(cont.)

1. **Integrity 完整性** Most commercial database systems don't support types consisting of enumerated(枚举) sets
2. **particular type ** 可以创建一个自定义类型 Domain vs Domain



**Relational Algebra 关系代数**

Domain of column is like an enumerated type

Domain(City) All the city names in the U.S.



**Cartesian Product**笛卡尔乘积

set： CID = Domain(cid) CNAME = Domain(cname) 

then consider cid * cname consisting of all tuples (x,y) x in cid y in cname

A relation between these four domains is a subset of the Cartesian products Í

A \subset cid x cname




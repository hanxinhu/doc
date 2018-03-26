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

- [database](#database)
  - [chapter1 Introduction](#chapter1-introduction)
    - [terminology 专业术语](#terminology-%E4%B8%93%E4%B8%9A%E6%9C%AF%E8%AF%AD)
    - [Data Model](#data-model)
    - [History of Database Systems](#history-of-database-systems)
  - [chapter 2 The Relation Model](#chapter-2-the-relation-model)
    - [2.3 Relational Rules](#23-relational-rules)
    - [keys Superkeys and NUll Values](#keys-superkeys-and-null-values)
      - [key & superkey](#key-superkey)
      - [table key](#table-key)
      - [Every table T has at least one key](#every-table-t-has-at-least-one-key)
      - [Null Values](#null-values)

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

### 2.3 Relational Rules

* Rule 1. First Normal Form Rule 第一范式  **Can't have multi-valued attributes(repeating fields.) or have any internal structure(record).**

1. could create one table with duplicates on different rows but this is bad for other reasons 不知道有多少列 各个元组所需要的列数不同，会造成空间浪费
2. ends up meaning we have to create two tables and join them in later queries.
3. in OR model, it's OK, but won't handle this for a while so as not to confuse you. assume relational no multi-valued fields

* Rule 2. **Access Rows By Content Only Rule**只能根据内容访问（取某一元组）
  1. can't say the third row down from the top. no order to the rows and the columns
  2. disallows pointers to rows e.g. row IDs or "refs" 
  3. Most relational products break this rule by allowing users to get at rows by RIDs
  4. new object-relational products have refs as part of syntax

  **implies**:
  1. no order to rows and columns
* Rule 3. The Unique Row Rule 元组的唯一性
  1. two rows can't be same in all attributes at once. So that a relation is an unordered SET of tuples
  2. but many products allow this for efficiency
  3. **we will assume that all these rules hold perfectly**
### keys Superkeys and NUll Values
* **idea of keys**: some set of columns in a table distinguishes rows
* defined by DBA which set of column has this property
* It is USEFUL to have such a key for a table. other table can refer to a row in this table
#### key & superkey
superkey : a set of columns that has uniqueness property 
e.g. id,name. only id matters
key : is a minimal superkey: no subset of columns also has uniqueness.e.g. id
#### table key
Given a table T, with Head(T) = {$A_1,A_2,A_3....A_n$} A key for table T, sometimes called a candidate key, is a set of attributes. K = {$A_{i1},....A_{ik}$},,with two properties:
#### Every table T has at least one key

#### Null Values
Null unknown
* A null value is placed in a field of a table when a specific value is either unknown or inappropriate
* a null value can be used for either a numeric or character type.BUT IT HAS a different VALUE FROM ANY REAL FIELD. It's not zero or null string
* be handled specially by commercial databases

**RULE 3 Entity Integrity Rule**实体完整性
No Column belonging to a primary key of a table T is allowed to take on NULL values for any row in T

与Rule 3 等价

### 2.5 Relational Algebra

abstract language 

information stored in the form of tables $\implies$ results of a query in table form

two types of operations:

* set-theoretic operations. depend on fact that table is a set of rows

* native relational operations. depend on structure of table

  | NAME          | SYMBOL | FORM      | EXAMPLE |
  | ------------- | :----: | --------- | ------- |
  | UNION(并)      |   ∪    | UNION     | R U S   |
  | INTERSECTION交 |   ∩    | INTERSECT | R ∩ S   |
  | DIFFERENCE 差  |   -    | MINUS     | R - S   |
  | PRODUCT 乘积    |   ×    | TIMES     | R × S   |

native relational operations

| NAME             | SYMBOL             | FORM                    | EXAMPLE                                           |
| ---------------- | ------------------ | ----------------------- | ------------------------------------------------- |
| PROJECT(投影)    | R[] $\pi$          | R[]                     | R[$A_{i1},...,A_{Aik}$]<br>$\pi_{Ai1,....Aik}(R)$ |
| SELECT(选择)     | R where C $\delta$ | R where C $\delta_c(R)$ | R where $A_1 = 5$ $\delta_{A1}(R)$                |
| JOIN（连接）     |                    | JOIN                    |                                                   |
| DIVISION（除法） | ÷                  | DIVIDEBY                | R ÷ S                                             |



#### Compatible Tables

* Table R and S are *compatible* if they have the same headings
* if Head(R) = Head(S) , with attributes chosen from the same domains and with the same meaning


**In relational algebra, two columns are said to have the same meanings if they have the same name of column**



only in two *compatible* tables, set-theoretic operations make sense.

### 2.6

Def 2.6.3 Assignment, Alias**

Table R: R(A1,A2...,An)

赋值运算 S(B1,B2,..,Bn) = R(A1,A2,...,An)

define a new table S, and Domain(Bi) = Domain(Ai) for all i (1 <= i <= n)

可以利用赋值运算创建临时的中间关系

* 可以利用已有的关系创建中间关系
* 可以用一个关系代数表达式的计算结果创建中间关系
* 中间关系有关系名 并且可以定义新的属性名和调整属性的排列次序



**def 2.6.4 Rroduct  x**

the product of the tables R and S is a table T that 

* if $Head(R) = {{A_1,A_2,.....,A_n}}$, $Head (S) = {B_1,B_2,....,B_n}$ then Head(T) = {$R.A_1,....R.A_n,S.B_1,......,S.B_m$}
* t is a row in T if and only if there are two rows u in R and v in S such that t(R.$A_i$) = u(Ai) for i <= i <= n and t(S.Bk) = v(Bk) for 1<=k<= m 

the number of columns in product of tables R and S is ($C_R+C_S$)

the number of rows in product of tables R and S is ($N_R × N_S$)

### 2.7 Native Relational Operations

#### 2.7.1 projection 映射 R[$A_{i1},......A_{Ik}$]

$Head(R) = \{A_1,A_2,...,An\} $

$A_{ij} \in Head(R) \space for\space all \space 1 \le j \le k$

 the projection of R on attributes Ai1,Ai2,....Aik,is a table T that Head(T) = {Ai1,....,Aik}

can be write as $\pi_{Ai1,.....Aik}(R)$

*cast out duplicate rows in the result of projection*

#### 2.7.2 Selection

S where C or $\delta_C(S)$

the rows of S that obey the selection condition C



The selection Condition C

C can be any comparison of the form $A_i \space \theta  \space Aj $ or $A_i \theta a$

Ai are attributes of S having the same domain, a is a constant from Domain(A_i) and $\theta$ is  one of the comparison operators <,>,=,>=,<=,<>

C and D are conditions.  new conditions can be writing C AND D, C OR D, NOT C

#### 2.7.3 precedence of relational operation

| Precedence | Operations       |
| ---------- | ---------------- |
| Highest    | PROJECT          |
|            | SELECT           |
|            | PRODUCT          |
|            | JOIN,DIVIEDBY    |
|            | INTERSECTION     |
|            | UNION,DIFFERENCE |
|            |                  |
| Lowest     |                  |


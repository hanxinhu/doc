# progmatic

**程序员修炼之道 读书笔记**

[TOC]

## progmatic programmer

1.早期的采纳者、快速的改编者

2. 好奇
3. 批判的思考者
4. 有现实感
5. 多才多艺
6. **care about your craft**
7. **think! about your work**

*我们，采集的只是石头，却必须时刻展望未来的大教堂*

**kaizen** 持续地做出小改进

## A pragmatic Philosophy

### 我的源码让猫给吃了

 ** 在所有的弱点中最大的弱点就是害怕弱点 **

为自己和自己的行为负责 不害怕承认无知或错误

#### 负责

provide options, don't make lame excuses

#### 软件的熵entropy

**don't live with broken windows**

**Be a catalyst for change**  请求原谅比获取许可更容易

**remember the big picture**

欲求更好，常把好事变糟 李尔王

**make quality a requirement issue**

知识上的投资总能得到最好的回报 富兰克林

知识资产knowledge portfolios

1. 严肃的投资者定期投资——作为习惯

2. 多元化是长期成功的关键

3. 聪明的投资者在保守的投资和高风险、高回报的投资之间平衡他们的资产

4. 投资者设法低买高卖，以获取最大回报

5. 应周期性地重新评估和平衡资产

   定期投资 多元化 管理风险 低买高卖 重新评估和平衡

   **invest regularly in your knowledge portfolio**

   *suggestions*

   1. 每年至少学习一种新的语言

   2. 每季度阅读一本技术书籍

   3. 也要阅读非技术书籍

   4. 上课

   5. 参加本地用户组织

   6. 试验不同的环境

   7. 跟上潮流

   8. 上网

      **把找到答案视为对个人的挑战**

**critically analyze what you read and hear**

*被打量比被忽略要好*

1. 知道自己想说什么
2. 了解你的听众

```markdown
#wisdom 离合诗 了解听众
what do you want them to learn
what is their interest in what you've got to say
how sophisticated are they
how much detail they want
whom do you want to own the information
how can you motivate them to listen to you	

```



 3.   选择时机

 4.  让文档美观

 5.  让听众参与

     **It's both what you say and the way you say it**

## a pragmatic approach

**DRY don't repeat yourself**

在可能的情况下，应该总是使用访问器accessor函数读写对象的属性，使得未来增加功能更容易

**make it easy to reuse**

正交性 不相依赖性或是解耦性

当任何系统的各组件相互高度依赖时，就不再有局部修正local fix这样的事情

**eliminate effects between unrelated things**

self-contained 自足的组件 独立、具有单一、良好定义的目的	 内聚 cohesion

**不要依赖无法控制的事物属性**



面向切面编程Aspect-Oriented Programming,AOP

AOP使得在一个地方表达原本会分散在源码各处的某种行为

如日志、安全

不影响原有的代码



编码

1. 让代码保持解耦 law of demeter

2. 避免使用全局数据 全局数据都是有害的

3. 避免编写相似的函数 strategy

   **养成不断地批判对待自己的代码的习惯，寻找任何重新组织、以改善其结构和正交性的机会 重构 refactoring**

*如果某个想法是你唯一的想法，再没有什么比这更危险的事情了*

可撤销性	

**there are no final decision**

###曳光弹

*在黑暗中发光的代码*

**use tracer bullets to find the target**

1. 用户能够及早看到能工作的东西
2. 开发者构建了一个他们能在其中工作的结构
3. 有了一个集成平台
4. 有了可用于演示的东西
5. 能够感受到工作进展

应该制作原型的事物

* 架构
* 已有系统中的新功能
* 外部数据的结构或内容
* 第三方工具或组件
* 性能问题
* 用户界面设计

**prototype to learn**为了学习而制作原型

构建原型时可以忽略的细节

* **正确性** 适当的地方使用虚设的数据
* **完整性** 只能在非常有限的地方工作
* 健壮性
* 风格



*语言的限界就是一个人的世界的界限*

**program close to the problem**



**Estimate to avoid surprises**



1. 检查需求
2. 分析风险
3. 设计、实现、集成
4. 向用户确认



**use a single editor well**



*进步远非由变化组成，而是取决于好记性，不能记住过去的人，被判重复过去*



**always use source code control**

**fix the problem,not the blame**

**Don't panic**



再现bug

**std isn't broken**

**don't assume it Prove it**



**learn a text manipulation language**



**write code that writes code**



## pragmatic paranoia

**you can't write perfect software**

*当每个人都确实要对你不利时，偏执就是一个好主意*

**design by contracts**



**crash early**

#### 断言式编程

在自责中有一种满足感，当我们责备自己时，会觉的没有人有权责备我们

**if it can't happen, use assert to ensure that it won't **



**use exceptions for exceptional problems**



**finish what you start**



**minimize coupling between modules**



#### 源程序设计

configure,Don't Integrate	

用元数据metadata描述应用的配置选项，用户偏好，安装目录等

​	

元元素是任何对应用进行描述的数据——应用该怎么运行，应该使用什么资源

**put abstractions in code,details in metadata**

for example 

**Enterprise Java Beans**

#### 时间耦合

temporal coupling

并发 次序

##### 工作流

同一时间可能发生什么 以及什么必须一严格的次序发生

UML活动图

**Analyze workflow to improve concurrency**

**design using services**

#### 观察者模式

#### MVC

**Separate Views from Models**

example 

Java TreeView

#### 黑板

JavaSpace T Space

**Use Blackboards to Coordinate Workflow**

## While You Are Coding

### 靠巧合编程

* 实现的偶然

* 语境的偶然

* 隐含的假定

  *Don't Program by Coincidence*

### 深思熟虑地编程

* 意识到自己在做什么

* 不要盲目编程  （理解应用再构建） 

* 按照计划行事

* 依靠可靠的事物

* 为假定建立 **文档**

* 不要只是测试代码，还有测试假定

* 为工作划分优先级

* 不要做历史的奴隶 不要让已有的代码支配将来的代码

  #### 算法效率

  #### 重构

  ##### 何时重构

  代码不再合适 遇到绊脚石

  注意到有两样东西其实应该合并 或者其他任何错误的东西

  *不要对改动犹豫不决*

  Feature

  * 重复

  * 非正交的设计

  * 过时的知识

  * 性能

    **Refactor Early, Refactor Often**

litte tips

* 不要试图在重构的同时增加功能
* 开始重构之前，确保拥有良好的测试。尽可能经常运行，如果改动破坏了东西，就能很快知道。
* 采取短小、深思熟虑的步骤

**不要容忍破窗户**

#### 易于测试

* 单元测试

* 针对合约进行测试

  **Design to Test**

  ​

测试装备的功能

* 用以指定设置和清理的标准途径 setup and cleanup

* 用以选择个别或所有可用测试的方法

* 分析输出是否是预期（或意外）结果的手段

* 标准化的故障报告形式

  **Test Your Software， or Your Users Will**

**Don't Use Wizard Code You Don't Understand**

## Before The Project

### 需求之坑

*完美，不是在没有什么需要增加，而是在没有什么需要去掉时达到的*

**Don't Gather Requirements Dig for Them**

**Work with a User to Think Like a User**



用例 use case 目标驱动 goal -driven



用例模板

```markdown


```

需求文档 保持抽象

需求不是架构，需求不是设计，也不是用户界面，需求是**需要**

**Abstractions Live Longer than Details**



### 维护词汇表 **project glossary**

**Use a Project Glossary**

同一事物同一名称

把话说出来

将需求制作成超文本文档

**Don't Think Outside the Box** Find the box

### 一定有更容易的方法

* 有更容易的方法吗

* 你是在设法解决真正的问题，还是被外围的技术问题转移了注意力

* 这件事情为什么是一个问题

* 是什么使得它如此难以解决

* 它必须以这种方式完成吗

* 它真的必须完成吗

  ### 等你准备好

  *有时犹豫的人会得以保全*

  **Listen to Nagging Doubts -Start When You're Ready**

  倾听反复出现的疑虑，等准备好再开始

  #### 是良好的判断还是拖延

  选择一个自己觉的有困难的地方 构建原型 进行概念验证proof of concept

  记住为啥要这么做

  两种情况

  1. 觉的自己浪费时间，表明最初的勉强只是希望推迟启动。放弃原型，回到真正的开发中

  2. 随着原型取得进展，在某个时刻得到启示，突然意识到有些基本的前提错了。不仅如此，还将清楚地看到怎样纠正错误。放弃原型，投入真正的开发

     ​

### 规范陷阱

编写程序规范

**Some Things Are Better Done than Described**
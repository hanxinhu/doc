# data mining

# chapter 1

## 1.1 数据挖掘简介

​	数据挖掘旨在让计算机根据已有数据做出决策。

* 数据集
  * 表示真实世界物体的样本
  * 描述数据集中样本的特征

亲和性分析

根据样本个体（物体）之间的相似度，确定关系的亲疏



规则优劣的衡量 **支持度** **置信度**

支持度指数据集中规则应验的次数。

支持度衡量的是给定规则应验的比例

premise 前提

**置信度**衡量的是规则准确率如何，即符合给定条件（即规则的“如果”语句所表示的前提条件）的所有规则里，根当前规则结论一致的比例有多大。计算方法为，首先统计当前规则的出现次数，再用它除以条件（“如果”语句）相同的规则数量。



找出支持度最高的规则，对支持度字典进行排序。 字典中的元素默认为没有前后顺序；字典的items()函数返回包含所有元素的列表，使用itemgetter()类为键，就可以对嵌套列表进行排序。itemgetter(1)表示以字典各元素的值



##1.4 分类问题的简单实例

只关注类别（目标）这个变量





把连续值转变为类别型，这个过程叫做离散化

最简单的离散化算法，莫过于确定一个阈值，将低于该阈值的特征值设置为0，高于阈值的置为1 把某项特征的阈值设定为该特征所有特征值的均值

oneR 算法

one Rule 根据已有数据中，具有特征值相同的个体最可能属于哪个类别进行分类。 表示只选取四个特征中分类效果最好的一个用作分类依据

算法首先遍历每个特征的每一个取值，对于每一个特征值，统计它在各个类别中出现的次数，找到它出现次数最多的类别，并统计它在其他类别中出现的次数

# chapter2 用scikit-learn估计器分类

估计器 **Estimator** 用于分类、聚类和回归分析

转换器 **Transformer** 用于数据预处理和数据转换

流水线 **Pipeline** 组合数据挖掘流程，便于下次使用



## 2.1 scikit-learn 估计器

主要用于分类任务，主要包括

fit()： 训练算法，设置内部参数。该函数接受训练集及其类别两个参数

predict(): 参数为测试集。预测测试集类别，并返回一个包含测试集各条数据类别的数组。

接收和输出的数据格式均为numpy数组或类似格式

### 2.1.1 近邻算法

为了对新个体进行分类，查找训练集，找到与新个体最相似的那些个体，看看这些个体大多属于哪个类别，就把新个体分到哪个类别。

缺点：计算量大，特征取离散值的数据集表现差

### 2.1.2 距离度量

* 欧氏距离即真实距离。两个点之间的距离。正式点说，两个特征向量长度平方和的平方根。
* 曼哈顿距离。两个特征在标准坐标系中绝对轴之和（没有使用平方距离）。也叫截取距离
* 余弦距离 更适合解决异常值和数据稀疏问题。直观上讲，余弦距离是指特征向量夹角的余弦值。

### 2.1.3 加载数据集

cross_validation 可以改为 model_selection

### 2.1.5 运行算法

交叉检验

1. 将整个大数据集分成几个部分(fold) 行话为折
2. 对每一部分执行以下操作
   1. 选取其中一部分作为当前测试集
   2. 用剩余部分训练算法
   3. 在当前测试集上测试算法
3. 记录每次得分及平均得分
4. 每条数据只在测试集中出现一次，以减少运气成分

### 2.1.6 设置参数

近邻参数中最重要的参数是选取多少个近邻作为预测依据 n_neighbors

过小时，分类结果容易受到干扰，随机性强，相反，如果n_neighbors过大，实际近邻的效果将被削弱。
date: 13/12/2021

# 第1章

## 一些需要理解的术语

模型（model） 有时称为“学习器”（learner）

学习算法（learning algorithm）

数据集（data set）

示例（instance）or 样本（sample）

属性（attribute）or 特征（feature）

属性值（attribute value）

属性空间（attribute space）or 样本空间（sample space）or 输入空间

特征向量（feature vector）

学习（learning）or 训练（training）

训练数据（training data）；训练样本（training sample）；训练集（training set）

假设（hypothesis）

真相/真实（ground-truth）

预测（prediction）

标记（label）；标记空间（label space）or 输出空间

分类（classification）；二分类（binary classification）；正类（positive class） vs 反类/负类（negative class）；多分类（multi-class classification）

回归（regression）

测试（testing）；测试样本（testing sample）

clustering（聚类）；簇（cluster）

监督学习（supervised learning）：分类，回归；有label

无监督学习（unsupervised learning）：聚类；无label

泛化（generalization）

分布（distribution）D；独立同分布（independent and identically distributed / _i.i.d._)【our assumption on sample space!!】

归纳（induction）：特殊->一般 [泛化（generalization）]；归纳学习（inductive learning）

演绎（deduction）：一般->特殊 [特化（specialization）]

匹配（fit）

版本空间（version space）：针对某个假设空间有多个假设，version space是它们的集合

归纳偏好（inductive bias）：有效的机器学习算法会有它的偏好避免训练集中因有多个一致的假设而无法产生结果

奥卡姆剃刀（Occam's razor）



## Other stuff...

chapter 1主要介绍一些与机器学习相关的概念及术语，1.4 归纳偏好大致阅读。

1.4提到的“没有免费的午餐”定理（No Free Lunch Theorem）指算法的优劣取决于具体的问题，一个算法并非在所有的问题上都有一样的performance.

1.5主要关于机器学习历史。我们现在的机器学习主要是“从样例中学习”即归纳学习，其中包括符号主义学习例如决策树（decision tree; 最小化entropy）；神经网络对应的连接主义（backpropagation；black box model；手动调参；及现在的深度学习）；统计学习（statistical learning）例如支持向量机（support vector machine）与“核方法”（kernel methods）



14/12/2021-补充一些关于1.4归纳偏好不确定的想法：今天学校的machine learning课学到regularisation（Ridge regularisation/L2 & Lasso regularisation/L1)。在从同一training set产生不同complexity的function时 e.g.degree of 2/5/9...，我们会有版本空间，regularisation会对复杂的model加更多的penalty，根据features的数量选择L2 or L1。我将它们理解为归纳偏好？





# 第2章

date: 14/12/2021 - 2.1~2.3.2

## 2.1 经验误差与过拟合

错误率error rate _E = a/m_ a errors and m is the sample size；精度accuracy=1-E

误差error是预测值与真实值间的差距

通过训练，我们会得到训练误差training error/经验误差empirical error，目的是学习到数据集中的规律并得到小的泛化误差generalization error，i.e. to generalize to unseen examples。通常在未见过的数据上使用我们的model是会比在训练集上表现得差.

过拟合overfitting：死记硬背，学太好了，泛化差；not generalised；难以避免的challenges

欠拟合underfitting：没有学好训练集的规律；solution: 让model更复杂



## 2.2 评估方法

我们通过会将数据集分出训练集与测试集(unseen & 不可用于训练)，处理不同集的方法包括 留出法hold-out【直接分成training & testing】，交叉检验法cross validation（也叫k折交叉检验 k-fold cross validation）【分成k部分每一次一个部分作为testing其余的k-1作为training，重复直到所有的部分都用被用作testing set并平均它们的结果；特例：留一法leave-one-out】，自助法bootstrapping【我们想要生成一个大小为m的数据集，从原数据集抽一个数又放回去重复m次，通常在样本不够时使用，足够时会使用另外2个更多】

*注意分出训练/测试集时，要确保它们的分布一致，避免偏差（使用分层采样stratified sampling）

## 2.3 性能度量

选择model时我们会使用度量判断好坏，常用的有错误率与精度；除了它们还有查准率 查全率 F1










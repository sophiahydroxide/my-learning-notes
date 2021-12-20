# 第3章 线性模型



## 3.1 基本形式

线性模型linear model的基本形式 （d features），参数（w，b通过学习，或者w0表示b）与属性进行线性组合
$$
y(\textbf{x,w})=w_1x_1+w_2x_2+...+w_dx_d+b
$$
向量形式
$$
y(\textbf{x,w})=w^Tx+b
$$


## 3.2 线性回归Linear Regression

- 干嘛：线性回归模型预测实质

  - 多个属性的称为“多元线性回归”multivariate linear regression

- 离散属性discrete attributes【无法直接用于预测】

  - 属性值间有“序”order：转成连续值
    - Example: 1 【二值属性】转为{1.0, 0.0} 如高矮； 2 【三值属性】进一步分隔连续值为{1.0, 0.5, 0.0}
  - 不存在order：k个属性值，转为k维向量（如one-hot encoding）

- 常用性能度量：均方误差/平方误差square loss，对应常用的欧几里得距离Euclidean distance

  - 最小化均方误差求出参数w b，使得预测值尽可能接近true values【这种方法叫least square method最小二乘法,最小化data point到regression line的Euclidean distance之和】
    - 最小化的过程叫做“参数估计”parameter estimation

- 现实中可能存在的问题

  - 属性数>样例数，会导致多组解 => 归纳偏好决定
    - 常见的做法：正则化regularisation项
    - 例子：生心中基因芯片数据很多属性但是样例少

- 线性回归变式的一般形式如下（称为“广义线性模型”generalised linear model）;g()是联系函数Link function
  $$
  y=g^{-1}(\textbf{w}^T\textbf{x}+b)
  $$

  - 例子：对数线性回归log-linear regression，给左边y加上了对数
    $$
    \ln{y}=\textbf{w}^T\textbf{x}+b => y=e^{\textbf{w}^T\textbf{x}+b}
    $$



## 3.3 对数几率回归Logistic Regression

- 干嘛：二分类

- 与线性回归的不同：y->z，z转为0/1

- 优先考虑单位阶跃函数unit-step function但它非连续，则用相似的“替代函数”surrogate function
  $$
  y=\frac{1}{1+e^{-z}}=\frac{1}{1+e^{-(w^Tx+b)}}
  $$
  

- 几率odds为正例比反例，它取对数后称为对数几率log odds/logit
  $$
  odds=\frac{y}{1-y},\space log\space odds=\ln\frac{y}{1-y}
  $$

-  Logistic regression好处：不需要假设数据分布，避免分布不对的问题；概率预测

- 计算w b使用极大似然法maximum likelihood method最大化概率

  - 以Product形式将probability density function展开表示组成该数据集的概率在某参数下...
  - 对数似然Log-likelihood
  - 求偏导等于0



## 3.4 线性判别分析Linear Discriminant Analysis (LDA)

- 干嘛：分类；样例投射到一条直线，同类接近，异类的中心尽可能互相远离
  - 与ANOVA (analysis of variance) & regression analysis紧密相关
- 如何
  - 1 小化同类的协方差；2 最大化异类中心间距
  - 涉及：类内散度矩阵within-class scatter matrix；类间散度矩阵between-class scatter matrix
    - 存在多个类：全局散度矩阵
  - LDA最大化的目标：广义瑞丽商generalised Rayleigh quotient



## 3.5 多分类学习

- 原理：拆解法【多分类变多个二分类任务】
- 拆分策略
  - 一对一One vs. One
    - N(N-1)/2个二分类任务
    - 两两配对，最终结果投票
  - 一对其余One vs. Rest
    - N个二分类
    - 各classifier的预测置信度中取最大的
  - 多对多Many vs. Many
    - 某些作为正类，某些作为反类
    - 正反构造由常用的技术“纠错输出码”error correcting output codes (ECOC)挑选正反：编码与解码



## 3.6 类别不平衡class-imbalance

- 啥：不同类别的训练样例数相差大

- 怎么解决

  - 再缩放rescaling （但真实样本总体无偏采样难成立）【阈值移动threshold-moving】【即“代价敏感学习”】
    $$
    \frac{y'}{1-y'}=\frac{y}{1-y}\times\frac{m^-}{m^+}
    $$
    

  - 欠采样undersampling
    - 去除多的那类样例使正反类数量差不多
    - 问题：丢弃过多样例
    - 算法：Easy Ensemble
  - 过采样oversampling
    - 对数量少的类别增加样例使它们相差不大
    - 不可以重复采样否则可造成过拟合
    - 算法：SMOTE

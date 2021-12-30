# 第6章 支持向量机 Support Vector Machine

## 6.1 间隔与支持向量

- SVM通过划分超平面进行分类；

  - 划分以线性方程**w**^T.**x**+b=0表示，其中**w**是法向量(normal vector) 决定超平面方向，b是位移，我们可以计算样本**x**到超平面(w,b)的距离r
    $$
    r=\frac{|\textbf{w}^T\textbf{x}+b|}{||\textbf{w}||}	
    $$

  - **w**^T.**x**+b的值>= +1或-1以进行分类，而这2个直线（其实是超平面）(2d图表示的话)中间的gap的叫做“间隔”margin（即2个超平面间的距离）gamma=2/||**w**||

    - 为了更好的划分，我们需要最大化margin称“最大间隔”maximum margin=>找出合适的**w** & b
      - 最大化gamma & ||w||^-1 ->等同于最小化||**w**||^2 (**SVM基本型**)

    $$
    \gamma = \frac{2}{||\textbf{w}||}
    $$

    

  - 离超平面最近的点叫做“支持向量”support vector



## 6.2 对偶问题

- 对前面的gamma利用拉格朗日乘子法的“对偶问题”dual problem求出我们的参数**w**和b
  - 涉及数学中的二次规划问题拉格朗日乘子法
  - 最终模型只与SV有关
  - 使用二次规划会因为数据集大小而造成大开销，所以我们用Sequential Minimal Optimization (SMO)
    - SMO高效的原因：每次固定式子中拉格朗日乘子alpha_i alpha_j之外的参数，只优化它俩



## 6.3 核函数

- 基本型SVM假设线性可分，但实际中常常无法仅一个平面进行分类，映射到更高维的空间中，如果维数有限（属性数），那么在高维特征空间可分；

  - 将原来式子中的**x**以phi(**x**)表示(类似linear regression中polynomial的basis function, phi(x)仍与参数w呈线性关系)，用f(**x**)=**w**^T.**x**+b表示线性划分

    - 换到对偶问题中同理，将x换成phi(x)

    $$
    f(\textbf{x})=\textbf{w}^T\phi(\textbf{x})+b
    $$

- 由于对偶问题中计算存在不同data points在特征空间的内积，维数高的时候计算困难，使用6.22（pg127）的函数，其代替内积部分。这个函数称为”核函数“kernel function
- 在训练SVM模型时，我们有几种可用的核函数，常用的包括：线性核，多项式核，高斯核，拉普拉斯核。sigmoid核
  - 合适的核函数对于分割特征空间起很重要的作用



## 6.4 软间隔与正则化

- 硬间隔hard margin: 前面的**w**^T.**x**+b的值>= +1或-1以进行分类
- 软间隔soft margin: 现实中往往难以做到完全正确线性划分，若做到可能是过拟合，soft margin允许不能正确划分的样本存在（尽可能少）同时又最大化间隔
- 正则化regularization：降低过拟合风险，penaltise complexity
  - L0, L1倾向尽量稀疏w
    - L1适用于多数量的features，会选择特征来降低复杂度
  - L2相反
    - 不适用于features数量多



## 6.5 支持向量回归Support Vector Regression

- 在传统线性回归中预测值与真实值完全相同时损失才为0；在SVR中，所有落在间隔这条带中的损失值等于0（\epsilon-间隔带），之外的才计算偏差/损失



【这章的学习未完，数学方面还没能完全理解好做总结】




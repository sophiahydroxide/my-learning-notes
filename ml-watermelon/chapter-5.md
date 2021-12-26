# 第5章 神经网络Neural Network

## 5.1 神经网络

- 神经网络Neural network由生物神经网络启发，以神经元neuron为单位
  - 神经元中的电位达到阈值threshold/bias 处于“兴奋”状态
  - 多个带有权重的神经元连接一起汇总后与threshold比较并通过“激活函数”activation function输出
    - 常用sigmoid作为activation function，输出范围压倒[0, 1]
      - 由于非连续与不光滑，不用阶跃函数step function



## 5.2 感知器与多层网络

- 感知器perceptron有两层神经元

  - 输入层input layer：传给output layer
  - 输出层output layer 为M-P神经元
    - M-P神经元即McCulloch-Pitts model（亦称为“阈值逻辑神经元”threshold logic unit）；input为[0, 1] (boolean)作逻辑运算 (0-excitatory; 1-inhibitory)
      - 线性可分问题linear separable：“与”，“或”，“非”
        - 学习过程中找出合适的w（参数）并且会_收敛converge_；否则过程会振荡flutation
      - 非线性可分：“异或”
        - 无法找到合适解；感知器过于简单无法解决非线性问题=>solution: 多层功能神经元functional neuron

- 多层功能神经元：

  - 输入层与输出层间的神经元：隐层/隐含层hidden layer
    - 输出层与隐层都有activation function
  - 学习过程调整update神经元之间的”连接权“connection weight及每个neuron的threshold
  - 每层neuron与下层全互连（无不同层连接与跨层连接）=>称为”多层前馈神经网络“multi-layer feedforward neural networks【不意味着不可以信号后传】

  

## 5.3 误差逆传播算法Back Propagation (BP)

- BP算法可以用于multi-layer feedforward neural networks以及其他类NN例如RNN

  - 基于梯度下降gradient descent策略
  - 更新参数【负梯度方向】->until gradient=0
  - 训练前如果存在离散属性，需要用前面章节提到的方法预处理（有”序“order关系；无order）

- 如何更新参数：需要用”链式法则“chain rule，算出不同层的误差error与参数的偏导

  - v为参数，v<-v + delta v， learning rate [0, 1]
    $$
    \Delta v = \frac{\partial E}{\partial v}\cdot\eta,\space where\space E\space is\space error\space function\space and\space\eta\space is\space learning\space rate
    $$

  - sigmoid function的性质
    $$
    f'(x)=f(x)(1-f(x))
    $$

  - 步骤大致为【输入：训练集&学习率；输出：参数确定的multi-layer feedforward neural network】
    - 随机初始参数(connection weights & threshold)
    - 【重复】
      - 计算当前样本输出
      - 计算各层神经元gradient
      - update parameters
    - until达到停止条件

- BP的目标：最小化训练集的累积误差

- 两种BP算法（两者间的区别与SGD和标准gradient descent类似）

  - 标准BP
    - 每次更新基于单个训练样例的E
      - 达到相同的累积误差需要更多的迭代iterations
      - 参数更新非常频繁
        - 更新效果可能“抵消” （？？？不明白）
  - 累积BP
    - 每次更新基于整个训练集（直接是累积误差最小化）
      - 参数更新频率低多了
      - 潜在问题：累计误差下降到一定时会难以进一步下降
        - =>这时候标准BP更快获得最优解，特别是大的数据集

- 实际中常用“试错法”trial-by-error设置隐层神经元的个数number of hidden layers（无法解决如何设置）

- 使用BP的潜在风险：由于BP效果好，容易过拟合

  - 策略1-“早停”early stopping：学习过程用训练集进行更新threshold与connection weights（参数）同时用验证集计算误差；若训练集误差下降但验证集误差上涨，停止，并返回验证集误差最小的参数
  - 策略2-“正则化”regularisation：误差目标函数error funciont中增加一项针对复杂度的(penaltise complexity)；regularisation parameter lambda between 0 and 1
    - 常用交叉检验法估计
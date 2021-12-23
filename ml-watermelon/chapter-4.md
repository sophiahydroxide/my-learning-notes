# 第4章 决策树

## 4.1 基本流程

- 什么是决策树decision tree: 树状模型用于决策
- 包括：根节点root node，一些内部结点internal node，一些叶结点leaf node
- 每一个结点对应一个属性



## 4.2 划分选择

- 选择最优划分属性，使分支的样本尽可能包含同一类别（找纯度purity高的）
- 如何划分
  - 信息增益information gain
    - 信息熵Information entropy衡量数据集纯度
      - entropy越小，纯度越高
    - 计算某属性的每个取值的entropy相加->给每个不同分支因不同样本树带来不同权重，then计算出此属性a对样本集D进行划分带来的“信息增益”information gain
      - 增益越大，纯度越高
    - 例子：ID3决策树
    - 弊端：对可取值数目多的属性有所偏好（e.g.不泛化）
  - 增益率gain ratio
    - 解决information gain带来的偏好不良影响，计算“增益率”gain ratio
    - 信息增益(Gain)/属性a的“固有值”intrinsic value (IV)
      - 属性a取值数目越多，IV越大
    - 弊端：对取值数目少的属性有所偏好
      - =>不直接作为划分属性的准则：
        - 1 找出信息增益高于平均水平的属性
        - 2 从中选gain ratio最高的
    - 例子：C4.5
  - 基尼指数Gini index
    - 基尼技术Gini index衡量数据集纯度
    - 例子：CART决策树
    - 最小化基尼基数



## 4.3 剪枝处理 pruning

- 目的：解决过拟合overfitting问题
  - 无pruning会不断划分结点导致过多分支，类似记住training dataset
  - pruning主动去掉一些分支
- 策略（数据集划分出training和testing/validation）
  - 预剪枝pre-pruning
    - 在进行下一个划分前估算在验证集划分前后的泛化性能，有提高则划
    - 优点：降低overfitting风险；降低训练时间开销；降低测试时间开销
    - 缺点：划分与否可能只是暂时的性能下降，不代表进一步划分就会表现差；“贪心”greedy的性质使之提早停止结点分支，导致欠拟合underfitting
  - 后剪枝post-pruning
    - 构造无pruning树再从下到上对比去除子树前后是否提高泛化性能，提高则替换子树为叶结点
    - 优点：比pre-pruning保留更多分支，欠拟合underfitting风险更小，泛化性能通常>pre-pruning
    - 缺点：训练时间比no pruning & pre-pruning长

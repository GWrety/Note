# 深度学习概况
Pytorch版本是0.4 看上去很老
发展期->顶峰->下降(缺点被发现)->冰河期(解决自身的问题)->应用期(应该学习 java c)
互联网公司所要求的和教授的很难一致
## 需要的能力
1. 线性代数 概率论与数理统计
2. Python
## 目标
1. 实现升深度学习使用Python
2. 理解神经网络和深度学习
## 智能
### 人类智能
1. 推理
    - 中午吃什么？ 
      - 外部信息: 经济 地点 偏好等
      - 推理:吃什么 
    - 穿什么？
      - 外部信息->推理
2. 预测
    - 猫
    猫的图像->猫的抽象概念
    - 数字
    数字的图像->数字的抽象概念

### 机器学习/人工智能
用算法模拟人的思维过程
- 主要是监督学习:数据集(知道图片答案，训练模型)
- 和算法课不同  算法来自于数据
## 深度学习
花书 
![20220714091519](https://raw.githubusercontent.com/GWrety/Ima/master/images/20220714091519.png)

# 开发深度学习系统
## 基于规则的系统
input->手工设计程序->output
1. 求原函数
- 知识库 基础求导公式  等价变形规则   三角变换(搜索树，找到可求)
## 经典机器学习
input->手工特征提取(x)->映射函数(y=f(x))->output(y)
## 表示学习
input->特征提取(x)->映射函数(y=f(x))->output(y)
*特征提取是无监督学习，映射是监督学习，分开训练*
>维度诅咒 维度越高对数据需求越大  
>降低维度(保留特性)：表示
## 深度学习  
input->简单特征->提取特性->映射函数->output
*end2end 端到端，大型系统，在一起训练*

# 神经网络
神经科学起源->数学与工程学
猫看幻灯片->哺乳动物大脑处理视觉分层->感知机
- 反向传播  back propagation
  前馈过程 反向传播:链式法则求偏导



# 线性模型
## 训练集
只用训练集容易过拟合
训练集->一部分模型训练+一部分开发集进行评估
1. 随机猜测
2. 评估模型和数据集存在的误差->损失
  
## 损失函数
1. 平均平方误差(Mean Square Error)MSE
![20220715082522](https://raw.githubusercontent.com/GWrety/Ima/master/images/20220715082522.png)
## 可视化工具
1. Visdom


# 梯度下降
分治法有可能会错过更优的目标点
## 梯度下降算法
导数 学习率 
1. 学习率不能过大，可能导致无法收敛
2. 非凸函数，可能局部最优
3. 深度学习中局部最优很少，但很多鞍点(梯度为0)  鞍点问题更大，会导致无法迭代
![20220715200559](https://raw.githubusercontent.com/GWrety/Ima/master/images/20220715200559.png)
## 绘图时
指数加权均值 将曲线画平滑
## 随机梯度下降
每次更新都选一点的损失
随机噪声可能会推动模型跨越鞍点，向最优值前进
![20220715202528](https://raw.githubusercontent.com/GWrety/Ima/master/images/20220715202528.png)

- 缺点 没法并行计算
## 折中
全都扔到一起算训练模型性能不好，全部用随机梯度时间复杂度高
Mini-Batch随机梯度(批量)
每次选一小部分进行下降



## 反向传播
### 损失对权重的偏导
![20220717155712](https://raw.githubusercontent.com/GWrety/Ima/master/images/20220717155712.png)
### 多层普通网络可以合并，所以需要用非线性函数进行变换
![20220717160818](https://raw.githubusercontent.com/GWrety/Ima/master/images/20220717160818.png)
### 反向传播过程
![20220717161543](https://raw.githubusercontent.com/GWrety/Ima/master/images/20220717161543.png)
### 实例
1.线性模型反向传播过程
![20220717162224](https://raw.githubusercontent.com/GWrety/Ima/master/images/20220717162224.png)

## PyTorch
### Tensor
张量，可以进行梯度的反向计算  自动前馈
```Python
b.requires_grad = True#设置进行计算历史的追踪，利用反向传播计算梯度
l.backward()#进行前馈  l代表b参与计算后的结果
b.data = b.data - 0.01 * b.grad.data#只取数据
b.grad.data.zero_()#梯度数据手动清0
```
构建模型就是构建计算图

# 用Pytorch实现线性回归
1. 数据集
2. 设计模型
3. 构造损失函数和优化器
    MSELoss
    SGD 
4. 训练周期
## 转置转化
![20220719082333](https://raw.githubusercontent.com/GWrety/Ima/master/images/20220719082333.png)

## 最终过程
![20220719130635](https://raw.githubusercontent.com/GWrety/Ima/master/images/20220719130635.png)



# 逻辑斯特回归
## 分类不是简单的线性回归
在分类手写字母时，不能简单的将输出结果按0~9排，因为7与9的输入相似性更高，对于相似的输入，输出也因该在附近，而8不符合规律
## 分类最后输出的是概率

## torchvision
包含了比较常用的数据集使用链接，进行下载到本地使用

## 二分类问题
只需要计算一个概率，剩下的另外一个直接1减去得到

## 饱和函数
logistics函数（又称之sigmoid函数）
函数有极限
![20220719173242](https://raw.githubusercontent.com/GWrety/Ima/master/images/20220719173242.png)

## 逻辑斯特线性回归模型
![20220719173445](https://raw.githubusercontent.com/GWrety/Ima/master/images/20220719173445.png)

## 交叉商
表示两个分布的相似性

## 二分类所用的损失函数 BCE
![20220719174803](https://raw.githubusercontent.com/GWrety/Ima/master/images/20220719174803.png)

## 实际使用
![20220719181351](https://raw.githubusercontent.com/GWrety/Ima/master/images/20220719181351.png)


# 处理多维度特征输入
修改权重的维度来配合输入与输出的维度

## 层数可以通过维度转换来增加
层数越多，学习能力越强，但可能会学习到噪声的规律，会导致问题

## 能力
1. 读文档
2. 基本架构理解(面对新东西从容，泛化能力比较好)

## 多层线性网络
用一个变量就行
![20220719220921](https://raw.githubusercontent.com/GWrety/Ima/master/images/20220719220921.png)

## 激活函数
有很多，有的连续，有的不连续

# 加载数据集



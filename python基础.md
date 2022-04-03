

`dot` 点积

`(5,)` 秩为1的数组  不要用



在代码中使用如下声明，随意插入   好习惯

```python
assert(a.shape == (5,1))
```





# 多个训练样本

将训练样本的特征写成列向量叠在一起，每一个样本的特征作为一个列向量。







### 画散点图

![image-20220216093310235](C:\Users\s'c\AppData\Roaming\Typora\typora-user-images\image-20220216093310235.png)



### 一个简单的神经网络

![image-20220216094946541](C:\Users\s'c\AppData\Roaming\Typora\typora-user-images\image-20220216094946541.png)





#### 回归

![image-20220216093731022](C:\Users\s'c\AppData\Roaming\Typora\typora-user-images\image-20220216093731022.png)

均方差

![image-20220216093957533](C:\Users\s'c\AppData\Roaming\Typora\typora-user-images\image-20220216093957533.png)

训练过程

![image-20220216094244413](C:\Users\s'c\AppData\Roaming\Typora\typora-user-images\image-20220216094244413.png)

加上可视化之后的总体过程

![image-20220216094434333](C:\Users\s'c\AppData\Roaming\Typora\typora-user-images\image-20220216094434333.png)

![image-20220216094344462](C:\Users\s'c\AppData\Roaming\Typora\typora-user-images\image-20220216094344462.png)



#### 分类

数据

![image-20220216095059759](C:\Users\s'c\AppData\Roaming\Typora\typora-user-images\image-20220216095059759.png)

![image-20220216095212272](C:\Users\s'c\AppData\Roaming\Typora\typora-user-images\image-20220216095212272.png)



优化器不变，但是损失函数有变化

![image-20220216095645877](C:\Users\s'c\AppData\Roaming\Typora\typora-user-images\image-20220216095645877.png)

这个损失函数计算的就是softmax，神经网络输出的东西就是每一个东西的概率

画图

![image-20220216101354134](C:\Users\s'c\AppData\Roaming\Typora\typora-user-images\image-20220216101354134.png)





### 保存提取

两种保存神经网络的方式

![image-20220216102309781](C:\Users\s'c\AppData\Roaming\Typora\typora-user-images\image-20220216102309781.png)

第一种是保存整个神经网络，第二种是保存神经网络节点的参数



两种提取方式

第一种，直接按神经网络的名字进行提取

```python
def restore_net():
    # restore entire net1 to net2
    net2 = torch.load('net.pkl')
    prediction = net2(x)
```

第二种，先创建一个一模一样的神经网络，然后复制相关的参数 

```python
def restore_params():
    # 新建 net3
    net3 = torch.nn.Sequential(
        torch.nn.Linear(1, 10),
        torch.nn.ReLU(),
        torch.nn.Linear(10, 1)
    )

    # 将保存的参数复制到 net3
    net3.load_state_dict(torch.load('net_params.pkl'))
```



出图方式代码，详见mofanpy.com 网站

最后别忘了写调用函数

![image-20220216103423783](C:\Users\s'c\AppData\Roaming\Typora\typora-user-images\image-20220216103423783.png)



### 批数据训练

```python
import torch.utils.data as Data

torch_dataset = Data.TensorDataset(x,y)
```

mini-batch 

不是很明白，用的时候再看看视频，





### 不同的优化器

![image-20220216112250384](C:\Users\s'c\AppData\Roaming\Typora\typora-user-images\image-20220216112250384.png)

具体代码见网站







## 使用tf构建一个手势识别模型的步骤

最后，我们已经实现了我们所有的函数，我们现在就可以实现我们的模型了。

我们之前在课程2就实现过random_mini_batches()这个函数，它返回的是一个mini-batches的列表。

在实现这个模型的时候我们要经历以下步骤：

创建占位符
初始化参数
前向传播
计算成本
反向传播
创建优化器
最后，我们将创建一个session来运行模型。



## 运算

#### dot

真正意义上的矩阵乘积



#### np.multiply   或者 *

单个元素对应乘积



## tf神经网络卷积函数的理解

### conv2d

例子：

```python
W = tf.truncated_normal([5, 5, 1, 32], stddev=0.1)
tf.nn.conv2d(x, W, strides=[1, 2, 2, 1], padding='SAME')
```


1、shape= [5,5,1,32]

前面两个5,表示卷积核的长宽分别为5

1表示输入图像对应的通道数，比如输入的图像是单通道的则设置为1，如果是RGB三通道的，则设置为3

32表示卷积核的个数，对应输出32张图

2、strides=[1, 2, 2, 1]

四个元素规定前后必须为1，中间两个数表示水平滑动和垂直滑动步长值

3、padding='SAME'

SAME表示在扫描的时候，如果遇到卷积核比剩下的元素要大时，这个时候需要补0进行最后一次的行扫描或者列扫描




### max_pool

```python
tf.nn.max_pool(A, ksize = [1,f,f,1], strides = [1,s,s,1], padding = 'SAME')
```

给定输入X，该函数将会使用大小为（f,f）以及步伐为(s,s)的窗口对其进行滑动取最大值



### ReLu

```python
tf.nn.relu(Z1)
```

计算Z1的ReLU激活
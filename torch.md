# torch



## tensors

可以利用GPU加速



## 基本语法

### 基本操作

导入包

```python
import torch
from __future__ import print_function
```

创建一个没有初始化的矩阵

```python
x = torch.empty(5,3)
```

#### 初始化

```python
torch.empty()
torch.rand(n,m)
torch.zeros(n,m,dtype=torch.long)
```

其他若干操作

```python
x.new_ones(n,m,dtype=torch.double)
torch.randn_like(x,dtype=torch.float)
s.size()
```



创建一个有初始化的矩阵

```python
x = torch.rand(5,3)
```



创建一个全零的矩阵，并指定数据的类型为long

```python
x = torch.zeros(5,3,dtype=torch.long)
print(x)
```

直接扔数据进去，常量张量

```python
x = torch.tensor([2.5,3.5])
# 和列表是不一样的，因为已经通过tensor进行了封装
```



通过已有的张量创建相同尺寸的张量

```python
x = x.new_ones(5,3,dtype = torch.double)
print(x)
```

采用随机初始化赋值，但是矩阵形状相同

```python
y = torch.randn_like(x,dtype = torch.float)
# 采用随机初始化的方法
print(y)
```

打印张量形状

#### x.size()返回的是一个元组类型tuple

```python
print(x.size())
# 张量形状返回的本质是一个tuple类型，torch.Size([5,3])
a, b = x.size()
print('a=',a)
print('b=',b)
```



### 基本运算

加法

```python
y = torch.rand(5,3)
print(x+y)
# 相同维度可以直接相加
```

```python
z = torch.add(x,y)
```



提前设定一个空的张量

```python
result = torch.empty(5,3)
# 将空的张量作为加法的结果存储张量
torch.add(x,y,out = result)
print(result)
```



原地置换

```python
y.add_(x)
print(y)
```



### 切片操作

选中某一列

```python
print(x[:,1])
```

选中前两列（注意这里列要填2，表示第0列，第1列）

```python
print(x[:,:2])
```



改变张量的形状

view必须保证个数一样

```python
x = torch.randn(4,4)
y = x.view(16) # 写成别的就会报错
z = x.view(-1,8) # -1自动匹配个数
print(x.size(),y.size(),z.size())
# view的关键，就是保证元素个数不变

# 但是用-1匹配，也不一定总是ok
# 比如不能整除的情况
z = x.size(-1,5)
```

但是可以这样，只写一个-1

![image-20220401115248241](C:\Users\s'c\AppData\Roaming\Typora\typora-user-images\image-20220401115248241.png)

**如果张量中只有一个元素，可以用.item()将值取出**，作为一个python number

多个元素则不行，不能使用item()

```python
x = torch.randn(1)
print(x)
print(x.item())
```

![image-20220401115429809](C:\Users\s'c\AppData\Roaming\Typora\typora-user-images\image-20220401115429809.png)

```python
x = torch.randn(2) # 一行两列
print(x)
print(x.item()) # 会报错
```



### tensor与array之间的转换

torch与array共享底层的内存空间，因此改变其中的一个值，另一个也会随之改变

```python
a = torch.ones(5)
print(a)
```



将tensor转换为array

```python
b = a.numpy()
print(b)
```



对其中一个进行加法操作，另一个也随之改变

```python
a.add_(b)
print(a)
print(b)
# .sub_
# .mul_
# 都是就地操作
```



将Numpy array转化为 torch Tensor

```python
import numpy as np
a = np.ones(5)
b = torch.from_numpy(a)
np.add(a,1,out=a)
print(a)
print(b)
# a和b都变成2了，共享内存
```

![image-20220401202829634](C:\Users\s'c\AppData\Roaming\Typora\typora-user-images\image-20220401202829634.png)



所有在CPU上的Tensors，除了Char Tensor之外，都可以转换为humpy array并可以反向转换。



### CUDA Tensor

两个不同设备上的Tensor是不可以直接执行加法的

Tensors可以用.to()方法来将其移动到任意设备上

```python
# 首先判断服务器上已经安装了GPU和CUDA
if torch.cuda.is_available():
    # 定义一个设备对象，这里指定成CUDA，即使用GPU
    device = torch.device("cuda")
    # 直接在GPU上创建一个Tensor,在cpu上创建张量x
    x = torch.randn(1);
    y = torch.ones_like(x,device=device)
    # 将x转移到GPU上
    x = x.to(device)
    # 此时x和y都在GPU上，才可以执行加法运算
    z = x + y
    # 和的结果z在GPU上
    print(z)
    # 再将z转移到CPU上进行打印
    z = z.to("cpu",torch.double)
    print(z)
```

想to到cpu上，直接to("cpu")

想to到gpu上，要to("cuda")



### autograd

pytorch中的自动求导

- 掌握自动求导中的Tensor概念和操作

- 掌握自动求导中的梯度Gradients概念和操作

在整个pytorch框架中，所有的神经网络本质上是一个autograd package(自动求导工具包)

- autograd package 提供了一个对Tensors上所有的操作进行**自动微分**的功能



#### 关于torch.Tensor

- **torch.Tensor是整个package中的核心类**,如果将属性requires_grad设置为True,它将追踪在这个类上定义的所有操作.当代码要进行反向传播的时候,直接调用.backward()就可以自动计算所有的梯度.在这个Tensor上的所有梯度将被累加进属性.grad中。

两种方法不让Tensor参与反向传播：

- 如果想终止一个Tensor在计算图中的追踪回溯,只需要执行.detach()就可以将该Tensor从计算图中撤下,在未来的回溯计算中也不会再计算该Tensor。**未来都没有了**
- 除了.detach()，如果想终止对计算图的回溯，也就是不再进行方向传播求导数的过程，也可以采用代码块的方式with torch.no_grad()；这种方式非常适用于对模型进行预测的时候，因为预测阶段不再需要对梯度进行计算.



#### 关于torch.Function

- Function类是和Tensor类同等重要的一个核心类，它和Tensor共同构建了一个完整的类，每一个Tensor拥有一个.grad_fn属性，**代表引用了哪个具体的Function创建了该Tensor。**
- 如果某个张量Tensor是用户自定义的，则其对应的graq_fn is None.



#### 关于Tensor的操作

```python
x1 = torch.ones(3,3)
print(x1)

x = torch.ones(2,2,requires_grad=True)
print(x)
```

![image-20220401211321837](C:\Users\s'c\AppData\Roaming\Typora\typora-user-images\image-20220401211321837.png)

在requires_grad属性等于True的任意一个Tensor上执行一个操作，他都会自动进行一个回溯，Tensor类就将追踪在上面定义的所有的操作，梯度也将被累加到属性.grad中。



打印grad.fn属性

```python
print(x1)
print(x)
z = x+2
print(z)
# 只有z打印出来的带有AddBockward对象
```

![image-20220401215901677](C:\Users\s'c\AppData\Roaming\Typora\typora-user-images\image-20220401215901677.png)



```python
x = torch.ones(2,2,requires_grad=True)
y = x+2
print(y)
z = y*y*3
out = z.mean
print(z,out)
```

关于方法.requires_grad_()  该方法可以原地改变Tensor的属性requires_grad的值，如果没有主动设定，默认为False

```python
a = torch.randn(2,2)
a = ((a*3)/(a-1))
# 这种操作都是矩阵对应元素相乘，相除
print(a.requires_grad)
a.requires_grad_(True)
print(a.requires_grad)
b = (a * a).sum()
print(b.grad_rn)
```



### 反向传播

是依靠.backward()实现的

```python
out.backward()
# 执行反向传播时，梯度就会累计地加到结果上
print(x.grad)
```

关于自动求导地属性设置，可以通过设置.requires_grad=True来执行自动求导，也可以通过代码块的限制来停止自动求导。

可以通过.detach()获得一个新的Tensor，有用相同的内容但不需要自动求导

```python
print(x.requires_grad)
y = x.detach() # 将X这个Tensor从计算图中拿掉
print(y.requires_grad)
print(x.eq(y).all()) # .eq只是纯数学的比较，只比较数值
```

这里x和y是完全相同的，只是对y不再自动求导了



```python
with torch.no_grad(): # 建议大量执行这个，而不是detach
    print((x**2).requires_grad)
# 放在这里，就代表不对with其中的代码块进行梯度求导了
```



![image-20220402180500513](C:\Users\s'c\AppData\Roaming\Typora\typora-user-images\image-20220402180500513.png)



requires_grad: 如果需要为张量计算梯度，则为True，否则为False。我们使用pytorch创建tensor时，可以指定requires_grad为True（默认为False），

grad_fn： grad_fn用来记录变量是怎么来的，方便计算梯度，y = x*3,grad_fn记录了y由x计算的过程。

grad：当执行完了backward()之后，通过x.grad查看x的梯度值。



## pytorch初步应用

> 掌握pytorch构建神经网络的基本流程
>
> 掌握pytorch构建神经网络的实现过程

### torch.nn

- 构建神经网络的工具都在torch.nn包中
- nn包依赖于autograd来定义，并对其自动求导



### 构建神经网络的典型流程

1. 拥有一个拥有可学习参数的神经网络
2. 遍历训练数据集
3. 处理输入数据使其流经神经网络
4. 计算损失值
5. 将网络参数的梯度进行反向传播
6. 以一定的规则更新网络的权重



#### 定义一个pytorch实现的神经网络

> 完成一个完整的class Net类


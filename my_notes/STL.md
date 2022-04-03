# STL

> 容器，迭代器，算法



## 容器

> 一些数据结构
>
> 写数据怎么结合存储



= 赋值操作符两边的容器必须要有相同型别，

### 序列式容器

最重要的特点，就是可以在首段删除元素，在尾端添加元素    

序列中至少包含一种迭代器

元素在容器中的位置，是由元素进入容器的时间和地点来决定其在容器中的位置



#### vector

容量大于等于其大小，vector可以实现队列，数组，堆栈的所有功能

```c++
vector<int> vec;//...初始化
count_if(vec.begin(),vec.end(),bind2nd(less<int>(),4));//统计vec中所有小于4的元素的个数
count_if(vec.begin(),vec.end(),bind2nd(greater<int>(),4));//统计vec中所有大于4的元素的个数

find_if(vec.begin(),vec.end(),bind2nd(less<int>(),4));//找到vec中第一个小于4的数字的下标
find_if(vec.begin(),vec.end(),bind2nd(greater<int>(),4));//..

for_each(vec.begin(),vec.end(),[](int &x){cout<<x<<"   ";});//使用lambda表达式来遍历vec数组
```



插入元素

在指定位置loc前插入值为val的元素,返回指向这个元素的迭代器,
在指定位置loc前插入num个值为val的元素
在指定位置loc前插入区间[start, end)的所有元素 .

```c++
//插入一个元素,加几就在下标为几的位置插入
vec.insert(vec.bagin(),5);//在下标为0的位置插入
vec.insert(vec.bagin()+1,5);//在下标为1的位置插入

//在某个位置插入几个相同的元素
vec.insert(vec.begin(),5,-1);//在第一个位置插入5个-1

vec.insert(vec.begin(),vec.begin()+5,vec.begin()+7);//将vec中下标为5的元素到下标为7的元素（不包括第7个元素）插入到vec的第一个元素处
```



#### deque

find 算法

```c++
deque<double>:: iterator it = find(dq.begin(),dq.end(),80.5);//返回80.5的迭代器
int step = (it-dq.bagin());//80.5的下标
```



### 关联式容器

元素的位置与先进后进无关，容器已经有规则了

#### set

set中的元素已经排好序，而且元素**不可以**重复

```c++
//从小到大，默认
set<int> s;

//从大到小
set<int,greater<int> > s;

s.lower_bound(5);//默认返回s中大于等于5的元素的迭代器，若从大到小排序则返回小于等于5的元素的迭代器
s.upper_bound(5);//与lower的区别是，没有等于了
```

pair的first是一个迭代器，不能直接cout，会报错

```c++
//可以使用distance算法来计算插入的元素的位置
p = s.insert(9);//返回一个pair
cout << *p.first << " " << p.second << endl;
cout << "the position is " << distance(s.begin(),p.first)+1 << endl;//若不+1，返回的是下标
```



#### multiset

可以包含重复的值



set和mutilset不能使用remove() 算法



#### map

insert方式，重复的key会直接被放弃，而不是进行覆盖（这一点与Java不同）

[]方式是可以覆盖的

```c++
testMap["bkey"] = "dval";
```





#### multimap

可以有多个重复的key值，即一个key值可以对应多个value





## 迭代器

用来遍历容器中元素的指针，默认情况下指向第一个元素的位置，当你给它++操作的时候，就往后移一位，迭代器可以取*，由此可以拿到这个元素。

对指针的操作都可以对指针操作。

事实上，迭代器是一个类，这个类封装了一个指针而已。可以把迭代器理解成一个指针



## 算法

通过有限的步骤来解决问题

STL提供了大约100个实现算法的模板函数

如统计，查找，替换，遍历





为什么会有这三样东西？？

开发容器的是一帮人，写算法的是一帮人，于是可以分工开发，但是两者之间要有联系，否则各做各的，是不行的。

于是，写容器的人，只要提供迭代器就可以了；写算法的人，只要用你提供的迭代器就可以了。迭代器在两者之间作为一个桥梁。





### 函数

> 变长数组

```c
vector <int> v;// 指定变长数组存储元素类型为int
```

##### insert

```c++
string s="abcdefg";
s.insert(3,"111");// 往第三个地址的前面插入
```


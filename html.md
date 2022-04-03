# html



![image-20210704084241058](C:\Users\s'c\AppData\Roaming\Typora\typora-user-images\image-20210704084241058.png)

详见vscode笔记



# CSS

## 三种引用方式

1. 外部样式表

   引入一个外部的css文件

   ```html
   <link rel="stylesheet" href="css/cssImport.css"/>
   ```

   

2. 内部样式表

   在head标签中引入css样式，使用style标签

   ```html
   <style>
       p{
           color:blue;
       }
   </style>
   ```

   

3. 标签中的style

   这种方式不建议使用，他把html和css的代码混在一起，不利于维护

   ```html
   <p style="color:red;">hello world</p>
   ```



## 选择器

1. 标签，类(.)和ID(#)选择器

   可以同时指定多个类名，会进行覆盖，后面写的样式会覆盖之前写的样式；但是要保证ID选择器设置的ID是唯一的

   优先级：ID选择器>类选择器>标签选择器

   BEM命名法   Block（模块）、Element（元素）、Modifier（修饰符）

2. 标签属性选择器

3. 伪类与伪元素

4. 关系选择器





## 样式

![image-20210704102222515](C:\Users\s'c\AppData\Roaming\Typora\typora-user-images\image-20210704102222515.png)

padding:内间距

margin：外间距





# web布局

## CSS常用布局

#### 什么是布局？

尺寸   定位



#### 普通文档流

默认将元素从左到右从上到下的摆放方式

块级元素<p>,<div>，行内元素<span>,<img>   可能需要做元素类型的转化，通过一个叫display的属性实现



## CSSflex布局

什么是flex

flexbox的缩写，弹性布局，一维的布局模型，任何一个容器都可以指定为flex布局



### flex容器

![image-20210712202711994](C:\Users\s'c\AppData\Roaming\Typora\typora-user-images\image-20210712202711994.png)

### 常用属性

#### 容器上的属性

- flex_direction

  控制flex元素的排列方向，四种摆放方式，水平方向从左向右，从右向左；竖直方向从上到下，从下到上

- flex-wrap

  控制换行的

- flex-flow

  将direction和wrap两个属性融合在一起

#### flex元素上的属性

- flex-basis

  控制图中的main size，若没有设置，这寻找widths，若设置了，则就是flex-basis

- flex-grow

  对元素剩余空间的处理

- flex-shrink

  对元素溢出空间的处理

- flex   综合

元素的对齐

- align-items 交叉轴对齐方式（纵轴）
- justify-content  主轴对其方式（水平轴）

### flex的适用场景

- 导航
- 拆分导航
- 元素居中
- 绝对底部

## CSS定位

### 定位（position）

> 对位置进行微调

- static(默认)

- relative（与top,left,right,buttom结合使用）

- absolute（所相对的值是**position值不为static**的父元素的偏移）一般用来实现居中

  子元素，父元素是指在html中嵌套的关系，一层套着一层，救说外面的是里面的父亲

- fixed（固定定位就是相对于浏览器的可视窗口所做的偏移）

- sticky 新兴的定位  relative+fixed的效果，当没有滚动到这个元素时，用的是relative，滚动到时，用的是fixed

  用途：随着页面滚动，导航栏还漂浮在上方



### 浮动

应用：文字环绕图片

缺点：影响的元素太多，会影响写在后面的元素，可以通过设置clear属性的值（left，right，both等）来清除浮动，也会清除写在其后面的所有浮动，**从当前元素开始，清除浮动。**       用途：写在浮动元素的后面，但又不想浮动



## 综合布局

纯文本类型：

一般使用line-height(行高)和text-align（文本居中）center



## 响应式布局






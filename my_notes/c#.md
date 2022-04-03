# c#



## 字符串插值

虽然字符串连接简单方便，但在需要将许多文字字符串和变量组合成单个格式化消息的情况下，*字符串插值*越来越受欢迎。

### 什么是字符串插值？

字符串插值通过使用“模板”和一个或多个*插值表达式*将多个值组合成单个文字字符串。的**插值表达式**是通过开闭大括号符号包围的变量`{ }`。当文字字符串以`$`字符为前缀时，它就成为模板。

换句话说，而不是编写以下代码行：

```csharp
string message = greeting + " " + firstName + "!";
```

您可以改为编写以下更简洁的代码行：

```csharp
string message = $"{greeting} {firstName}!";
```

在这个简单的示例中，您保存了几次击键。您可以想象在更复杂的操作中可以有多简洁的字符串插值。此外，许多人发现字符串插值语法更清晰、更易于阅读。



### 如何操作

要将两个字符串插入到一起，您需要创建一个文字字符串并在字符串前加上`$`符号。文字字符串应至少包含一组花括号，`{}`并在这些字符内使用变量名。

将以下代码添加到代码窗口：

```csharp
string firstName = "Bob";
string message = $"Hello {firstName}!";
Console.WriteLine(message);
```

现在，运行代码。您将在输出控制台中看到以下结果：

```output
Hello Bob!
```



您可以在同一行代码中执行多个插值操作。

将您在步骤 2 中编写的代码修改为以下代码：

```csharp
string firstName = "Bob";
string greeting = "Hello";
string message = $"{greeting} {firstName}!";
Console.WriteLine(message);
```

现在，运行代码。您将在输出控制台中看到以下结果：

```output
Hello Bob!
```



正如我们在前面的练习中所做的那样，我们可以消除用于存储消息的临时变量。

将您在第 3 步中编写的代码修改为以下代码：

```csharp
string firstName = "Bob";
string greeting = "Hello";
Console.WriteLine($"{greeting} {firstName}!");
```

现在，运行代码。输出控制台中的结果应该是相同的，但是我们简化了代码：

```output
Hello Bob!
```





假设您需要在模板中使用逐字文字。您可以同时使用逐字文字前缀符号`@`和字符串插值`$`符号。

删除前面步骤中的代码，然后在 .NET 编辑器中键入以下代码。

```csharp
string projectName = "First-Project";
Console.WriteLine($@"C:\Output\{projectName}\Data");
```

现在，运行代码，您应该会看到以下结果。

```output
C:\Output\First-Project\Data
```





## winform





### 事件

load：加载窗体。 当加载窗体的时候，将窗体对象放进Test类的静态字段中

click

注册事件：注册一个点击事件



触发事件：



静态类一个项目中资源共享，不能创建对象


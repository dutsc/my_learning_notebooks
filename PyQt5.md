# PyQt5



## 一个小案例

```python
from PyQt5.QtWidgets import QApplication, QMainWindow, QPushButton, QPlainTextEdit

'创建一个应用程序'
app = QApplication([])

'创建程序的主窗口'
window = QMainWindow()
window.resize(500, 400)
window.move(300, 310)
window.setWindowTitle('薪资统计')

textEdit = QPlainTextEdit(window)
textEdit.setPlaceholderText("请输入薪资表")
textEdit.move(10,25)
textEdit.resize(300,350)

button = QPushButton('统计', window)
button.move(380,80)
'展示窗口'
window.show()
'进入程序循环'
app.exec_()
```



## singal 和 slot

```python
def handCale():
    print('统计按钮被点击了')
button.clicked.connect(handClac)
```



如何从文本框中获取内容？

提供方法？



## Qt designer

exe文件路径：`E:\Devtools\anaconda\Lib\site-packages\PySide2`



## 界面布局layout

实现控件与界面一同缩放

手动控制水平布局与垂直布局


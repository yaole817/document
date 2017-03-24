# Python Debug

​	调试程序对于开发人员来说是一项非常重要的技能，它使得我们能够查看程序的运行过程，帮助我们准确的定位程序中的错误。

​	python最简单的调试方式就是**print**函数，这个对于简短的程序来说是没有问题的，但是对于大型项目来说简直是灾难，因为最终的输出文件里面是不需要这些debug信息的。

​	Python自带的pdb库，发现用pdb来调试程序还是很方便的，当然了，什么远程调试，多线程之类，pdb是搞不定的。这里介绍两种python调试器，分别为python自带的pdb和开源的ipdb。

## 1 标准库pdb

​	pdb是Python自带的一个库，为Python程序提供了一种交互式的源代码调试功能，包含了现代调试器应有的功能，包括设置断点、单步调试、查看源码、查看程序堆栈等。如果读者具有C或C++程序语言背景，则一定听说过gdb。gdb是一个由GNU开源组织发布的、UNIX/LINUX操作系统下的、基于命令行的、功能强大的程序调试工具。如果读者之前使用过gdb，那么，几乎不用学习就可以直接使用pdb。pdb和gdb保持了一样的用法，这样可以降低工程师的学习负担和Python调试的难度，pdb提供的部分调试命令见下表。

| Command        | Description   | Example       |
| -------------- | ------------- | ------------- |
| break 或 b 设置断点 | 设置断点          | b 3  在第三行设置断点 |
| continue 或 c   | 继续执行程序        |               |
| list 或 l       | 查看当前行的代码段     |               |
| step 或 s       | 进入函数          |               |
| return 或 r     | 执行代码直到从当前函数返回 |               |
| exit 或 q       | 中止并退出         |               |
| next 或 n       | 执行下一行         |               |
| p              | 打印变量的值        |               |
| help           | 帮助            |               |



​	有两种方式来启动python 调试器，一种是直接在命令行参数中指定使用pdb模块启动python文件，如下所示：

```python
python -m pdb test_pdb.py
```

​	另一种方法是在python代码中，调用pdb模块的set_trace方法设置一个断点，当程序运行到这里时，将会暂停执行并打开pdb调试器。如下所示：

```python
# /usr/bin/python
from __future__ import print_function
import pdb
def sum_nums(n):
	s = 0
	for i in range(n):
		pdb.set_trace()
		s+= i
		print(s)

if __name__ == '__main__':
	sum_nums(10)
```



​	两种方法并没有什么质的区别，选择使用哪一种方式主要取决于应用场景，如果程序文件较短，可以通过命令行参数的方式启动Python调试器；如果程序文件较大，则可以在需要调试的地方调用set_trace方法设置断点。无论哪一种方式，都会启动Python调试器，前者将在Python源码的第一行启动Python调试器，后者会在执行到pdb.set_trace()时启动调试器。

## 2 ipdb

​	ipdb是一个开源的Python调试器，它和pdb有相同的接口，但是，它相对于pdb，具有语法***高亮、tab补全、更友好的堆栈信息***等高级功能。ipdb之于pdb，就相当于IPython之于Python，虽然都是实现相同的功能，但是，在易用性方面做了很多的改进。

​	需要注意的是，pdb是Python的标准库，不用安装就可以直接使用。而ipdb是一个第三方的库，因此，需要使用pip先安装，然后才能使用，安装方法是：

```python
pip install ipdb
```


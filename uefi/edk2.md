# edk2 learning

## 1 protocol

### 1.1 什么是protocol

​	先说一下protocol是什么，《uefi原理与编程》中介绍说protocol 是服务器与客户端之间的一种约定，双方根据这种约定互通信息。自我感觉这种定义很不好，不能形象的描述protocol的功能。

​	网上还有一种定义是protocol是功能和数据的集合。这就比较贴切，但是对于刚开始接触这个概念的还是有点模糊。我自己给的定义是protocol其实类似于C++中的象类的定义，其实就是功能和数据的集合。

### 1.2 如何使用protocol

​	有了上面的概念其实使用就很好理解了，想想如何使用类就很相似了。主要分为三步：

1.   找到想要使用的protocol，也就是实现一个类的实例化，edk2中定义了三个函数来实现这个功能，openProtocol，LocateProtocol 或者是handleProtocol；

2.   使用这个protocol 提供的服务，也就是使用类的成员函数；

3.   关闭打开的protocol，也就是要销毁这个类，在C++中由析构函数自动实现，在edk2中使用CloseProtocol 这个函数实现。

## 1.3 protocol 安装

​	protocol 安装在image中

 

##2 image

### 2.1 什么是image

​	image中文翻译是镜像，给人的第一反应是一个iso文件，但是在内存中需要消除这个刻板印象，image在内存中其实就是一个可执行文件所对应的内存区域。

​	

## 3 handle

### 3.1 什么是handle

# 4 UEFI 相关概念

## 4.1 UEFI 驱动

​	定义：UEFI驱动是指符合UEFI驱动模型的驱动。这个定义比较生硬，也不太好理解。简单的理解方式是其实是UEFI kernel 的驱动。也可以说是UEFI kernel 的服务。

## 4.2 DXE 驱动

​	定义：不遵循UEFI驱动模型的驱动称为DXE驱动。这里的DXE驱动一般指实际硬件的驱动，因为硬件厂商有自己的定义接口不需要严格遵循UEFI的驱动模型，只要接口一致就可以了。


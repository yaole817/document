# edk2 learning

流程：SEC——PEI——DXE——BDS——TSL——RT——AT



​	整个系统可以描述为CPU加一系列外设。系统的工作就是CPU带动一些列外设的工作。

​	**SEC**：前期验证，验证一些电源信号

​	**PEI**：初始化CPU，系统想要开始工作，首先需要初始化CPU（包括时钟的初始化，中断的初始化，总线的初始化等）；初始化芯片，这个主要是初始化DRAM；主板的初始化

​	**DXE**：执行大部分系统初始化工作，主要是驱动的加载，系统的逻辑控制

​	**BDS**：初始化控制台，加载必要的设备驱动，根据设置加载和执行启动项

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

​	Handle 可以理解为数据库的概念，而protocol 就是数据库中的表，而GUID可以理解位主键，主键必须唯一。

​	Handle 数据库由handles和protocol 组成，handles由一个或多个protocols组成，protocols则是由GUID来命名的数据结构体，这个数据结构体可能是空，可能包含数据，可能包含服务，或者同时包含数据和服务程序。在EFI的初始化中，系统固件，EFI驱动和EFI应用创建handles，并为每个handle挂上一个或多个protocols。在handle数据库中信息是全局的，而且能被任何一个可执行的EFI image访问。

# 4 UEFI 相关概念

## 4.1 UEFI 驱动

​	定义：UEFI驱动是指符合UEFI驱动模型的驱动。这个定义比较生硬，也不太好理解。简单的理解方式是其实是UEFI kernel 的驱动。也可以说是UEFI kernel 的服务。

​	

## 4.2 DXE 驱动

​	定义：不遵循UEFI驱动模型的驱动称为DXE驱动。这里的DXE驱动一般指实际硬件的驱动，因为硬件厂商有自己的定义接口不需要严格遵循UEFI的驱动模型，只要接口一致就可以了。

## 4.3 PPI

PPI (PEIM-to-PEIM interface)

## 4.4 主机总线控制器

​	在第一个驱动控制器被连接之前，某些最初的（固有的）控制器需要存在来被驱动管理，这些最初的固有的控制器就是大家知道的主机总线控制器。主机总线控制器所提供的I/O抽象是由EFI驱动模型之外的固件组件所产生的，主机总线控制器的device handle 和I/O抽象必须由平台上的固件内核或者可能不遵循EFI驱动模型的EFI驱动产生



## 4.5 Driver Binding

​	Driver Binding 有start support 和 stop。


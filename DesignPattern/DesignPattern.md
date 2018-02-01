# 设计模式汇总整理

学习设计模式是通过《Head First 设计模式》这本书，现在需要总结一下学习结果，由于需求，会把书中的代码转换为c++来展示。

## 背景

我们都知道设计经验的重要价值。你曾经多少次有过这种感觉——你已经解决了一个问题但是就是不能确切知道是在什么地方或者怎么解决的？如果你能记起以前问题的细节和怎么解决它的，你就可以复用以前的经验而不需要重新发现它。然而我们并没有很好的记录下可供他人使用的软件设计经验。设计模式就是将面向对象软件的设计经验作为设计模式记录下来。

设计模式就是面向对象的圣经。

## 综述

### 设计模式定义：

**模式**是某一情境下，针对某问题的解决方案。

**情境**就是应用某个模式的情况。这应该是会不断出现的情况

**问题**就是你想在某种情境下达到的目标，但也可以是某种情境下的约束。

**解决方案**就是你所追求的：一个通用的设计，用来解决约束、达到目标。

​	设计模式是一套被反复使用的、多数人知晓的、经过分类编目的、代码设计经验的总结。使用设计模式是为了重用代码、让代码更容易被他人理解、保证代码可靠性。 毫无疑问，设计模式于己于他人于系统都是多赢的，设计模式使代码编制真正工程化，设计模式是软件工程的基石，如同大厦的一块块砖石一样。项目中合理地运用设计模式可以完美地解决很多问题，每种模式在现实中都有相应的原理来与之对应，每种模式都描述了一个在我们周围不断重复发生的问题，以及该问题的核心解决方案，这也是设计模式能被广泛应用的原因。

### 设计模式的意义：

**共享词汇**

共享词汇可以帮我们节省表达方式，更便于理解，比如说这段代码实现的是一个二分法，如果不关注细节，只关注整体框架，其实就已经完成了对于框架的把握。比如说 bios dispatcher 对driver的遍历是通过迭代器模式来实现的。windows 的消息机制是通过观察者模式实现的。callback 函数是通过模板模式实现的等

**解耦**，耦合是指代码之间的相互依赖性，解耦就是指代码的独立性

**代码复用**，有一些语言已经将一些通用的模式作为库函数来使用

###设计模式总共分为三大类：

**创建型模式**，共5种：工厂方法、抽象工厂方法、单利模式、建造者模式、原型模式

**结构性模式**， 共7种：适配器模式、装饰器模式、代理模式、外观模式、桥接模式、组合模式、享元模式。

**行为模式**，共11种：策略模式、模板方法模式、观察者模式、迭代器模式、责任链模式、命令模式、备忘录模式、状态模式、访问者模式、中介者模式、解释器模式。

###设计模式六大原则：

**开闭原则** ——总原则：

对扩展开放，对修改封闭。在程序需要进行拓展的时候，不能去修改原有的代码，而是要扩展原有的代码，实现一个热插拔的效果

**单一职责原则（类应该只有一个改变的理由）**

不要存在多余一个导致类变更的原因，也就是说每个类应该实现单一的职责，否则就应该把类拆分

**接口隔离原则（多用组合少用继承）**

每个接口中不存在子类用不到却必须实现的方法，如果不然，就要将接口拆分。使用多个隔离接口，比使用单个几口要好。

**里氏替换原则**

任何基类可以出现的地方，子类一定可以出现。历史替换原则是继承复用的基石，只有当衍生类可以替换基类，软件单位的功能不受任何影响时，积累才能真正的被复用，而衍生类也能够在积累的基础之上增加新的行为。

里氏替换原则是对“开-闭”原则的补充。实现开闭原则的关键步骤就是抽象化，而基类与子类的继承关系就是抽象的具体实现，所以里氏替换原则是对实现抽象化的具体步骤的规范。

**依赖倒置原则**

这个原则是开闭原则的基础，具体内容：针对接口编程，不针对实现编程。

**迪米特法则（最少知道原则）**

最少知道原则是指：一个实现应该尽量少的与其他实体之间发生的相互作用，使系统功能模块相对独立



## 单例模式

### 定义

**单例模式** 确保一个类只有一个对象，并提供一个全局的访问点。

有一些对象其实我们只需要一个，比如说注册表的对象，线程池、充当打印机、显卡等设备的驱动程序的对象等。事实上，这类对象只能有一个实例，如果制造出多个实例，就会导致许多问题产生，例如：程序的异常、资源使用过量，或者是不一致的结果。

### 独一无二的对象

单例模式用来创建独一无二的，只能有一个实例对象。

### 如何创建一个独一无二的对象

 ```c++
class Singleton {
public:
	Singleton(void);
	~Singleton(void);
     other method
};
 ```

```c++
s = Singleton()
```

问：如何创建一个对象？

​	答：new MyObject

问：万一另一个对象想创建MyObject会怎么样？可以再次 new MyObject吗？

​	答：当然可以

问：所以一旦有一个公开类，我们是否都能多次实例化它？

​	答：如果是公开的类，就可以

问：如果这个类不是公开的呢？如果是私有的构造器呢？

 ```c++
class Singleton{
private:
    Singleton(){}
}
 ```

​	答： 私有构造器没有办法被实例化



​	

### 创建一个独一无二的对象

```C++
class Singleton {
private/protected:
	Singleton(void);
	~Singleton(void);
     other method
};
```

Tips：protected 和private 区别

1. private 是完全私有的,只有当前类中的成员能访问到.
2. protected 是受保护的,只有当前类的成员与继承该类的类才能访问.
3. 这两个是访问类中成员权限的限制符.在类外如果想使用类中的成员,只能直接使用public类型的,protected和private都是不能访问的,对于类外使用而言,这两个是完全相同的.

可是，怎么实例化这个类？

```c++
s = Singleton()  ????
```

### 静态成员函数

使用static修饰的成员函数，只能被定义一次，而且要被同类的所有对象所共享，它是类的一种行为，与对象无关，它有如下特点：

1）静态函数成员不可以直接访问类中非静态数据成员以及非静态成员函数，只能通过对象名（由参数传入）来访问；

2）静态成员函数在类外实现时，无需加static修饰，否则出错；

3）在类外，可以通过对象名以及类名来调用类的静态成员函数。

### 最终实现

singleton.h

```c++
#pragma once
class Singleton {
public:
    static Singleton* getInstance(void);
	void showMessage(void);
  
protected:
	Singleton(void){};

private:
	~Singleton(void);
	static Singleton* uniqueSingleton;
};
```

singleton.cpp

```C++
#include "Singleton.h"
#include <iostream>

Singleton* Singleton::uniqueSingleton = NULL;

Singleton* Singleton::getInstance() {
	if(uniqueSingleton == NULL){
		uniqueSingleton = new Singleton();
	}
	return uniqueSingleton;
}

Singleton::~Singleton(void) {
	if (uniqueSingleton == NULL) {
		return;
	}
	delete uniqueSingleton;
	uniqueSingleton = 0;
}

void Singleton::showMessage(){
	std::cout<<"singleton is created!"<<std::endl;
}
```

main.cpp

```c++
#include "Singleton.h"

int main() {
	Singleton* singleton = Singleton::getInstance();
	singleton->showMessage();
	return 0;
}
```



##策略模式

### 模拟鸭子应用

Joe 公司做了一套相当成功的模拟鸭子的游戏：SimUDuck。游戏中会出现各种鸭子，一边游泳戏水，一边呱呱叫。此系统的内部设计使用了标准的OO技术，设计一个鸭子超类（Superclass），并让鸭子继承此超类。



![Duck](DesignPattern\Duck.png)

quack()  所有的鸭子都有叫（quak()）的属性，也会游泳（swim()），所以在基类中负责处理这部分代码实现。

而每种鸭子的外观都不相同，所以display 方法是抽象的，由每个子类来实现自己的display方法



class Duck 代码

Duck.h

```c++
#pragma once
class Duck {
public:
	virtual void display() = 0;
	void swim();
	void quak();
};
```

Duck.cpp

```c++
#include "Duck.h"
#include <iostream>
void Duck::quak(){
	std::cout<<"quak,quak"<<std::endl;
}

void Duck::swim(){
	std::cout<<"I can swim"<<std::endl;
}
```



Class MallardDuck 代码

MallardDuck.h

```c++
#pragma once
#include "duck.h"
class MallardDuck : public Duck {
public:
	void display();
	MallardDuck(void);
	~MallardDuck(void);
};
```

MallardDuck.cpp

```c++
#include "MallardDuck.h"
#include <iostream>

void MallardDuck::display() {
	std::cout<<"I am a mallard duck!"<<std::endl;
}
```



ReadHeadDuck 类似实现

测试代码

main.cpp

```c++
#include "Duck.h"
#include "MallardDuck.h"

int main() {
	MallardDuck mallardDuck;
	mallardDuck.display();
}
```



###新的需求，让鸭子起飞

现在市场部发来了一个新的需求，要让某些鸭子会飞的属性。怎么通过改动最少的代码来让增加一个会飞的鸭子？

1、在超类中添加一个fly() 属性，这样就可以让鸭子具有一些fly()的特性，如下面的类图所示

![fly](DesignPattern\fly.png)

但是，这样所有的子类都会继承fly 的方法，让有些不会飞的鸭子也在屏幕上乱飞，比如小黄鸭之类的

2、将fly() 属性添加到派生类的属性中，即在子类中实现fly 的方法，但是这样又不会出现代码重复，不符合OO设计原则

3、使用接口实现，实现两个接口（c++ 中的纯虚类，所有的成员函数是由纯虚函数来实现的，子类必须实现父类的成员函数）。将fly() 和quack()  抽象成行为来实现，子类如果需要使用，需要自己实现自己的行为，如下图所示

![interface](DesignPattern\interface.png)



这种实现的重复代码也会增加很多，假设有48种鸭子需要修改飞行行为，那是不是要改所有的飞行实现（因为接口是不存在实现的，只是提供一个抽象）？

### 把问题归零

现在我们会发现使用继承并不能很好的解决问题，因为鸭子的行为在子类中不断的改变，并且让所有的子类都有这些行为是不恰当的。

**设计原则：找出应用中可能需要变化之处，把它门独立出来，不要和那些不需要变化的代码混淆在一起**

### 设计鸭子行为

现在我们把鸭子的行为分离出来，将分离出flyable 和 quackable行为，希望所有的代码能有弹性

**设计原则： 针对接口编程，而不是针对实现编程**

### 针对接口编程与针对实现编程

针对实现编程

```c++
Dog* d = new Dog();
d->bark()
```

针对接口编程

```c++
Animal* animal = new Dog();
animal->bark();
```

### 重构

#### 实现鸭子的行为

![FlyBehavior](DesignPattern\FlyBehavior.png)



![QuackBehavior](DesignPattern\QuackBehavior.png)

这样的设计可以让飞行和呱呱叫的动作被其他对象复用，因为这些行为已经与鸭子类无关了。

并且当我们新增一些新的行为时候，不会影响到现在既有的行为类，也不会影响到“使用”到飞行行为的鸭子类。

#### 整合鸭子的行为

这样就将飞行和呱呱叫的行为委托给其他类进行处理，而不是使用定义在Duck类(或子类)中的的呱呱叫或飞行方法。

做法是这样的：

首先，在Duck类中“加入两个实例变量”，分别为“flyBehavior” 与 “quackBehavior”， 声明为接口类型（而不是具体实现类型），每一类鸭子对象都会动态的设置这些变量以在运行时正确的引用正确的行为类型

![DuckUML](DesignPattern\DuckUML.png)

DucK 类

Duck.h

```c++
#pragma once
class Duck {
public:
	virtual void display() = 0;
	void swim();
	void performQuack();
	void performFly();
private:
	QuackBehavior* quackBehavior;
	FlyBehavior* flyBehavior;
};
```



###解决方案

#### fly 行为

FlyBehavior.h

```c++
#pragma once
class FlyBehavior{
public:
	virtual void fly() = 0;
};
```

FlyWithWings.h

```c++
#pragma once
#include "flybehavior.h"
class FlyWithWings : FlyBehavior {
public:
	void fly();
};
```

FlyWithWings.cpp

```c++
#include "FlyWithWings.h"
#include <iostream>

void FlyWithWings::fly(){
	std::cout<< "I am flying" <<std::endl;
}
```

FlyNoWay.h

```c++
#pragma once
#include "flybehavior.h"
class FlyNoWay : public FlyBehavior {
public:
	 void fly();
};
```

FlyNoWay.cpp

```c++
#include "FlyNoWay.h"
#include <iostream>

void FlyNoWay::fly(){
	std::cout<< "I can not fly" <<endl;
}
```



####quack行为

QuackBehavior.h

```c++
#pragma once
class QuackBehavior {
public:
	virtual void quack()=0;
};
```

Quack.h

```c++
#pragma once
#include "quackbehavior.h"
class Quack : public QuackBehavior {
public:
	void quack();
};
```

Quack.cpp

```c++
#include "Quack.h"
#include <iostream>

void Quack::quack(){
	std::cout<<"I am quacking"<<std::endl;
}
```

Squeak.h

```c++
#include "Squeak.h"
#include <iostream>

void Squeak::quack(){
	std::cout<<"squeak, squeak, squeak" <<std::endl;
}
```

MuteQuack.h

```c++
#pragma once
#include "quackbehavior.h"
class MuteQuack : public QuackBehavior {
public:
	void quack();
};
```

MuteQuack.cpp

```c++
#include "MuteQuack.h"
#include <iostream>

void MuteQuack::quack(){
	std::cout<< "I am silence"<<std::endl;
}
```



#### Duck 类

Duck.h

```c++
#pragma once
#include "QuackBehavior.h"
#include "FlyBehavior.h"
class Duck {
public:
	virtual void display() = 0;
	void swim();
	void performQuack();
	void performFly();
	virtual ~Duck();

private:
	QuackBehavior* quackBehavior;
	FlyBehavior* flyBehavior;
};
```



Duck.cpp

```C++
#include "Duck.h"
#include <iostream>

void Duck::swim(){
	std::cout<<"I can swim"<<std::endl;
}

void Duck::performFly(){
	flyBehavior->fly();
}
void Duck::performQuack(){
	quackBehavior->quack();
}

Duck::~Duck(){
	delete flyBehavior;
	delete quackBehavior;
}
```

#### Duck子类

MallardDuck.h

```c++
#pragma once
#include "Duck.h"
class MallardDuck : public Duck {
public:
	MallardDuck();
	void display();
};
```

MallardDuck.cpp

```c++
#include "MallardDuck.h"
#include "FlyWithWings.h"
#include "Quack.h"
#include <iostream>

void MallardDuck::display(){
	std::cout<<"I am a mallard duck!"<<std::endl;
}

MallardDuck::MallardDuck(){
	quackBehavior = new Quack();
	flyBehavior = new FlyWithWings();
}
```

#### 测试函数

main.cpp

```c++
#include "Duck.h"
#include "MallardDuck.h"
#include "FlyNoWay.h"
#include <iostream>
int main() {
	MallardDuck* mallardDuck = new MallardDuck();
	mallardDuck->display();
	Duck* mallard = new MallardDuck();
    mallard->performFly();
    mallard->performQuack();
    //mallard->setFlyBehavior(new FlyNoWay());
    //std::cout<<"My wings hurt!!"<<std::endl;
    //mallard->performFly();
    delete mallard;
    delete mallardDuck;
    return 0;
}
```

#### 运行结果

```
I am a mallard duck!
I am flying
I am quacking
My wings hurt!!
I am flying
请按任意键继续. . .
```



### 定义

策略模式 定义了算法族，分别封装起来，让他们之间可以互相替换，此模式让算法的变化独立于使用算法的用户。



## 装饰器模式

### Starbuzz咖啡厅

Starbuzz 是一个以扩张速度最快而闻名的咖啡连锁店。因为扩张速度实在太快，老板门准备更新订单系统，以合乎他们的饮料供应要求。

原先的设计是这样的

![Starbuzz](DesignPattern\Starbuzz.png)



但是购买咖啡时，也可以要求在其中加入各种饮料，例如：蒸奶（Steamed Milk)、豆浆（soy）、摩卡（Mocha）或者奶泡。Starbuzz 会根据所加入的调料收取不同的费用。所以订单系统必须考虑到这些调料部分的价格。

###第一个尝试

一个基类，剩下的所有子类全部继承这个基类，然后实现自己的私有方法(因为每个类都有自己的cost属性)，但是这样就会产生非常多的类。



### 认识装饰器模式

1. 拿一个深焙咖啡(DarkRost)对象

2. 以Mocha对象装饰它

3. 以奶泡(Whip)对象装饰它

4. 调用cost() 方法，并依赖委托将调料的价钱加上去


### 以装饰者构造饮料订单

1 定义一个DarkRoast 对象开始

2 如果顾客想要摩卡，所以建立一个Mocha对象，并用它将DarkRoast 对象包起来

3 如果顾客也想要奶泡了，所以需要建立一个Whip装饰者，并用它将Mocha对象包起来。


![DarkRoast](DesignPattern\DarkRoast.png)



4 最后，给顾客算钱的时候，通过最外圈的装饰者的cost() 就可以办得到。whip的cost() 先委托它的装饰的对象（也就是mocha）计算出价钱，然后再加上奶泡的价格。以此类推出最后的结果。

![StarbuzzDecorate](DesignPattern\StarbuzzDecorate.png)

### 定义

装饰者模式动态地将责任附加到对象上。若要扩展功能，装饰者提供了比继承更有弹性的替代方式。

- 装饰者和被装饰者有相同的超类型


- 你可以用一个或多个装饰者包装同一个对象
- 既然装饰者和被装饰者拥有相同的超类，所以在任何需要原始对象的场合，可以用装饰过的对象来替换他
- 装饰者可以在所委托被装饰者的行为之前或之后，加上自己的行为，已达到特定的目的
- 对象可以在任何时候被装饰，所以可以在运行时动态地、不限量地用你喜欢的装饰者来装饰对象。

### Starbuzz 框架



![Beverage](DesignPattern\Beverage.png)

### 设计原则

类应该对扩展开放，对修改关闭。

### Starbuzz 实现

####实现基类 Beverage

Beverage.h

```c++
#include <string>
using std::string;
#pragma once
class Beverage {
public:
	Beverage(){}
	Beverage(string discription);
	virtual double cost() = 0;
	virtual string getDescription();
private:
	string _description;
};
```

Beverage.cpp

```c++
#include "Beverage.h"

Beverage::Beverage(string description = "Unknow Beverage") : _description(description){}
//Beverage::Beverage(string description = "Unknow Beverage"){
//	_description = description;
//}

string Beverage::getDescription(void) {
	return _description;
}
```

#### 装饰基类

CondimentDecorator.h

```c++
#pragma once
#include "Beverage.h"
class CondimentDecorator : public Beverage {
public:
	CondimentDecorator(){}
	virtual string getDescription() = 0;
};
```

#### 原料类

DarkRost.h

```c++
#pragma once
#include "beverage.h"
class DarkRost : public Beverage {
public:
	DarkRost();
	double cost() override;
};
```

DarkRost.cpp

```c++
#include "DarkRost.h"

DarkRost::DarkRost(void) : Beverage("DarkRost"){}

double DarkRost::cost(){
	return 0.89;
}
```

#### 装饰类

Mocha.h

```c++
#pragma once
#include "condimentdecorator.h"
class Mocha : public CondimentDecorator {
public:
	Mocha(Beverage* beverage);
	string getDescription() override;
	double cost() override;
private:
	Beverage* _beverage; 
};

```

Mocha.cpp

```c++
#include "Mocha.h"
Mocha::Mocha(Beverage* beverage) : _beverage(beverage){}
//Mocha::Mocha(Beverage* beverage){
//	_beverage = beverage;
//} 

string Mocha::getDescription(){
	return _beverage->getDescription() + ", Mocha";
}

double Mocha::cost(){
	return 0.20 + _beverage->cost();
}
```

Whip.h

```c++
#pragma once
#include "CondimentDecorator.h"
class Whip : public CondimentDecorator{
public:
	Whip(Beverage* beverage);
	string getDescription() override;
	double cost() override;
private:
	Beverage* _beverage; 
};
```

Whip.cpp

```c++
#include "Whip.h"
//Whip::Whip(Beverage* beverage) : _beverage(beverage){}
Whip::Whip(Beverage* beverage){
	_beverage = beverage;
} 

string Whip::getDescription(){
	return _beverage->getDescription() + ", Whip";
}

double Whip::cost(){
	return 0.10 + _beverage->cost();
}
```



#### 测试

main.cpp

```c++
#include <iostream>
#include "DarkRost.h"
#include "Mocha.h"
#include "Whip.h"
using std::cout;
using std::endl;

int main(){
	Beverage* beverage = new DarkRost();
	cout << beverage->getDescription() << " $" << beverage->cost() << endl;
	
	Beverage* beverage2 = new DarkRost();
	beverage2 = new Mocha(beverage2);
	cout<< beverage2->getDescription()<< " $"<< beverage2->cost() <<endl;

	beverage2 = new Whip(beverage2);
	cout<< beverage2->getDescription()<< " $"<< beverage2->cost() <<endl;

	delete beverage;
	delete beverage2;
}
```

#### 运行结果

```bash
DarkRost $0.89
DarkRost, Mocha $1.09
DarkRost, Mocha, Whip $1.19
请按任意键继续. . .
```



### Python 装饰器与语法糖

#### 函数装饰器

```python
# coding: utf-8

def foo():
    print("foo")
foo
foo()
foo = lambda x: x + 1
foo(1)

def w1(func):
    def inner():
        print("test")
        return func()
    return inner

@w1
def f1():
    print("f1")

@w1
def f2():
    print("f2")
@w1
def f3():
    print("f3")
f1()
f2()
f3()

def w1(func):
    def wrapper(*args, **kwargs):
        print("test")
        return func(*args, **kwargs)
    return wrapper

@w1
def f1():
    print("f1")
f1()
```

#### 带参数的函数装饰类

```python

def w1(parameter):
    def wrapper(func):
        def inner_wrapper(*args, **kwargs):
            print("test")
            print(parameter)
            return func(*args, **kwargs) 
        return inner_wrapper
    return wrapper

@w1("w1")
def f1():
    print("f1")
f1()

@w1("W2")
def f2():
    print("f2")
f2()


def logging(level):
    def wrapper(func):
        def inner_wrapper(*args, **kwargs):
            print("[{level}]:enter funtion {func}() ".format(level=level, func = func.__name__), end = "")
            return func(*args, **kwargs)
        return inner_wrapper
    return wrapper

@logging(level = "INFO")
def say(something):
    print("say {}!".format(something))

say("hello world")

```



#### 不带参数装饰类

```python
class logging(object):
    def __init__(self, func):
        self.func = func
    def __call__(self, *args, **kwargs):
        print("[DEBUG]: enter function {func}() : ".format(func = self.func.__name__), end = '')
        return self.func(*args, **kwargs)

    
@logging
def say(something):
    print("say {}!".format(something))

say("hello world")

```

#### 

####带参数的装饰类

```python
class logging(object):
    def __init__(self, level = "INFO"):
        self.level = level
    def __call__(self, func):
        def wrapper(*args, **kwargs):
            print("[DEBUG]: enter function {func}() : ".format(func = func.__name__), end = '')
            func(*args, **kwargs)
        return wrapper
@logging(level = "DEBUG")
def say(something):
    print("say {}".format(something))
say("hello world")
```



## 模板模式

###咖啡和茶

星巴克有一个需求是需要制造一套程序来泡咖啡和茶，冲泡方法如下：

咖啡冲泡方法

(1) 把水煮沸

(2) 用沸水冲泡咖啡

(3) 把咖啡倒进杯子里

(4) 加糖和牛奶



茶冲泡方法

(1) 把水煮沸

(2) 用沸水冲泡茶叶

(3) 把茶水倒进杯子里

(4) 加柠檬

### 快速实现

Coffee.h

```c++
#pragma once
class Coffee {
public:
	void prepareRecipe();
	void boilWater();
	void brewCoffeeGrinds();
	void pourInCup();
	void addSugarAndMilk();
	Coffee(void);
};
```

Coffee.cpp

```C++
#include "Coffee.h"
#include <iostream>

void Coffee::prepareRecipe(){
	boilWater();
	brewCoffeeGrinds();
	pourInCup();
	addSugarAndMilk();
}
void Coffee::boilWater(){
	std::cout<< "Boiling water"<<std::endl;
}
void Coffee::brewCoffeeGrinds(){
	std::cout<< "Dripping Coffee through filter"<<std::endl;
}
void Coffee::pourInCup(){
	std::cout<<"Pouring into cup"<<std::endl;
}
void Coffee::addSugarAndMilk(){
	std::cout<<"Adding Sugar and Milk"<<std::endl;
}
```

Tea.h

```c++
#pragma once
class Tea {
public:
	void prepareRecipe();
	void boilWater();
	void steerTeaBag();
	void pourInCup();
	void addLemon();
};
```

Tea.cpp

```c++
#include "Tea.h"
#include <iostream>

void Tea::prepareRecipe(){
	boilWater();
	steerTeaBag();
	pourInCup();
	addLemon();
}
void Tea::boilWater(){
	std::cout<< "Boiling water"<<std::endl;
}
void Tea::steerTeaBag(){
	std::cout<< "Steeping the tea"<<std::endl;
}
void Tea::pourInCup(){
	std::cout<<"Pouring into cup"<<std::endl;
}

void Tea::addLemon(){
	std::cout<<"Adding Lemon"<<std::endl;
}
```



这两个类的实现很像，存在很多的重复代码，怎样设计一个通用的基类来删除这些重复代码

### 第一版抽象

将共同方法抽象出来

步骤如下

- 把水煮沸
- 用热水泡咖啡和茶
- 把饮料到进杯子
- 在饮料中加入适当的调料


```c++
void prepareRecipe(){
	boilWater();
	brewCoffeeGrinds();  / steepTeaBag();
	pourInCup();
	addSugarAndMilk();  /  addLemon();
}
```

### 抽象共同的方法

```c++
void prepareRecipe(){
	boilWater();
	brew();
	pourInCup();
	addConditions();
}
```


### 定义模板方法

**模板方法模式** 在一个方法中定义一个算法骨架，而将一些步骤延迟到子类中。模板方法使得子类可以在不改变算法的结构情况下，重复定义算法中的某些步骤。

###解决方案

#### 抽象基类

CaffeineBeverage.h

```c++
#pragma once
class CaffeineBeverage {
public:
    void prepareRecipe();
private:
    virtual void brew() = 0;
    virtual void addCondiments() = 0;
    void boilWater();
    void pourInCup();
    virtual bool customerWantsCondiments(); 
};  
```

CaffeineBeverage.cpp

```c++
#include "CaffeineBeverage.h"
#include <iostream>
void CaffeineBeverage::prepareRecipe() {
    boilWater();
    brew();
    pourInCup();
    if (customerWantsCondiments()){
        addCondiments();
    }
}

void CaffeineBeverage::boilWater(){
    std::cout<<"把水煮沸" << std::endl;
}

void CaffeineBeverage::pourInCup() {
    std::cout<<"倒入杯子中"<<std::endl;
}

bool CaffeineBeverage::customerWantsCondiments() {
    return true;
}
```

#### Tea

Tea.h

```c++
#pragma once
#include "CaffeineBeverage.h"
class Tea : public CaffeineBeverage {
private:
    void brew() override;
    void addCondiments() override;
    bool customerWantsCondiments() override;
};
```

Tea.cpp

```c++
#include "Tea.h"
#include <iostream>
bool Tea::customerWantsCondiments(){
    char zAnswer;
    std::cout<<"您的茶中是否需要柠檬：";
    fflush(stdin);
    std::cin>>zAnswer;
    zAnswer = toupper(zAnswer);
    if ('Y'==zAnswer){
        return true;
    }
    else if ('N'==zAnswer){
        return false;
    }
    else{
        std::cout<<"输入错误，默认不加调料"<<std::endl;
        return false;
    }
}
```



#### Coffee

Coffee.h

````c++
#pragma once
#include "CaffeineBeverage.h"
class Coffee : public CaffeineBeverage {
private:
    void brew() override;
    void addCondiments() override;
    bool customerWantsCondiments() override;
};
````

Coffee.cpp

```c++
#include "Coffee.h"
#include <iostream>

void Coffee::brew() {
    std::cout<<"用沸水冲泡咖啡粉"<<std::endl;
}

void Coffee::addCondiments() {
    std::cout<<"加糖和牛奶"<<std::endl;
}

bool Coffee::customerWantsCondiments() {
    char zAnswer;
    std::cout<<"您的咖啡中是否需要牛奶和糖：";
    std::cin>>zAnswer;
    zAnswer = toupper(zAnswer);
    if ('Y'==zAnswer) {
        return true;
    }
    else if ('N'==zAnswer) {
        return false;
    }
    else {
        std::cout<<"输入错误，默认不加调料"<<std::endl;
        return false;
    }
}
```

#### 测试

main.cpp

```c++
#include "Tea.h"
#include "Coffee.h"

int main() {
    Coffee coffee;
    Tea tea;
    coffee.prepareRecipe();
    tea.prepareRecipe();
    return 0;
}
```

#### 输出结果

```
准备煮咖啡
把水煮沸
用沸水冲泡咖啡粉
倒入杯子中
您的咖啡中是否需要牛奶和糖：y
加糖和牛奶

准备泡茶
把水煮沸
用沸水浸泡茶叶
倒入杯子中
您的茶中是否需要柠檬：y
加柠檬
请按任意键继续. . .
```



## 总结

设计模式看起来是代码复杂化了，但是更易于维护和阅读；

设计模式不是让你染上模式病，不是要写一个hello world 的程序就要想应该使用哪种模式；

设计模式是重构的指导方向；

过度使用设计模式可能导致代码被过度工程化。应该总是使用最简单的解决方案完成工作，并在真正需要模式的地方使用它；

设计模式只是软件工程师总结的一套设计规范，我们也可以自己创建自己的模式；

## 涉及到的C++知识

1. 构造函数和析构函数
2. public, private, protected
3. this 指针
4. 虚函数
5. 纯虚函数
6. 静态成员函数
7. 多态


##资料

《设计模式--可复用面向对象软件的基础》—— C++ 版  ----权威

《Head First 设计模式》 ——Java版    -----推荐这本

《大话设计模式》 ——Java版
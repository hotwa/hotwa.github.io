---
title: python类
categories: 类
type: categories
date: 2021-01-07 10:25:49
tags:
 - 高级特性
 - python
---

# python类

1. 普通类继承object
2. 抽象基类继承abc

---



# 高级特性

`构造函数`

> 构造函数不同于普通方法的地方在于，将在对象创建后**自动调用**它们。

`构造函数内置方法`

`__init__`: add some varvale in function

`__del__`:destructor, 析构函数。这个方法在对象被销毁（作为垃圾被搜集）前被调用。

## 重写普通方法和特殊的构造函数

在子类中重写了构造函数（在子类中重新初始化了内部变量`__init__`，导致在子类中不含有超类（父类）中内置属性），则无法调用超类中的方法是出现报错。

---

# self，cls，staticmethod，classmethod

> 例子

```python
class Person:
    belong_to = 'earthman'
    def __init__(self,skin, name):
        self.skin = skin
        self.name = name
    def get_skin(self):
        return self.skin
        
    @classmethod
    def menthod_cls(cls):
        print(f'{cls},hello，{Person.belong_to}')
        
    @staticmethod
    # 减少实例化对象的开销，如果方法没有用到实例化的任何属性和方法，推荐使用静态类方法
    # 属于类的方法放到类里面，利于组织代码，容易阅读。
    def menthod_state():
        print(f'hello，{Person.belong_to}')
        
lm = Person('yellow', '李明')
print(lm.get_skin())
print(Person.menthod_cls())
print(lm.menthod_cls())
print(Person.menthod_state())

# cls和self有什么特点
# 类的方法，第一个参数必须是self或者是cls（必须用classmethod装饰），这是一种约定。
# cls，表示的是类本身，self表示实例化具体对象的本身。好比说在解析器执行代码的时候，具体的Person类也是一个对象，cls是Person的引用。slef就是lm对象的引用。
```

@classmethod，第一个参数必须是cls，类方法，**可以来调用类的属性，类的方法，实例化对象**等，避免硬编码。比如上面使用类.方法()，实例化.方法()效果是一样的。**重构类的时候不必要修改构造函数，只需要额外添加你要处理的函数（使用场景）。**我在看scrapy代码中发现不少这类型的方法，现在想来确实是用在重构中多些，之前还看不懂。

```python
lm = Person('yellow', '李明')
lm.get_skin()#类成员方法
#也可以这样使用,一样能用
Person.get_skin(lm)
```

lm现在是一个具体叫李明的人，那么在调用Person成员方法的时候，会隐式传递lm对象给get_skin()，也就是self。那为什么非要把self写到方法中？在官方python文档有解释：

在python中没有局部变量声明，加self就可以表示本实例化的变量/方法。**可以理解成类里面的全局变量**,局部变量和实例变量存在于两个不同的命名空间中，您需要告诉 Python 使用哪个命名空间。

那么对于cls参数其实也类似，必须告诉调用的方法，具体的类名，通过cls传递类对象进行调用。在重构的时候，也用得着。

## classmethod

1--classmethod设计的目的是什么呢？

事实上与Python面向对象编程有关的，由于Python不支持多个的參数重载构造函数，比方在C++里，构造函数能够依据參数个数不一样。能够写多个构造函数。Python为了解决问题，採用classmethod修饰符的方式，这样定义出来的函数就能够在类对象实例化之前调用这些函数，就相当于多个构造函数，解决多个构造函数的代码写在类外面的问题。

 

2---类最基本的作用是实例化出一个对象，但是有的时候再实例化之前，就需要先和类做一定的交互，这种交互可能会影响实际实例化的过程，所以必须放在调用构造函数之前。大概也可能是因为这个原因出现了classmethod

 

3---直接一点来说，我们知道对于一个普通的类，我们要使用其中的函数的话，需要对类进行实例化，而一个类中，某个函数前面加上了staticmethod或者classmethod的话，那么这个函数就可以不通过实例化直接调用，可以通过类名进行调用的

 

4---@classmethod 定义的类方法是可选构造函数中，我们定义了一个类方法，类方法的**第一个参数(cls)指代的就是类本身**。**类方法会用这个类来创建并返回最终的实例。**使用类方法的另一个好处就是在继承的时候，保证了**子类使用可选构造函数构造出来的类是子类的实例而不是父类的实例**。
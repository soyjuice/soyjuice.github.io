---
layout: post
title: Python学习日记2
categories: [Python, 学习笔记]
description: 新文章
mini-description: 虽然说是day几day几，但我其实并不是连续几天在学。
keywords: Python
---

### Python学习日记/SoyJuice

#### DAY3 面向对象

1.把一组数据结构和处理它们的方法组成对象（object），把相同行为的对象归纳为类（class），通过类的封装（encapsulation）隐藏内部细节，通过继承（inheritance）实现类的特化（specialization）和泛化（generalization），通过多态（polymorphism）实现基于对象类型的动态分派。

*2.上面这个东西在我的理解之中就是指，对象是一组数据和其相关函数，是具体的，而类是这些相似的对象的集合，是抽象的，举个例子，比如说`SoyJuice-20yearsold`就是一个对象，而`name-age`就是这些对象所归纳的类（`class`）。

*3.面向对象编程是一种思想，有三大要素：封装，继承以及多态

4.

##### 类

在Python中可以使用`class`关键字定义类，然后在类中通过之前学习过的函数来定义方法，这样就可以将对象的动态特征描述出来，代码如下所示。

```Python
class Student(object):

    # __init__是一个特殊方法用于在创建对象时进行初始化操作
    # 通过这个方法我们可以为学生对象绑定name和age两个属性
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def study(self, course_name):
        print('%s正在学习%s.' % (self.name, course_name))

    # PEP 8要求标识符的名字用全小写多个单词用下划线连接
    # 但是部分程序员和公司更倾向于使用驼峰命名法(驼峰标识)
    def watch_movie(self):
        if self.age < 18:
            print('%s只能观看《熊出没》.' % self.name)
        else:
            print('%s正在观看岛国爱情大电影.' % self.name)
            
    # 上面的属性具体就是（对象的）数据，而这些函数就是（对象的）方法
```

*5.封装在我的理解之中就是，将类代码封装（隐藏）起来，无法直接看到代码实现的内容，只需要知道相关方法使用方法即可，就类似于那些自带的数据结构，只能或者说只需要知道如何使用，而不需要知道如何实现。

#### DAY4 面向对象

1.对象中受到保护的属性，可以设为私有属性，使用`__`（双`_`）前缀表示为私有，无法直接访问（实际上这也可用另外的方法去访问，这里暂且不提），但这也会导致子类无法访问，并且在Python编程中开放往往是比封闭要好的；综上，使用一个折中的办法，使用单`_`前缀表示属性是受到保护的，这没有实际上的影响，只是一个标记，意味着编程者在编程时需要慎重使用、修改这些属性。

2.

##### `@property`装饰器

考虑到上述有关属性受保护程度的考虑，为了防止出现直接开放所可能造成的问题，可以使用`@property`装饰器来包装getter（访问器）和setter（修改器）

```Python
class Person(object):

    def __init__(self, name, age):
        self._name = name
        self._age = age

    # 访问器 - getter方法 ：使得可以使用.name访问._name
    @property
    def name(self):
        return self._name

    # 访问器 - getter方法 ：使得可以使用.age访问._age
    @property
    def age(self):
        return self._age

    # 修改器 - setter方法 ：使得可以通过修改.age从而修改._age
    @age.setter
    def age(self, age):
        self._age = age

    def play(self):
        if self._age <= 16:
            print('%s正在玩飞行棋.' % self._name)
        else:
            print('%s正在玩斗地主.' % self._name)


def main():
    person = Person('王大锤', 12)
    person.play()
    person.age = 22
    person.play()
    # person.name = '白元芳'  # AttributeError: can't set attribute


if __name__ == '__main__':
    main()
```

3.

##### `__slots__`关键字

使用`__slots__`关键字可以约束当前类（无法约束子类）的属性，确定此类只有这些属性，还可以节省内存大小（Python貌似是用字典存储属性和值，固定属性数量可以有效减少内存占用）

```python
class Person(object):
    
    __slots__ = ('_name', '_age', '_gender')
    
    pass
```

4.

##### 静态方法和类方法

类中直接定义的方法往往是以对象为主体，而如果想以类为主体定义方法，那么可以使用`@staticmethod`和`@classmethod`定义

```python
class Dio(object):
    
    @staticmethod
    def f1():
        return 1
    
    @classmethod
    def f2(cls):
        return cls.f1()


def main():
    print(Dio.f2()) # 1


if __name__ == '__main__':
    main()
```

可以看出静态方法不能再与当前类相关，就只是个函数，而类方法还可以用第一个参数`cls`（约定俗成的，跟常规方法第一个参数约定为`self`一样）获取和类相关的信息并且可以创建出类的对象

*5.类的本身也是一个对象，又称为类的元数据对象。

*6.简单的说，类和类之间的关系有三种：is-a、has-a和use-a关系。

- is-a关系也叫继承或泛化，比如学生和人的关系、手机和电子产品的关系都属于继承关系。
- has-a关系通常称之为关联，比如部门和员工的关系，汽车和引擎的关系都属于关联关系；关联关系如果是整体和部分的关联，那么我们称之为聚合关系；如果整体进一步负责了部分的生命周期（整体和部分是不可分割的，同时同在也同时消亡），那么这种就是最强的关联关系，我们称之为合成关系。
- use-a关系通常称之为依赖，比如司机有一个驾驶的行为（方法），其中（的参数）使用到了汽车，那么司机和汽车的关系就是依赖关系。

7.

##### 类的继承

在已有类的基础上创建新类，这其中的一种做法就是让一个类从另一个类那里将属性和方法直接继承下来，从而减少重复代码的编写。提供继承信息的我们称之为父类，也叫**超类**或基类；得到继承信息的我们称之为子类，也叫派生类或衍生类。子类除了继承父类提供的属性和方法，还可以定义自己特有的属性和方法，所以子类比父类拥有的更多的能力

```Python
class Person(object):
    """人"""

    def __init__(self, name, age):
        self._name = name
        self._age = age

    @property
    def name(self):
        return self._name

    @property
    def age(self):
        return self._age

    @age.setter
    def age(self, age):
        self._age = age

    def play(self):
        print('%s正在愉快的玩耍.' % self._name)

    def watch_av(self):
        if self._age >= 18:
            print('%s正在观看爱情动作片.' % self._name)
        else:
            print('%s只能观看《熊出没》.' % self._name)


class Student(Person): # 注意此处object替换为父类的名字
    """学生"""

    def __init__(self, name, age, grade):
        super().__init__(name, age) 
        # super()取自超类一词，直接取用父类的方法
        self._grade = grade

    @property
    def grade(self):
        return self._grade

    @grade.setter
    def grade(self, grade):
        self._grade = grade

    def study(self, course):
        print('%s的%s正在学习%s.' % (self._grade, self._name, course))


class Teacher(Person):
    """老师"""

    def __init__(self, name, age, title):
        super().__init__(name, age)
        self._title = title

    @property
    def title(self):
        return self._title

    @title.setter
    def title(self, title):
        self._title = title

    def teach(self, course):
        print('%s%s正在讲%s.' % (self._name, self._title, course))


def main():
    stu = Student('王大锤', 15, '初三')
    stu.study('数学')
    stu.watch_av()
    t = Teacher('骆某', 38, '砖家')
    t.teach('Python程序设计')
    t.watch_av()


if __name__ == '__main__':
    main()
```

8.

##### 类的多态

子类在继承了父类的方法后，可以对父类已有的方法给出新的实现版本，这个动作称之为方法重写（override）。通过方法重写我们可以让父类的同一个行为在子类中拥有不同的实现版本，当我们调用这个经过子类重写的方法时，不同的子类对象会表现出不同的行为，这个就是多态（poly-morphism）

```Python
from abc import ABCMeta, abstractmethod


class Pet(object, metaclass=ABCMeta):

    def __init__(self, nickname):
        self._nickname = nickname

    @abstractmethod
    def make_voice(self):
        pass


class Dog(Pet):

    def make_voice(self):
        print('%s: 汪汪汪...' % self._nickname)


class Cat(Pet):

    def make_voice(self):
        print('%s: 喵...喵...' % self._nickname)


def main():
    pets = [Dog('旺财'), Cat('凯蒂'), Dog('大黄')]
    for pet in pets:
        pet.make_voice()


if __name__ == '__main__':
    main()
```

上面的代码中，`Dog`和`Cat`两个子类分别对`Pet`类中的`make_voice`抽象方法进行了重写并给出了不同的实现版本，当我们在`main`函数中调用该方法时，这个方法就表现出了多态行为（同样的方法做了不同的事情）；而所谓抽象类就是不能够创建对象的类（不使用抽象类照样可以达成多态的效果，只不过`Pet`类的使用可能会出现其他问题），这种类的存在就是专门为了让其他类去继承它，Python从语法层面并没有像Java或C#那样提供对抽象类的支持，但是我们可以通过`abc`模块的`ABCMeta`元类和`@abstractmethod`包装器来达到抽象类的效果，如果一个类中存在抽象方法那么这个类就不能够实例化（创建对象），注意，这两者达成此效果是and的关系。

*9.顺着继承树向上，我们可以知道，一切对象的顶层是type，一切类的顶层是object，这两者既是对象，亦是类，object对象是由type类创建，type类的父类是object类，type是object的类型，她们是一切的造物主，是一切的主宰。

关于这俩的关系，比较抽象，不过查看文档之后可以有一个比较直观的看法：

```python
class object
 |  The most base type
# 描述甚至只有一句，可能object就像是一个空类，专为继承顶点而设置的


class type(object)
 |  type(object_or_name, bases, dict)
 |  type(object) -> the object's type
 |  type(name, bases, dict) -> a new type
 |
 |  Methods defined here:
 |
 |  __call__(self, /, *args, **kwargs)
 |      Call self as a function.
 |
 |  __delattr__(self, name, /)
 |      Implement delattr(self, name).
 |
 |  __dir__(self, /)
 |      Specialized __dir__ implementation for types.
 |
 |  __getattribute__(self, name, /)
 |      Return getattr(self, name).
 |
 |  __init__(self, /, *args, **kwargs)
 |      Initialize self.  See help(type(self)) for accurate signature.
 |
 |  __instancecheck__(self, instance, /)
 |      Check if an object is an instance.
 |
 |  __repr__(self, /)
 |      Return repr(self).
 |
 |  __setattr__(self, name, value, /)
 |      Implement setattr(self, name, value).
 |
 |  __sizeof__(self, /)
 |      Return memory consumption of the type object.
 |
 |  __subclasscheck__(self, subclass, /)
 |      Check if a class is a subclass.
 |
 |  __subclasses__(self, /)
 |      Return a list of immediate subclasses.
 |
 |  mro(self, /)
 |      Return a type's method resolution order.
 |
 |  ----------------------------------------------------------------------
 |  Class methods defined here:
 |
 |  __prepare__(...)
 |      __prepare__() -> dict
 |      used to create the namespace for the class statement
 |
 |  ----------------------------------------------------------------------
 |  Static methods defined here:
 |
 |  __new__(*args, **kwargs)
 |      Create and return a new object.  See help(type) for accurate signature.
 |
 |  ----------------------------------------------------------------------
 |  Data descriptors defined here:
 |
 |  __abstractmethods__
 |
 |  __dict__
 |
 |  __text_signature__
 |
 |  ----------------------------------------------------------------------
 |  Data and other attributes defined here:
 |
 |  __base__ = <class 'object'>
 |      The most base type
 |
 |  __bases__ = (<class 'object'>,)
 |
 |  __basicsize__ = 864
 |
 |  __dictoffset__ = 264
 |
 |  __flags__ = -2146675712
 |
 |  __itemsize__ = 40
 |
 |  __mro__ = (<class 'type'>, <class 'object'>)
 |
 |  __weakrefoffset__ = 368
```

**我的理解**，object是type类型的，而具体描述type的类是从object继承而来的；object像是名义上的王，实际上是type具体落实了object的统治，两者是**概念上**相辅相成的关系，我觉得这俩没啥实际的影响，也就不继续深入理解了。
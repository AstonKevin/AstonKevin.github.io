+++
date = '2026-07-25T16:13:57+08:00'
draft = false
title = 'OOP Summary'
+++
## 面向对象编程--总结
这一周学完了廖雪峰老师的python章节中面向对象章节的知识点，今天写一份博客总结一下，会有许多可能不太对的地方，还请大家指正
## 01
我个人觉得在面向对象这一章节中，最重要的一点就是类的概念，最突出的一点就是类将方法和属性绑定在了一起，每个类都有自己的属性和方法，通过类创建的对象称之为实例，面向对象编程，我们要思考的是将数据类型看成一个类，而不是程序的运行过程，之前学C++的时候感觉就是这样，C对于python来说更接近底层，所以说许多很多程序都要从本身出发，也就是面向过程，emmm，其实说实话，我到现在还没有完全get面向对象的精髓吧，我的能力还是太弱了。面向对象编程的最主要的特性：数据封装，继承，多态
## 数据封装
哦对，刚刚说的类，每一个类都要有自己的__init__方法进行初始化，可以在__init__方法中传入参数，第一个参数永远都是self，也就是实例本身，有了__init__，传入的参数就有要求了
```python
class Student(object):
    def __init__(self,name,sex):
        self.name = name
        self.sex = sex
    

s1 = Student("kevin") # 这样在创建一个实例中就必须传入对应的参数
```
接下来就是数据封装部分，这一部分我理解的还可以，在原本的类中，如果我要访问类中的变量，就可以不再通过外部的函数进行访问，而是可以通过函数封装到类的内部，这样用户就可以不知道类的内部实现细节，还可以增加新的方法
```python
class Student(object):
    def __init__(self,name,sex):
        self.name = name
        self.sex = sex
    
    def print_score(self):
        print(f'score:{self.score}')
    

```
python是一个动态语言，这也就允许了可以让实例绑定任何数据，就比如说我可以定义一个s1之后，给它定义一个age方法，但是定义的s2却没有这个方法
## 访问限制
这一部分掌握的还可以，访问限制的目的是什么呢，在类中，当我们做出一个实例之后呢，可以调用实例中的方法和属性，但是同时呢，也可以直接进行修改，为了避免这一种情况，就出现了访问限制，通过给内部属性加下划线，就会变成私有变量，这样的话就可以只能内部访问，外部不可以访问：
```python
class Student(object):
    def __init__(self,name,sex):
        self._name = name
        self._sex = sex
    
    def print_score(self):
        print(f'score:{self._score}')
    

```
变成这样之后呢，可以通过定义get，set方法来得到，修改属性值
```python
class Student(object):
    def __init__(self,name,sex,score):
        self._name = name
        self._sex = sex
        self._score = score
    
    def print_score(self):
        print(f'score:{self._score}')
    
    def getscore(self):
        return self._score

    def setscore(self,score):
        self._score = score
```
于此同时，通过set，get还可以对参数进行检查
## 继承、多态
这一部分中，继承比较好理解，就是子类可以继承父类，子类的方法可以重写父类的方法，通过isinstance方法可以发现，子类其实也是父类的类型，但是父类不是子类的类型，至于多态，是这样的，比如说我们先定义一个大类
```python
class Animal(object):
    def __init__(self,name,kind,sound):
        self._name = name
        self._kind = kind
        self._sound = sound
    def run(self):
        print(f"run")
    #然后定义一个子类
class Dog(Animal):
    def run(self):
        print("dog is running")
    #然后定义一个函数，接收类

def run_twice(animal):
    animal.run()
    animal.run()

```
通过这样，我们在run_twice函数中，无论我们传入的是什么类型的，无论是父类，还是各种其他继承的类，只要继承中存在run方法，就可以被调用，在廖雪峰老师中，他是这么说的：对拓展开放，对修改封闭，没错，就是这样，因此也引入了下面一部分：静态语言和动态语言。动态语言就是不要特定的类型，我们只要这个类型中存在run方法，那么就可以实现，即“鸭子类型”，看着像鸭子，那么他就是鸭子🤔
## 获取对象信息
这一部分非常简单呀，感觉已经狠狠拿捏了，type函数，isinstance函数，dir函数
```python
type("string")
isinstance(dog,Dog)#返回true/false
dir(Dog)#返回所有的对象方法
```
## 总结
今天第一次写这么多，心里面也是非常有成就感，希望自己不断进步，加油


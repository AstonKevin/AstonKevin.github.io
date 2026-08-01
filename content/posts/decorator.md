+++
date = '2026-08-01T09:44:22+08:00'
draft = false
title = 'Decorator'
+++
## 今天是建军节，81快乐！
## 装饰器--总结
装饰器是python中挺重要的一部分，最主要的功能就是在不修改原本函数的前提下，动态的给函数增加新的功能。
## 01
首先，要明白的一点就是，函数也是一个对象，而对象可以赋值给一个变量，因此可以通过变量调用函数。而且每一个函数都有都有各自的属性，可以调用.调用各自的属性。
```python
def now():
    print('2026-8-1')
f = now
print(f())
print(f.__name__)
print(now.__name__)
##这里会打印出'now'
```
## 02
其次呢就是装饰器，动态的给函数增加新的功能，就比如说我们现在要给now函数增加一个新的功能，在调用函数的同时呢，使用函数本身的__name__属性。
```python
def log(func):
    def wrapper(*args,**kw):
        print('function name:%s'%func.__name__)
        return func(*args,**kw)
    return wrapper

@log
def now():
    print('2026-8-1')
#运行
now()
```
```bash
function name:now
2026-8-1
```
我们先进行分析，首先，当@log在now函数定义的上方时，等同于：now = log(now)，首先，先在log函数中传入now函数作为形参，然后程序进入log函数内部，返回wrapper函数，然后再进入wrapper函数，注意wrapper函数接受的参数是*args，**kw，（这两个分别代表arguments和key word arguments，代表位置参数和关键字参数），这个wrapper包装函数类似于把所有的参数都可以传进来，替换原来的func，然后再wrapper内部打印__name__属性，最后再原样返回func，就可以理解为一个中间商，把传入的参数进行修改，然后再次返回。
## 03
那如果装饰器本身需要传入参数怎么办，这里就要进行一个三层的高阶函数：
```python
def log(text):
    def decorator(func):
        def wrapper(*args,**kw):
            print('text:%s,function name:%s'%(text,func.__name__))
            return func(*args,**kw)
        return wrapper
    return decorator

@log('kevin')
def now():
    print('2026-8-1')
#调用
now()
```
```bash
text:kevin,function name:now
2026-8-1
```
我们进行分析，当log定义再now函数上方时，相当于：now = log('kevin')(now)，先进行log('kevin')，这里先返回decorator函数，然后进入decorator内部，变成now = decorator(now)，然后返回wrapper函数，再次进入wrapper函数内部，下面的部分就是和之前一样。
## 04
但是这里呢，有一个弊端，当我们用decorator装饰之后呢，我们尝试进行如下操作：
```python
print(now.__name__)
```
```bash
wrapper
```
我们可以看到，经过wrapper包装之后，函数的__name__变成了wrapper，如果要修改回来，完整的装饰器内容如下，要加入python中内置的functools.wraps。
```python
import functools

def log(func):
    @functools.wraps(func)
    def wrapper(*args, **kw):
        print('call %s():' % func.__name__)
        return func(*args, **kw)
    return wrapper
```
对于带参数的装饰器
```python
import functools

def log(text):
    def decorator(func):
        @functools.wraps(func)
        def wrapper(*args, **kw):
            print('%s %s():' % (text, func.__name__))
            return func(*args, **kw)
        return wrapper
    return decorator
```
## 05 
ok呀，这一部分也算是明白了，自我感觉掌握的还可以，加油加油



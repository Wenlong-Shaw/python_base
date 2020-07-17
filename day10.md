# day10

## 1、设计一个类，实例化两个对象，然后小明跑步跑完步，会去吃东西，小美不跑步，小美喜欢吃东西

* **小明** 今年 **18 岁**，**身高 1.75**，每天早上 **跑** 完步，会去 **吃** 东西
* **小美** 今年 **17 岁**，**身高 1.65**，小美不跑步，小美喜欢 **吃** 东西


```python
class Person(object):     # 当被定义的类没有继承的父类时，类名后的括号应写 object 。
# class Person:            # 也可以不要 (object) 直接这样定义： class Person:

# python定义了一些“内置方法”（方法以双下划线__ __包住的）

    # 对象的初始化应该把对象的属性封装在对象的内部。
    # 也可以定义一些缺省属性。
    def __init__(self, name, age, height, house=None):
        self.name = name
        self.age = age
        self.height = height
        self.house = house
        

    # 当初始化Person后，print该实例时，会自动显示 __str__ 方法return的字符串。
    # 方便获取一些关于此类实例的信息。
    def __str__(self):    
        return ('My name is '+ self.name +'. '+
    'I am '+ str(self.age) +' year\'s old. '+
    'I am '+ str(self.height) +' meter. '+ 
               'My house is ' + str(self.house))

    # 对象的销毁发生在“程序（函数）的运行结束”（也可以说是在函数内的对象当程序运行离开了这个函数时会销毁）、
    #“对象的`引用计数`为0”、“对象被主动del掉”。
    # 当到达垃圾回收的阈值时，会被回收。
    # 当该实例在内存中被销毁（回收）时，会调用__del__方法。
    def __del__(self):
        print('我被销毁了！')
    
    def run(self):
        if self.name == 'xiaomei':
            print(self.name + ' can not run!')
        else:
            print(self.name + ':' + 'I can run!')
            self.eat()
    
    def eat(self):
        print(self.name + ':' + 'I will eat!')
        
        
xiaoming = Person('xiaoming',18, 1.75)
xiaomei = Person('xiaomei', 17, 1.65)
print(dir(xiaoming))    # 查看该类下的全部方法和属性（包括私有的）。
print(dir(xiaomei))
print(xiaoming)
print(xiaomei)
xiaoming.run()
xiaomei.run()
del(xiaoming)
print('Program is over!')
```

    ['__class__', '__del__', '__delattr__', '__dict__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__le__', '__lt__', '__module__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', '__weakref__', 'age', 'eat', 'height', 'house', 'name', 'run']
    ['__class__', '__del__', '__delattr__', '__dict__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__le__', '__lt__', '__module__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', '__weakref__', 'age', 'eat', 'height', 'house', 'name', 'run']
    My name is xiaoming. I am 18 year's old. I am 1.75 meter. My house is None
    My name is xiaomei. I am 17 year's old. I am 1.65 meter. My house is None
    xiaoming:I can run!
    xiaoming:I will eat!
    xiaomei can not run!
    我被销毁了！
    Program is over!


## 2、设计一个类，实例化1个对象，会实现下面两种行为:

* 需求:
 * 一只 **黄颜色** 的 **狗狗** 叫 **大黄**
 * 具有  **汪汪叫** 行为
 * 具有  **摇尾巴** 行为


```python
class Dog:
    def __init__(self, name, color):
        self.name = name
        self.color = color
        
    def __str__(self):
        return 'this is a ' + str(self.color) + 'dog. '
    
    def shake_tail(self):
        print('The dog shakes tail.')
        
    def bark(self):
        print('The dog barks')


dahuang = Dog('大黄','yellow')
dahuang.bark()
```

    The dog barks


## 3、使用dir查看类里的内容，是否有类属性，是否有对象方法，练习\_\_init\_\_，\_\_str\_\_还有\_\_del\_\_


```python
class Person(object):     # 当被定义的类没有继承的父类时，类名后的括号应写 object 。
# class Person:            # 也可以不要 (object) 直接这样定义： class Person:

# python定义了一些“内置方法”（方法以双下划线__ __包住的）

    # 对象的初始化应该把对象的属性封装在对象的内部。
    # 也可以定义一些缺省属性。
    def __init__(self, name, age, height, house=None):
        self.name = name
        self.age = age
        self.height = height
        self.house = house
        

    # 当初始化Person后，print该实例时，会自动显示 __str__ 方法return的字符串。
    # 方便获取一些关于此类实例的信息。
    def __str__(self):    
        return ('My name is '+ self.name +'. '+
    'I am '+ str(self.age) +' year\'s old. '+
    'I am '+ str(self.height) +' meter. '+ 
               'My house is ' + str(self.house))

    # 对象的销毁发生在“程序（函数）的运行结束”（也可以说是在函数内的对象当程序运行离开了这个函数时会销毁）、
    #“对象的`引用计数`为0”、“对象被主动del掉”。
    # 当到达垃圾回收的阈值时，会被回收。
    # 当该实例在内存中被销毁（回收）时，会调用__del__方法。
    def __del__(self):
        print('我被销毁了！')
    
    def run(self):
        if self.name == 'xiaomei':
            print(self.name + ' can not run!')
        else:
            print(self.name + ':' + 'I can run!')
            self.eat()
    
    def eat(self):
        print(self.name + ':' + 'I will eat!')
        
        
xiaoming = Person('xiaoming',18, 1.75)
xiaomei = Person('xiaomei', 17, 1.65)
print(dir(xiaoming))    # 查看该类下的全部方法和属性（包括私有的）。
print(dir(xiaomei))
print(xiaoming)
print(xiaomei)
xiaoming.run()
xiaomei.run()
del(xiaoming)
print('Program is over!')
```

    ['__class__', '__del__', '__delattr__', '__dict__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__le__', '__lt__', '__module__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', '__weakref__', 'age', 'eat', 'height', 'house', 'name', 'run']
    ['__class__', '__del__', '__delattr__', '__dict__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__le__', '__lt__', '__module__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', '__weakref__', 'age', 'eat', 'height', 'house', 'name', 'run']
    My name is xiaoming. I am 18 year's old. I am 1.75 meter. My house is None
    My name is xiaomei. I am 17 year's old. I am 1.65 meter. My house is None
    xiaoming:I can run!
    xiaoming:I will eat!
    xiaomei can not run!
    我被销毁了！
    Program is over!


## 4、练习私有属性和私有方法


```python
class Human:
    
    def __init__(self, name, age, height, house=None):
        self.name = name
        self.age = age
        self.height = height
        
        #私有属性以双下划线 __ 开头。
        #私有属性外，部不能直接访问。可通过类内方法间接调用。
        #私有方法，外部不能直接调用。可通过类内方法间接调用。
        self.__house = house
    
    def __str__(self):    
        return ('My name is %s . I\'m %d years old. I\'m %f meter high.'%(self.name,self.age,self.height))

    def __del__(self):
        print('我被销毁了！')
    
    #私有属性可以被内部的公有方法调用。
    def tell_house(self):
        print('The house of %s is %s'%(self.name, self.__house))
    
    #私有方法，外部不能直接调用。可通过类内方法间接调用。
    def __secret(self):
        print('This is a secert.')
        
    def tell_secret(self):
        print('call secret method.')
        self.__secret()

        
li = Human('li',18,1.88,house='apartment')

#li.__secret() 私有属性不能直接调用！
#私有方法调用通过内置公有方法
li.tell_secret()

#li.__house 私有属性不能直接调用！
#私有属性调用通过内置公有方法！
li.tell_house()
```

    我被销毁了！
    call secret method.
    This is a secert.
    The house of li is apartment


## 5、练习继承、使用super扩展父类，多重继承

> **继承的概念**
> 
> `子类`拥有`父类`的所有`方法`和`属性`。
> 
> **继承的语法**
>
> class 类名 (父类名)：
>    
> * **子类**继承自**父类**，可以直接享有**父类**中已经封装好的方法和属性，不需要再次开发。
>
>* **子类**中应该根据自身职责，封装**子类特有的属性和方法**。
>
> **继承的传递性**
>
> * C类从B类继承，B类又从A类继承
>
> * 那么C类就具有B类和A类的所有属性和方法
>
> * 当父类的方法不能满足子类的需求，子类可以在自己类域内 **重写(override)** 父类属性。
>
>  * 重写父类的方法有两种：
>    1. **覆盖**父类的方法。
>> (即直接在子类中重新写一个和父类同名的方法，把父类的方法覆盖掉。这样通过`子类名.方法名`这样调用时，
>> 就优先调用的是子类的方法，而不是父类中同名的方法。)
>    2. 对父类的方法进行**扩展**。
>> 扩展就是在**子类的方法实现中包含对原有父类方法的实现**（或者说父类封装的方法是子类的方法的一部分）。
>>
>> 实现扩展的方式：
>> 1. 在子类中重写父类的方法。
>> 2. 在需要的位置使用super().父类方法来调用父类方法的执行
>> 3. 代码其他的位置针对子类的需求，编写子类特有的代码实现



```python
class Animal:
    def fly(self):
        print('I can fly!')
    
    def run(self):
        print('I can run!')
        
    def eat(self):
        print('I can eat!')
    
    def bark(self):
        print('I can bark!')

        
class Dog(Animal):
    
    def bark1(self):
        #调用父类公有方法可以`父类名.方法名(self)`的方式。
        #也可以是`super().方法名`的方式。
        Animal.bark(self)
        print('bark1: wang!wang!wang!')
        
    def bark2(self):
        #super().bark()调用父类的公有方法。
        #但是super().__secret()不能直接调用父类的私有方法。
        super().bark()
        print('bark2: wang!wang!wang!')

class Cute:
    def cute_bark(self):
        print('ao~~~wu~~~')

#开发中尽量避免使用多继承中各个父类中存在同名的类方法的情况，避免混肴。        
class Samoyed(Dog, Cute):
    def samoyed_bark(self):
        
        #继承也可以传递。用super来引用父类的父类的方法。
        super().bark()
        #多重继承
        Cute.cute_bark(self)
        
hashiqi = Dog()
hashiqi.bark1()
hashiqi.bark2()
abai = Samoyed()
abai.samoyed_bark()

#当不清楚类的继承的方法调用顺序时，
#使用 类名.__mro__ 调用mro基属性，
#(注意是类名.__mro__，不是初始化的类变量名)
#来查看所看多继承类的父类引用顺序。
print(Samoyed.__mro__)    #其可以看出其引用优先顺序是基于深度遍历的顺序（最后引用的是object类中的方法）。
```

    I can bark!
    bark1: wang!wang!wang!
    I can bark!
    bark2: wang!wang!wang!
    I can bark!
    ao~~~wu~~~
    (<class '__main__.Samoyed'>, <class '__main__.Dog'>, <class '__main__.Animal'>, <class '__main__.Cute'>, <class 'object'>)


## 6、练习类属性


```python
class Human:
    
    __personInfo = {}
    
    #实例属性，在初始化的时候自动实例化。
    def __init__(self, name, age, height, house=None):
        self.name = name
        self.age = age
        self.height = height
        self.__house = house
        
    
    def call_house(self):
        return self.__house
    
    def add_personInfo(self,name,age):
        self.__personInfo.update({name:age})
    
    def show_personInfo(self):
        return self.__personInfo
        
class Chinese(Human):
    
    def __init__(self, name, age, height, skinColor,house=None):

        self.__skinColor = skinColor
        self.name = name
        self.age = age
        self.height = height
        self.__house = house
        self.add_personInfo(name,age)

    
    def __str__(self):
        return ('''
        name: %s\n
        age: %d\n
        height: %f\n
        skincolor: %s\n
        house: %s'''%(self.name, self.age, self.height, self.__skinColor, self.__house))
        

xiaoli = Chinese('xiaoli', 20, 1.77,'yellow')
xiaohong = Chinese('xiaohong',22,1.68,'yellow')
print(xiaoli)
print(type(xiaoli))

print(xiaoli.show_personInfo())
```


            name: xiaoli
    
            age: 20
    
            height: 1.770000
    
            skincolor: yellow
    
            house: None
    <class '__main__.Chinese'>
    {'xiaoli': 20, 'xiaohong': 22}


# 难度作业
_____

> 设计植物大战僵尸游戏的类，用好，封装，继承，多态，有时间写一个循环，不同的对象依次被创建，自动打游戏，当然也可以通过输入命令窗口打游戏


```python

```

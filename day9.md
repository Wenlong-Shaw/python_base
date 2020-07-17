# day9
----

## 1、函数的简单入参练习


```python
def test_rucan(num, numList):
    print('已进入test_rucan函数内')
    print(id(num),id(numList))   # 此时传入函数的参数还没有被赋值，或者被重写，所以地址依然是传入前地址（写时复制机制Copy-on-write）
    num += 1    # num被赋值（重写），此时函数内num参数指向的地址已改变。
    numList.append(num)
    print(num, numList)
    print(id(num),id(numList))
    return print('test_rucan函数执行完毕')


num = 4
numList = [1,2,3]
print(id(num),id(numList))
test_rucan(num,numList)
print(num,numList)      
print(id(num),id(numList))    # numList被修改后的地址未发生变化，说明是引用传入。
                               # 而num是不可变类型所以函数内部修改不会改变传入前外部的
                               # num的地址，故num（不可变变量）在函数内被修改不会影响其外部值。
```

    140714168709488 2690289633096
    已进入test_rucan函数内
    140714168709488 2690289633096
    5 [1, 2, 3, 5]
    140714168709520 2690289633096
    test_rucan函数执行完毕
    4 [1, 2, 3, 5]
    140714168709488 2690289633096


## 2、函数可变类型列表，字典入参练习，在函数内改变列表，字典内容后，函数外打印显示发生改变


```python
def test_rucan(d, numList):
    print('已进入test_rucan函数内')
    print(id(d),id(numList))   # 此时传入函数的参数还没有被赋值，或者被重写，所以地址依然是传入前地址（写时复制机制Copy-on-write）
    d.popitem()    
    numList.pop()
    print(d, numList) 
    print(id(d),id(numList))    # d和numList调用的是自己的方法来修改，修改后值变、地址不变。
    d = {"test":"测试", "score":100}    # d被赋值（重写），此时函数内d参数指向的地址已改变。
    numList += 'end'    # 相当于将'end'字符串的每个字符append进入numList
    print(d, numList)    # 此时的numList的地址不变，d的地址变化
    print(id(d),id(numList))    
    numList = ["end",'star']    # numList被赋值（重写），此时函数内d参数指向的地址已改变。
    print(d, numList)         
    print(id(d),id(numList))
    return print('test_rucan函数执行完毕')


d = {"name":"wangdachui","age":18, "ginder":"male" }
l = [1,2,3]
print(id(d),id(l))
test_rucan(d,l)
print(d,l)
print(id(d),id(l))    # d，l被修改后的地址未发生变化，说明是引用传入。
```

    2690324338792 2690328650184
    已进入test_rucan函数内
    2690324338792 2690328650184
    {'name': 'wangdachui', 'age': 18} [1, 2]
    2690324338792 2690328650184
    {'test': '测试', 'score': 100} [1, 2, 'e', 'n', 'd']
    2690324337512 2690328650184
    {'test': '测试', 'score': 100} ['end', 'star']
    2690324337512 2690327068744
    test_rucan函数执行完毕
    {'name': 'wangdachui', 'age': 18} [1, 2, 'e', 'n', 'd']
    2690324338792 2690328650184


## 3、多个缺省参数的传递练习，练习多个缺省参数

> **缺省参数**
> * 定义函数时，可以给某个参数指定一个默认值，具有默认值的参数就叫做`缺省参数`
> * 调用函数时，如果没有传入缺省参数的值，则在函数内部使用定义函数时指定的参数默认值
> * 函数的缺省参数，将常见的值设置为参数的缺省值，从而简化函数的调用
> _____
> **缺省参数的注意事项**
> 1. 缺省参数的定义位置
>   * **必须保证**带有默认值的缺省参数在参数列表**末尾**。所以，以下定义是错误的!
>    
>     def print_ info( name, gender=True, title):
>                                        
> 2. 调用带有多个缺省参数的函数
>   * 在调用函数时，如果有多个缺省参数，需要指定参数名，这样解释器才能够知道参数的对应关系!
>   
>     def print_ info( name, title='', gender=True):


```python
def default_para(age, name, personInfo={'name': None, 'age':None}):     
    print('已进入default_para函数内')
    print(id(age),id(name),id(personInfo))   # 此时传入函数的参数还没有被赋值，或者被重写，所以地址依然是传入前地址（写时复制机制Copy-on-write）
    age += 1
    personInfo.popitem()    
    name.center(20)
    print(age,name,personInfo)
    print(id(age),id(name),id(personInfo))    # d和numList用的是自己的方法，地址不变
    print(age, name, personInfo)
    d = {"test":"测试", "score":100}    # d被赋值（重写），此时函数内d参数指向的地址已改变。
    print(age, name, personInfo)
    print(id(age),id(name),id(personInfo))
    return print('default_para函数执行完毕')

age = 18
name = 'Long Bro'
print(id(age),id(name))
default_para(age,name)
print(id(age),id(name))
```

    140714168709936 2690328510384
    已进入default_para函数内
    140714168709936 2690328510384 2690323645848
    19 Long Bro {'name': None}
    140714168709968 2690328510384 2690323645848
    19 Long Bro {'name': None}
    19 Long Bro {'name': None}
    140714168709968 2690328510384 2690323645848
    default_para函数执行完毕
    140714168709936 2690328510384


## 4、可变参数练习，元组，字典的传参拆包练习

> **元组和字典的拆包(知道)**
>
> 1. 在调用带有多值参数的函数时，如果希望:
>   1. 将一个元组变量，直接传递给args
>   2. 将一个字典变量，直接传递给kwargs
> 
> 2. 就可以使用拆包，简化参数的传递，拆包的方式是: 
>   1. 在元组变量前，增加一个*
>   2. 在字典变量前，增加两个*


```python
def test_unpack(num, *args, **kwargs):
    print('-'*10,'已进入函数', '-'*10)
    print(num)
    print(args)
    print(kwargs)
    return print('-'*10,'函数执行完毕返回', '-'*10)

num = 1
t = (1,2,3)
d = {'name':'Long','age':18}

test_unpack(num,*t,**d)

# 对比传入参数时不加拆包符号 *，的输出如何？
test_unpack(num,t,d)    # 不加拆包符号 * ，输出结果往往会吧
```

    ---------- 已进入函数 ----------
    1
    (1, 2, 3)
    {'name': 'Long', 'age': 18}
    ---------- 函数执行完毕返回 ----------


# 难度作业：
--------

## 5、完成名片管理系统


```python

```

## 6、剩余时间做昨天作业，或预习我们的面向对象编程

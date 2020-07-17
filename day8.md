# day8_作业

## 1、把今天讲的列表，元组，字典，字符串的所有接口基本功能练习一遍，并用思维导出总结好（不清楚哪些是基础功能，就是照着上课代码练习一遍）


```python
l = [x for x in range(20)]
print(l)
l.append(20)    #append()在末尾增
print(l)
```

    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19]
    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20]


## 2、列表、元组，字典的相同点，不同点有哪些，请罗列

1. 相同点：
 1. 都是迭代器，都可以迭代内部items。
 2. 都可以索引。
 3. 列表和元组都有count，index方法。

2. 不同点：
  1. 列表和字典是可变类型，元组是不可变类型。
  2. 列表是有序变量，字典是无序的。
  3. 字典通过'键值对'来构成，并且键必须是唯一的；列表和元组则是单个变量元素构成，元素可以重复。


## 3、将元组 (1,2,3) 和集合 {4,5,6} 合并成一个列表。


```python
t = (1,2,3)
s = {4,5,6}
l = []
l.extend(t)
l.extend(s)
print(l)
```

    [1, 2, 3, 4, 5, 6]


## 4、在列表 [1,2,3,4,5,6] 首尾分别添加整型元素 7 和 0。


```python
# 首插 insert，尾添 append
l = [1,2,3,4,5,6]
l.insert(0,7)
l.append(0)
l
```




    [7, 1, 2, 3, 4, 5, 6, 0]



## 5、反转列表 [0,1,2,3,4,5,6,7] 


```python
l = [i for i in range(8)]
l.reverse()
l
```




    [7, 6, 5, 4, 3, 2, 1, 0]



## 6、反转列表 [0,1,2,3,4,5,6,7] 后给出其中元素 5 的索引号。


```python
l = [i for i in range(8)]
l.reverse()
index5 = l.index(5)
index5
```




    2



## 7、分别统计列表 [True,False,0,1,2] 中 True,False,0,1,2的元素个数，发现了什么？


```python
l =  [True,False,0,1,2] 
countTrue = l.count(True)    # bool型变量True可以参与算数计算，相当于数字1
countFalse = l.count(False)    # bool型变量False可以参与算数计算，相当于数字0
count0 = l.count(0)
count1 = l.count(1)
count2 = l.count(2)
countTrue,countFalse,count0,count1,count2    #因此统计0与1时，会把True和False也算进去
```




    (2, 2, 2, 2, 1)



## 8、从列表 [True,1,0,‘x’,None,‘x’,False,2,True] 中删除元素‘x’。


```python
l = [True,1,0,'x',None,'x',False,2,True] 
try:
    while True:
        l.remove('x')    # remove方法只会移除检索到的第一个出现的被删除元素。需要多次删除
except:
    print(l)
```

    [True, 1, 0, None, False, 2, True]


## 9、从列表 [True,1,0,‘x’,None,‘x’,False,2,True] 中删除索引号为4的元素。


```python
l = [True,1,0,'x',None,'x',False,2,True] 
l.remove(l[4])
l
```




    [True, 1, 0, 'x', 'x', False, 2, True]



## 10、删除列表中索引号为奇数（或偶数）的元素。


```python
# 删除奇数索引号元素
l = [x for x in range(20)]
l1 = []
for i in range(len(l)):
    if i % 2 == 1:
        l1.append(l[i])
for i in l1:
    l.remove(i)
l
```




    [0, 2, 4, 6, 8, 10, 12, 14, 16, 18]



## 11、清空列表中的所有元素。


```python
l = [x for x in range(20)]
print(l,id(l))
l.clear()
print(l,id(l))
```

    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19] 2844334760072
    [] 2844334760072


## 12、对列表 [3,0,8,5,7] 分别做升序和降序排列。


```python
l = [3,0,8,5,7] 
l.sort()
print(l,id(l))
l.sort(reverse=True)
print(l,id(l))
```

    [0, 3, 5, 7, 8] 2844340924808
    [8, 7, 5, 3, 0] 2844340924808


## 13、将列表 [3,0,8,5,7] 中大于 5 元素置为1，其余元素置为0。


```python
l = [3,0,8,5,7] 
for i in range(len(l)):
    if l[i] > 5:
        l[i] = 1
    else:
        l[i] = 0
l
```




    [0, 0, 1, 0, 1]



## 14、遍历列表 [‘x’,‘y’,‘z’]，打印每一个元素及其对应的索引号。


```python
l =  ['x','y','z']
for elem in l:
    print('l[%d] = %s'%(l.index(elem),elem))
```

    l[0] = x
    l[1] = y
    l[2] = z


## 15、将列表 [0, 1, 2, 3, 4, 5, 6, 7, 8, 9] 拆分为奇数组和偶数组两个列表。


```python
l =  [0, 1, 2, 3, 4, 5, 6, 7, 8, 9] 
l1, l2 = [], []
for elem in l:
    if elem % 2 == 1:
        l1.append(elem)
    else:
        l2.append(elem)
l1, l2
```




    ([1, 3, 5, 7, 9], [0, 2, 4, 6, 8])



## 16、分别根据每一行的首元素和尾元素大小对二维列表 [[6, 5], [3, 7], [2, 8]] 排序。


```python
l = [[6, 5], [3, 7], [2, 8]] 
l.sort()
for list in l:
    list.sort()
l
```




    [[2, 8], [3, 7], [5, 6]]



## 17、从列表 [1,4,7,2,5,8] 索引为3的位置开始，依次插入列表 [‘x’,‘y’,‘z’] 的所有元素。


```python
l1 = ['x','y','z']
l2 =  [1,4,7,2,5,8] 
for i in range(len(l1)):
    l2.insert(3+i,l1[i])

print(l2)
```

    [1, 4, 7, 'x', 'y', 'z', 2, 5, 8]


## 18、快速生成由 [5,50) 区间内的整数组成的列表。


```python
l = [i for i in range(5,50)]
print(l)
```

    [5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49]


## 19、若 a = [1,2,3]，令 b = a，执行 b[0] = 9， a[0]亦被改变。为何？如何避免？----讲了深COPY和浅COPY再做


```python
# 略
```

## 20、将列表 [‘x’,‘y’,‘z’] 和 [1,2,3] 转成 [(‘x’,1),(‘y’,2),(‘z’,3)] 的形式。


```python
l1 = ['x','y','z']
l2 = [1,2,3]
t =(x for x in l1)
t
```




    <generator object <genexpr> at 0x0000029640534948>



## 21、以列表形式返回字典 {‘Alice’: 20, ‘Beth’: 18, ‘Cecil’: 21} 中所有的键。


```python
d =  {'Alice': 20, 'Beth': 18, 'Cecil': 21} 
keyList = [x for x in d.keys()]
keyList
```




    ['Alice', 'Beth', 'Cecil']



## 22、以列表形式返回字典 {‘Alice’: 20, ‘Beth’: 18, ‘Cecil’: 21} 中所有的值。


```python
d =  {'Alice': 20, 'Beth': 18, 'Cecil': 21} 
valueList = [x for x in d.values()]
valueList
```




    [20, 18, 21]



## 23、以列表形式返回字典 {‘Alice’: 20, ‘Beth’: 18, ‘Cecil’: 21} 中所有键值对组成的元组。


```python
d =  {'Alice': 20, 'Beth': 18, 'Cecil': 21} 
itemList = [x for x in d.items()]
itemList,d.items()
```




    ([('Alice', 20), ('Beth', 18), ('Cecil', 21)],
     dict_items([('Alice', 20), ('Beth', 18), ('Cecil', 21)]))



## 24、向字典 {‘Alice’: 20, ‘Beth’: 18, ‘Cecil’: 21} 中追加 ‘David’:19 键值对，更新Cecil的值为17。


```python
d =  {'Alice': 20, 'Beth': 18, 'Cecil': 21}
d['David'] = 19
d['Cecil'] = 17
d
```




    {'Alice': 20, 'Beth': 18, 'Cecil': 17, 'David': 19}



## 25、删除字典 {‘Alice’: 20, ‘Beth’: 18, ‘Cecil’: 21} 中的Beth键后，清空该字典。


```python
d =  {'Alice': 20, 'Beth': 18, 'Cecil': 21}
d.pop('Beth')
print(d)
d.clear()
d
```

    {'Alice': 20, 'Cecil': 21}





    {}



## 26、判断 David 和 Alice 是否在字典 {‘Alice’: 20, ‘Beth’: 18, ‘Cecil’: 21} 中。


```python
d =  {'Alice': 20, 'Beth': 18, 'Cecil': 21}
if d.get('Alice')!= None:
    print('Alice is in d')
else:
    print('Alice is not in d')

if d.get('David')!= None:
    print('Alice is in d')
else:
    print('Alice is not in d')
```

    Alice is in d
    Alice is not in d


## 27、遍历字典 {‘Alice’: 20, ‘Beth’: 18, ‘Cecil’: 21}，打印键值对。


```python
d =  {'Alice': 20, 'Beth': 18, 'Cecil': 21}
for i in d:
    print(i,d[i])

for i in d.items():
    print(i)
```

    Alice 20
    Beth 18
    Cecil 21
    ('Alice', 20)
    ('Beth', 18)
    ('Cecil', 21)


## 28、若 a = dict()，令 b = a，执行 b.update({‘x’:1})， a亦被改变。为何？如何避免？----讲了深COPY和浅COPY再做


```python
# 略
```

## 29、以列表 [‘A’,‘B’,‘C’,‘D’,‘E’,‘F’,‘G’,‘H’] 中的每一个元素为键，默认值都是0，创建一个字典。


```python
l = ['A','B','C','D','E','F','G','H'] 
d = {}
for i in l:
    d[i] = 0
d
```




    {'A': 0, 'B': 0, 'C': 0, 'D': 0, 'E': 0, 'F': 0, 'G': 0, 'H': 0}




```python
l = ['A','B','C','D','E','F','G','H'] 
d = {x:0 for x in l}
d
```




    {'A': 0, 'B': 0, 'C': 0, 'D': 0, 'E': 0, 'F': 0, 'G': 0, 'H': 0}



## 30、将二维结构 [[‘a’,1],[‘b’,2]] 和 ((‘x’,3),(‘y’,4)) 转成字典。


```python
l = [['a',1],['b',2]] 
t = (('x',3),('y',4))
d1 = dict(l)
d2 = dict(t)

d1,d2
```




    ({'a': 1, 'b': 2}, {'x': 3, 'y': 4})



## 31、将元组 (1,2) 和 (3,4) 合并成一个元组。


```python
t1 = (1,2)
t2 = (3,4)
t = t1 + t2
t
```




    (1, 2, 3, 4)



## 32、将空间坐标元组 (1,2,3) 的三个元素解包对应到变量 x,y,z。


```python
t = (1,2,3)
t1,t2,t3=t
*_,t4=t    # *_类似与golang中的匿名变量 _ ，同样的python的 *_ 是不能拿来调用的。
print(t1,t2,t3)
print(t4)
print(*t)
```

    1 2 3
    3
    1 2 3


## 33、返回元组 (‘Alice’,‘Beth’,‘Cecil’) 中 ‘Cecil’ 元素的索引号。


```python
t = ('Alice','Beth','Cecil')
t.index('Cecil')
```




    2



## 34、返回元组 (2,5,3,2,4) 中元素 2 的个数。


```python
(2,5,3,2,4).count(2)
```




    2



## 35、判断 ‘Cecil’ 是否在元组 (‘Alice’,‘Beth’,‘Cecil’) 中。


```python
'Cecil' in ('Alice','Beth','Cecil')
```




    True



## 36、返回在元组 (2,5,3,7) 索引号为2的位置插入元素 9 之后的新元组。


```python
t = (2,5,3,7) 
l = [x for x in t]
l.insert(2,9)
tuple(l)

```




    (2, 5, 9, 3, 7)



## 37、创建一个空集合，增加 {‘x’,‘y’,‘z’} 三个元素。


```python
s = set()
s1 = {'x','y','z'} 
for x in s1:
    s.add(x)

print(s)
```

    {'z', 'x', 'y'}


## 38、删除集合 {‘x’,‘y’,‘z’} 中的 ‘z’ 元素，增加元素 ‘w’，然后清空整个集合。


```python
s = {'x','y','z'} 
s.remove('z')
print(s)
s.add('w')
print(s)
s.clear()
s
```

    {'x', 'y'}
    {'x', 'y', 'w'}





    set()



## 39、返回集合 {‘A’,‘D’,‘B’} 中未出现在集合 {‘D’,‘E’,‘C’} 中的元素（差集）。


```python
s = {'A','D','B'}
s1 = {'D','E','C'}
print(s.difference(s1))
s - s1
```

    {'A', 'B'}





    {'A', 'B'}



## 40、返回两个集合 {‘A’,‘D’,‘B’} 和 {‘D’,‘E’,‘C’} 的并集。


```python
s = {'A','D','B'}
s1 = {'D','E','C'}
s.union(s1)
print(s)
s | s1
```

    {'A', 'B', 'D'}





    {'A', 'B', 'C', 'D', 'E'}



## 41、返回两个集合 {‘A’,‘D’,‘B’} 和 {‘D’,‘E’,‘C’} 的交集。


```python
s = {'A','D','B'}
s1 = {'D','E','C'}
print(s.intersection(s1))
s & s1
```

    {'D'}





    {'D'}



## 42、返回两个集合 {‘A’,‘D’,‘B’} 和 {‘D’,‘E’,‘C’} 未重复的元素的集合。


```python
s = {'A','D','B'}
s1 = {'D','E','C'}

s1 ^ s
```




    {'A', 'B', 'C', 'E'}



## 43、判断两个集合 {‘A’,‘D’,‘B’} 和 {‘D’,‘E’,‘C’} 是否有重复元素。


```python
s = {'A','D','B'}
s1 = {'D','E','C'}
None not in s & s1
```




    True



## 44、判断集合 {‘A’,‘C’} 是否是集合 {‘D’,‘C’,‘E’,‘A’} 的子集。


```python
s = {'A','C'}
s1 = {'D','C','E','A'}
s in s1
```




    False



## 45、去除数组 [1,2,5,2,3,4,5,‘x’,4,‘x’] 中的重复元素。


```python
l = [1,2,5,2,3,4,5,'x',4,'x']
[set(l)]
```




    [{1, 2, 3, 4, 5, 'x'}]



## 46、返回字符串 ‘abCdEfg’ 的全部大写、全部小写和大下写互换形式。


```python
str = 'abCdEfg'
print(str.upper())
print(str.lower())
print(str.swapcase())   #大下写互换
```

    ABCDEFG
    abcdefg
    ABcDeFG


## 47、判断字符串 ‘abCdEfg’ 是否首字母大写，字母是否全部小写，字母是否全部大写。


```python
str = 'abCdEfg'
print(str[0].islower())
print(str.isupper())
print(str.islower())
```

    True
    False
    False


## 48、返回字符串 ‘this is python’ 首字母大写以及字符串内每个单词首字母大写形式。


```python
str = 'this is python'
print(str.capitalize())
print(str.title())   #或者用split分割再逐一首字母大写。
```

    This is python
    This Is Python


## 49、判断字符串 ‘this is python’ 是否以 ‘this’ 开头，又是否以 ‘python’ 结尾。


```python
str = 'this is python'
print(str.startswith('this'))
print(str.endswith('python'))
```

    True
    True


## 50、返回字符串 ‘this is python’ 中 ‘is’ 的出现次数。


```python
str = 'this is python'
str.count('is')
```




    2



## 51、返回字符串 ‘this is python’ 中 ‘is’ 首次出现和最后一次出现的位置。


```python
str = 'this is python'
print(str.index('is'))   #找不到时会返回ValueError
print(str.find('is'))    #找不到时返回-1
print(str.rfind('is'))
```

    2
    2
    5


## 52、将字符串 ‘this is python’ 切片成3个单词。


```python
str = 'this is python'
str.split()
```




    ['this', 'is', 'python']



## 53、返回字符串 ‘blog.csdn.net/xufive/article/details/102946961’ 按路径分隔符切片的结果。


```python
str = 'blog.csdn.net/xufive/article/details/102946961'
str.split('/')
```




    ['blog.csdn.net', 'xufive', 'article', 'details', '102946961']



## 54、将字符串 ‘2.72, 5, 7, 3.14’ 以半角逗号切片后，再将各个元素转成浮点型或整形。


```python
str = '2.72, 5, 7, 3.14'
l = str.split(', ')
print(l)

l1=[]
for elem in l:
    try:
        a = int(elem)
    except:
        a = float(elem)
    l1.append(a)
l1
```

    ['2.72', '5', '7', '3.14']





    [2.72, 5, 7, 3.14]



## 55、判断字符串 ‘adS12K56’ 是否完全为字母数字，是否全为数字，是否全为字母？ 


```python
str = 'adS12K56'
print(str.isalnum())      # 字符串中的所有字符都是字母数字并且至少包含一个字符，则返回true
print(str.isdigit())    # 字符串中的所有字符都是数字并且至少包含一个字符，则返回true
print(str.isalpha())    # 字符串中的所有字符都是字母并且至少包含一个字符，则返回true
```

    True
    False
    False


## 56、将字符串 ‘there is python’ 中的 ‘is’ 替换为 ‘are’。


```python
str = 'this is python'
t = str.count('is')
str.replace('is','are',t)
```




    'thare are python'



## 57、清除字符串 ‘\t python \n’ 左侧、右侧，以及左右两侧的空白字符。


```python
str = '\t python \n'
str.split()
```




    ['python']



## 58、将三个全英文字符串（比如，‘ok’, ‘hello’, ‘thank you’）分行打印，实现左对齐、右对齐和居中对齐效果。


```python
str1 = 'ok'
str2 = 'hello'
str3 = 'thank you'
print(str1.ljust(20,'-'))   # str.ljust(行输出字符数，空余填充字符)
print(str2.rjust(20,'*'))
print(str3.center(20,'+'))
```

    ok------------------
    ***************hello
    +++++thank you++++++


## 59、将三个字符串（比如，‘Hello, 我是David’, ‘OK, 好’, ‘很高兴认识你’）分行打印，实现左对齐、右对齐和居中效果。


```python
str1 = 'Hello, 我是David'
str2 = 'OK, 好'
str3 = '很高兴认识你'
print(str1.ljust(20,'-'))   
print(str2.rjust(20,'*'))
print(str3.center(20,'+'))
```

    Hello, 我是David------
    ***************OK, 好
    +++++++很高兴认识你+++++++


## 60、将三个字符串 ‘15’, ‘127’, ‘65535’ 左侧补0成同样长度。


```python
str1 = '15'
str2 = '127'
str3 = '65535'
[len(str1),len(str2),len(str3)].sort()
print(str1.rjust(l[-1],'0'))
print(str2.rjust(l[-1],'0'))
print(str3.rjust(l[-1],'0'))
```

    00015
    00127
    65535


## 61、将列表 [‘a’,‘b’,‘c’] 中各个元素用’|'连接成一个字符串。


```python
l = ['a','b','c']
str0 = '|'
str1 = (x for x in l)
str0.join(str1)
```




    'a|b|c'



## 62、将字符串 ‘abc’ 相邻的两个字母之间加上半角逗号，生成新的字符串。


```python
str = 'abc'
sepStr = ','
str1 = sepStr.join(str)
str1
```




    'a,b,c'



## 63、从键盘输入手机号码，输出形如 ‘Mobile: 186 6677 7788’ 的字符串。


```python
phoneNum = input('从键盘输入手机号码:')
'''
    l = [phoneNum[:3],phoneNum[3:7],phoneNum[7:]]
    sep = ' '
    sep.join(l)
'''
print('Mobile: {}'.format(' '.join([phoneNum[:3],phoneNum[3:7],phoneNum[7:]])))
```

    从键盘输入手机号码:18666777788
    Mobile: 186 6677 7788


## 64、从键盘输入年月日时分秒，输出形如 ‘2019-05-01 12:00:00’ 的字符串。


```python
import time
tm = input("从键盘输入年月日时分秒:")
print ('{0} {1}'.format('-'.join([tm[:4],tm[4:6],tm[6:8]]),':'.join([tm[8:10],tm[10:12],tm[12:]])))
```

    从键盘输入年月日时分秒:20190501120000
    2019-05-01 12:00:00


## 65、给定两个浮点数 3.1415926 和 2.7182818，格式化输出字符串 ‘pi = 3.1416, e = 2.7183’。


```python
PI = 3.1415926
E = 2.7182818
print('pi = %.4f, e = %.4f'%(PI,E))
```

    pi = 3.1416, e = 2.7183


## 66、将 0.00774592 和 356800000 格式化输出为科学计数法字符串。


```python
num1 = 0.00774592
num2 = 356800000
print('0.00774592 = %e\n356800000 = %e' % (num1,num2))
```

    0.00774592 = 7.745920e-03
    356800000 = 3.568000e+08


## 67、将列表 [0,1,2,3.14,‘x’,None,’’,list(),{5}] 中各个元素转为布尔型。


```python
l = [0,1,2,3.14,'x',None,'',list(),{5}]
for x in range(len(l)):
    l[x] = bool(l[x])
l    
```




    [False, True, True, True, True, False, False, False, True]



## 68、返回字符 ‘a’ 和 ‘A’ 的ASCII编码值。


```python
print(ord('a'),ord('A'))
```

    97 65


## 69、返回ASCII编码值为 57 和 122 的字符。


```python
print(chr(57),chr(122))
```

    9 z


## 70、将列表 [3,‘a’,5.2,4,{},9,[]] 中 大于3的整数或浮点数置为1，其余置为0。


```python
L = [3,'a', 5.2, 4, {}, 9, []]
for n in range(len(L)):
    if type(L[n]) == type(3):
        if type(L[n]) == type(1.1):
            L[n] = 1
        elif L[n] > 3:
            L[n] = 1
        else:
            L[n] = 0
    elif type(L[n]) == type(1.1):
            L[n] = 1
    else:
        L[n] = 0
print(L)
```

## 71、将二维列表 [[1], [‘a’,‘b’], [2.3, 4.5, 6.7]] 转为 一维列表。


```python
# l2 = [[1],['a','b'],[2.3,4.5,6.7]]

```

## 72、将等长的键列表和值列表转为字典。


```python
kl = ['name','age','ginder','title']
vl = ['Li',18,'male','boss']
d = {k:None for k in kl }
for x in range(len(vl)):
    d[kl[x]] = vl[x]
print(d)
```

## 73、数字列表求和。


```python
import random

len = random.randint(1,200)
numList = [x for x in range(random.randint(1,200))]
print(numList)
sum = 0
for num in numList:
    sum += num
print(sum)
```

    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18]
    171



```python

```

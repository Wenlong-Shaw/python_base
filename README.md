# day13

## 1、将《The_Holy_Bible.txt》中的标点符号替换成空格，大写字母转换成小写字母并将处理过的文本保存到 “The_Holy_Bible.txt”中。 


```python
import os
import string

path = os.getcwd()
# print(path)


def remove_punctuation(text):
    """
    移除字符串中的标点符号（移除除了 ' 符号以外的全部符号）。
    """

    temp = []
    punctuation = [c for c in string.punctuation]
    punctuation.remove("'")
    for c in text:
        if c not in punctuation:
            temp.append(c)
    newText = ''.join(temp)
    # print(newText)
    return newText


with open(path+'/2th-肖文龙-作业/The_Holy_Bible.txt', mode='r', encoding='utf-8') as f:
    #指针位置复位
    f.seek(0, 0)
    with open(path+'/2th-肖文龙-作业/copy.txt', mode='a+', encoding='utf-8') as t:
        while True:
            txt = f.readline()
            if not txt:
                break
            # print(txt)
            txt = txt.lower()
            # print(txt)
            txt = remove_punctuation(txt)
            t.write(txt)
```

## 2、统计” The_Holy_Bible.txt “ 中字符的个数，行数，单词的个数，统计单词的词频并打 印输出词频最高的前 10 个单词及其词频。


```python
import os
import string

path = os.getcwd()

d = {}
newTxtList = []
lineCount = 0
with open(path+'/2th-肖文龙-作业/copy.txt', mode='a+', encoding='utf-8') as f:
    f.seek(0, 0)
    i = 0
    while True:
        txt = f.readline()
        if not txt:
            break
        newTxtList += txt.split()
        lineCount += 1
    f.close()

charCount = 0
for word in newTxtList:
    charCount += len(word)
print('字符的总个数（已除去标点符号）：', charCount)
print('单词的总个数：', len(newTxtList))
txtSet = set(newTxtList)
txtList = list(txtSet)
for alph in txtList:
    wordCount = newTxtList.count(alph)
    d[alph] = wordCount
dOrder = sorted(d.items(), key=lambda x: x[1], reverse=True)
print('总行数统计：', lineCount)
print('词频最高的前10个单词：', dOrder[0:10])
```

**输出结果**
1. 字符的总个数（已除去标点符号）： 3291977
2. 单词的总个数： 824691
3. 总行数统计： 32432
4. 词频最高的前10个单词： [('the', 64045), ('and', 51714), ('of', 34765), ('to', 13643), ('that', 12916), ('in', 12674), ('he', 10431), ('shall', 9837), ('unto', 9003), ('for', 8985)]

## 3、使用Python的队列deque

> **class collections.deque([iterable[, maxlen]])**
> 返回一个新的双向队列对象，从左到右初始化(用方法 append()) ，从 iterable （迭代对象) 数据创建。如果 iterable 没有指定，新队列为空。
>
> Deque队列是由栈或者queue队列生成的（发音是 “deck”，”double-ended queue”的简称）。Deque 支持线程安全，内存高效添加(append)和弹出(pop)，从两端都可以，两个方向的大概开销都是 O(1) 复杂度。
>
> **虽然 list 对象也支持类似操作，不过这里优化了定长操作和 pop(0) 和 insert(0, v) 的开销。它们引起 O(n) 内存移动的操作，改变底层数据表达的大小和位置。**
>
> 如果 maxlen 没有指定或者是 None ，deques 可以增长到任意长度。否则，deque就限定到指定最大长度。一旦限定长度的deque满了，当新项加入时，同样数量的项就从另一端弹出。限定长度deque提供类似Unix filter tail 的功能。它们同样可以用与追踪最近的交换和其他数据池活动。
>
> **双向队列(deque)对象支持以下方法：**
>
> append(x): 添加 x 到右端。
>
> appendleft(x): 添加 x 到左端。
>
> clear(): 移除所有元素，使其长度为0.
>
> copy(): 创建一份浅拷贝。
>
> **3.5 新版功能.**
>
> count(x): 计算deque中个数等于 x 的元素。
>
> 3.2 新版功能.
>
> extend(iterable): 扩展deque的右侧，通过添加iterable参数中的元素。
>
> extendleft(iterable): 扩展deque的左侧，通过添加iterable参数中的元素。注意，左添加时，在结果中iterable参数中的顺序将被反过来添加。
>
> index(x[, start[, stop]]): 返回第 x 个元素（从 start 开始计算，在 stop 之前）。返回第一个匹配，如果没找到的话，升起 ValueError 。
>
> 3.5 新版功能.
>
> insert(i, x): 在位置 i 插入 x 。
>
> 如果插入会导致一个限长deque超出长度 maxlen 的话，就升起一个 IndexError 。
>
>3.5 新版功能.
>
>pop(): 移去并且返回一个元素，deque最右侧的那一个。如果没有元素的话，就升起 IndexError 索引错误。
>
> popleft():移去并且返回一个元素，deque最左侧的那一个。如果没有元素的话，就升起 IndexError 索引错误。
>
>remove(value): 移去找到的第一个 value。 如果没有的话就升起 ValueError 。
>
>reverse(): 将deque逆序排列。返回 None 。
>
>3.2 新版功能.
>
>rotate(n=1): 向右循环移动 n 步。 如果 n 是负数，就向左循环。
>
>如果deque不是空的，向右循环移动一步就等价于 d.appendleft(d.pop()) ， 向左循环一步就等价于 d.append(d.popleft()) 。
>
>Deque对象同样提供了一个只读属性:
>
>maxlen : 
>Deque的最大尺寸，如果没有限定的话就是 None 。
>
>3.1 新版功能.
>
>除了以上，deque还支持迭代，清洗，len(d), reversed(d), copy.copy(d), copy.deepcopy(d), 成员测试 in 操作符，和下标引用 d[-1] 。索引存取在两端的复杂度是 O(1)， 在中间的复杂度比 O(n) 略低。要快速存取，使用list来替代。


```python
from collections import deque

queue = deque()
print(queue)
queue += ['a', 'b', 'c', 'd', 'e', 'f']
print(queue)
print(queue.popleft())
print(queue)
queue.append('a')
print(queue)
```

    deque([])
    deque(['a', 'b', 'c', 'd', 'e', 'f'])
    a
    deque(['b', 'c', 'd', 'e', 'f'])
    deque(['b', 'c', 'd', 'e', 'f', 'a'])


## 4、实现有5个元素的循环队列


```python
class Cq:
    #初始化循环队列（最大队列长度，头、尾指针）
    def __init__(self,len):
        self.queue = [None]*len
        self.max_len = len
        self.front = 0
        self.rear = 0
        
    def enqueue(self,elem):
        # 牺牲一个元素空间来区分队空和满，入队时少用一个元素空间，这是普遍做法。
        # 约定“队头指针在队尾指针的下一个位置即为队满！”
        # 那么“队头指针与队尾指针在同一个位置即为队空！”
        # 入队前先判满，不满再入队！
        if (self.rear + 1) % self.max_len == self.front:
            print('queue is full')
            return False
        #赋值入队
        self.queue[self.rear] = elem
        #此时应该将队尾指针前移一个位置！
        self.rear = (self.rear + 1) % self.max_len
        return True
    
    def dequeue(self):
        # “队头指针与队尾指针在同一个位置即为队空！”
        # 出队前先判空，不空再出队！
        if self.rear == self.front:
            print('queue is empty!')
            return None
        #暂时存储出队元素
        elem = self.queue[self.front]
        #此时应该将队头指针前移一个位置！
        self.front = (self.front + 1) % self.max_len
        return elem

q = Cq(5)
print(q.dequeue()) 
while q.enqueue(2):
    pass
print(q.queue)
```

    queue is empty!
    None
    queue is full
    [2, 2, 2, 2, None]


## 5、实现目录的深度优先遍历(写了的不用再写)


```python
import os


def deep_walk_dir(path, width = 0):
    allFile = os.listdir(path)
    for i in allFile:
        print('  ' * width, end = '')
        print(i)
        if os.path.isdir(path+ '/' + i):
            width += 4
            deep_walk_dir(path+ '/' + i,width)
    
path = os.getcwd()
deep_walk_dir(path)
```

    .ipynb_checkpoints
            .ipynb_checkpoints
                    day10_肖文龙-checkpoint-checkpoint.ipynb
                    day10_肖文龙-checkpoint.ipynb
                    day11_肖文龙-checkpoint.ipynb
                    day12_肖文龙-checkpoint.ipynb
                    day13_肖文龙-checkpoint.ipynb
                    day6_肖文龙-checkpoint.ipynb
                    day7_note-checkpoint.ipynb
                    day7_肖文龙-checkpoint.ipynb
                    day8_note-checkpoint.ipynb
                    day8_肖文龙-checkpoint.ipynb
                    day9_肖文龙-checkpoint.ipynb
            day10_肖文龙.ipynb
            day11_肖文龙.ipynb
            day12_肖文龙.ipynb
            day13_肖文龙.ipynb
            day5_肖文龙.ipynb
            day6_肖文龙.ipynb
            day6_肖文龙_note.ipynb
            day7_note.ipynb
            day7_肖文龙.ipynb
            day8_note.ipynb
            day8_肖文龙.ipynb
            day9_肖文龙.ipynb
            pic
                    1.png
                    2.5.png
                    2.png
                    3.png
                    4.png
                    testdir
                            text


## 6、完成冒泡排序，选择排序，插入排序，快速排序

### 6.1 冒泡排序
> **冒泡排序原理**
>
> 冒泡法排序的思想是通过一轮比较，把最大的放在最后面，
> 然后将剩余的9个元素再进行- -趟比较，再把最大的放在最后面，
> 这样不断进行，最终实现数组有序。
>
> **时间复杂度**
>
> 冒泡排序平均和最坏： 
> ![n2](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADIAAAAXBAMAAAC7cAEHAAAAMFBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAv3aB7AAAAD3RSTlMAEHZmmasi3Ym7RO8yVM0Ml5alAAAACXBIWXMAAA7EAAAOxAGVKw4bAAABOklEQVQoFWVSIU/DQBh9bddyWXtZEwQOGmZwNCELwYGbbFAIRB0JFk1yAoVaUNMoAg7cVCUJZoRgSbNfMAxqyXjfjV0HvOS+77339b772ivwH29Xfz1dWSfKQqN+1+4WMqmDQXIo3NveO7JebSODMrgW3ktxlorORAk2UmwyqYJrQBKLaXEKhGPggc+3p3QOfnz4VQldwHuikcwYjpeVe2SIplCfNPQXw4i5u96rovncADOsyREt6cbq+UuuRRMX6BimuAAibh7vwycVTLCVMe2WPEv29RGKJoaIDdMjl62M0CnJiSFaNYeX3tKNE320xZdu3iVwItTjBEGNfiBCJoDq7pSWc2o/x/OrFZy6wU1Dbd9GvjeU7yxHL9F8UTryRR1U7igvYoUDqw3szbnqrWNY3LbTunKUf8g3TTo9hY+/v0wAAAAASUVORK5CYII=)
>
> 冒泡排序最好：
> ![n](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACkAAAATBAMAAAD/rzkOAAAAMFBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAv3aB7AAAAD3RSTlMAEHZmmasi3Ym7RO8yVM0Ml5alAAAACXBIWXMAAA7EAAAOxAGVKw4bAAAA/ElEQVQYGU2PsUoDQRRFz2422bjrmgGFlAbTiI0LIdjY2KVMaTlFIJjCPxDyA4J+hJWddlaWgiDrD8h+QmysLLwzs6s+duaee+fNGxZ+KxoFDBIdTM6c74aQPa9Tw9KIjpq0KAX9udaNoG5SD/fqyzbgW/zBNUSPou1v2LJt750uf8oUX5BLxrvTZ0+pG5loQgqr17KQHehbK83ncAnVCbEoN+yPlB5beJPO6Mqmhnwt96A11HpiYP3cpNZfaZh7rbfhI/MUXcG5QnYMnZpZBy7k+uND69K4Ii55eYeJs0319Hqo2xactubv2KULt6kSEzTsWRX09H8INljJD292JgaQtVzOAAAAAElFTkSuQmCC)
>
> **空间复杂度**
>
>![1](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACcAAAATBAMAAADhZgm9AAAAMFBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAv3aB7AAAAD3RSTlMAEHZmmasi3Ym7RO8yVM0Ml5alAAAACXBIWXMAAA7EAAAOxAGVKw4bAAAA4ElEQVQYGU2PPQrCQBCF30pMNPFnC8FS0UZEUBA7G2+Q0jKFIDbeQLCxU9BDWNnpPcQj5AAW2liIiG/HbMjA7Hvvy+wkAdJSTbH/U7WGExPzwlATGWnMNV0X8O9AeUBfCNl7mhhu7yMKnDjlP5IJA3eAulBLDMWIxsAjbz6p5RcQUAXSeGadw+uehVWgumYIQmBpYaDRaDL0I+BqoacRrBnO7LqF3OnE/BezN/sitQKmZqiiebzZC3ah3YkoyN2gNt8tMDQpKZdfIHVINBvShwJn/wnH7E7Lv4kdp0BMZM8fNIYoFO8nUDMAAAAASUVORK5CYII=)


```python
import random
import time
#冒泡排序原理
#冒泡法排序的思想是通过一轮比较，把最大的放在最后面，
#然后将剩余的9个元素再进行- -趟比较，再把最大的放在最后面，
#这样不断进行，最终实现数组有序。
class RandomList(object):
    
    def __init__(self,len,random_range):
        self.list = []
        for i in range(len):
            random.seed(random.randint(0,i*len))
            self.list.append(random.randint(0,random_range))
        self.len = len
        
    def bubble_sort(self):
        l = self.list
        for x in range(self.len - 1, 0, -1):
            flag = True
            for y in range(x):
                if l[y] > l[y+1]:
                    l[y], l[y+1] = l[y+1], l[y]
                    flag = False
            if flag:
                break


l = RandomList(500,10000)
print(l.list)
start_time = time.time()
l.bubble_sort()
end_time = time.time()
print(l.list)
print(end_time - start_time)
```

    [6311, 6042, 2607, 7930, 6795, 6101, 8314, 737, 388, 4069, 9710, 3811, 890, 8443, 5283, 5761, 6788, 1763, 8910, 6690, 6806, 2045, 745, 5243, 9638, 4088, 8401, 8859, 5809, 3200, 8721, 2018, 8557, 1304, 6726, 5484, 547, 3835, 8308, 8839, 5582, 1397, 4007, 2872, 3220, 1534, 7584, 5678, 7609, 1333, 2052, 9548, 322, 1688, 7369, 9235, 2792, 2125, 603, 4481, 2410, 9781, 5267, 7590, 3386, 6270, 465, 1774, 6238, 5655, 1268, 9625, 8056, 3966, 8696, 1981, 8256, 7710, 428, 127, 1190, 3858, 3996, 5996, 6315, 6311, 360, 3081, 8014, 3977, 7958, 6141, 1517, 4262, 9838, 4763, 7907, 7734, 8197, 7301, 2050, 9830, 2503, 6690, 1362, 136, 9309, 4103, 5643, 9211, 164, 1739, 1685, 1515, 912, 7070, 120, 7414, 3800, 7907, 4034, 2411, 9125, 3511, 9964, 7091, 4763, 7717, 4676, 1577, 2722, 8641, 8686, 3565, 3555, 3136, 7584, 779, 3032, 5783, 6191, 9536, 4648, 9998, 5414, 5917, 7776, 27, 2122, 7759, 8680, 3257, 192, 1028, 2576, 4550, 7324, 4643, 384, 7835, 7012, 885, 57, 5430, 6630, 2411, 5024, 5777, 1864, 129, 7575, 5885, 4177, 1268, 3531, 6703, 6644, 5915, 3245, 997, 5333, 9198, 8365, 7195, 7725, 4262, 7028, 4661, 2414, 4418, 713, 7244, 9585, 5249, 8545, 9033, 3704, 6395, 8238, 4893, 1817, 6746, 1346, 1780, 3418, 1611, 1777, 9782, 7162, 1809, 9232, 9385, 1885, 5329, 762, 1875, 4517, 8933, 4127, 4246, 9749, 1029, 1809, 2255, 5206, 1561, 1278, 7905, 4072, 2435, 8019, 3169, 7903, 4334, 4606, 1799, 9981, 1194, 5873, 8467, 9, 6529, 6592, 7096, 7598, 1581, 9092, 8231, 7378, 9565, 9864, 5742, 4397, 4779, 4421, 4984, 3450, 5660, 8152, 6305, 5413, 8249, 6776, 310, 8731, 6603, 3298, 6105, 2475, 9702, 3980, 7119, 3301, 6716, 8019, 3034, 5192, 35, 8650, 8597, 5923, 3174, 6932, 5924, 7079, 2187, 3752, 1162, 8480, 8353, 5102, 1238, 8026, 7468, 6081, 2282, 7589, 2298, 5395, 156, 3636, 9169, 2078, 7596, 8079, 2466, 2903, 6958, 3048, 6299, 7624, 6170, 3423, 5045, 1837, 5047, 4117, 9113, 7390, 1987, 3455, 5405, 2567, 5837, 3485, 9201, 5735, 9219, 3535, 4761, 4548, 3831, 7476, 9613, 130, 8994, 9361, 2594, 620, 5975, 5238, 1079, 1099, 8332, 8864, 3485, 5125, 3470, 6461, 6872, 9060, 6060, 7966, 4193, 8962, 9832, 9708, 6199, 1816, 2673, 9699, 1694, 5248, 5015, 2737, 6296, 3215, 4585, 2494, 5746, 7742, 5634, 9625, 2224, 839, 3272, 8916, 2138, 3059, 1846, 8924, 5198, 2171, 5049, 9304, 7586, 4481, 6516, 7900, 9843, 4612, 2451, 8410, 8974, 9029, 5378, 8635, 683, 3616, 118, 2266, 8293, 7042, 6599, 4493, 4313, 4294, 7019, 3729, 8042, 5494, 6072, 8582, 6755, 5144, 3059, 2957, 9541, 1259, 7844, 2555, 8313, 9812, 3280, 8455, 5308, 4854, 1333, 4026, 183, 165, 7464, 5843, 9249, 212, 9589, 7392, 8670, 7842, 5148, 897, 4811, 5787, 6727, 3948, 6755, 1068, 6434, 3833, 4656, 4603, 9709, 240, 5343, 40, 3792, 9592, 5492, 556, 9592, 3855, 9904, 9461, 406, 9867, 7652, 2369, 9964, 1459, 6768, 3790, 7474, 4839, 7650, 3318, 1644, 947, 2620, 7482, 9951, 2219, 1016, 9167, 7454, 7922, 3138, 1009, 2665, 544, 1945, 645, 7817, 5146, 3001, 5849, 9456, 2507, 4343, 895, 1140]
    [9, 27, 35, 40, 57, 118, 120, 127, 129, 130, 136, 156, 164, 165, 183, 192, 212, 240, 310, 322, 360, 384, 388, 406, 428, 465, 544, 547, 556, 603, 620, 645, 683, 713, 737, 745, 762, 779, 839, 885, 890, 895, 897, 912, 947, 997, 1009, 1016, 1028, 1029, 1068, 1079, 1099, 1140, 1162, 1190, 1194, 1238, 1259, 1268, 1268, 1278, 1304, 1333, 1333, 1346, 1362, 1397, 1459, 1515, 1517, 1534, 1561, 1577, 1581, 1611, 1644, 1685, 1688, 1694, 1739, 1763, 1774, 1777, 1780, 1799, 1809, 1809, 1816, 1817, 1837, 1846, 1864, 1875, 1885, 1945, 1981, 1987, 2018, 2045, 2050, 2052, 2078, 2122, 2125, 2138, 2171, 2187, 2219, 2224, 2255, 2266, 2282, 2298, 2369, 2410, 2411, 2411, 2414, 2435, 2451, 2466, 2475, 2494, 2503, 2507, 2555, 2567, 2576, 2594, 2607, 2620, 2665, 2673, 2722, 2737, 2792, 2872, 2903, 2957, 3001, 3032, 3034, 3048, 3059, 3059, 3081, 3136, 3138, 3169, 3174, 3200, 3215, 3220, 3245, 3257, 3272, 3280, 3298, 3301, 3318, 3386, 3418, 3423, 3450, 3455, 3470, 3485, 3485, 3511, 3531, 3535, 3555, 3565, 3616, 3636, 3704, 3729, 3752, 3790, 3792, 3800, 3811, 3831, 3833, 3835, 3855, 3858, 3948, 3966, 3977, 3980, 3996, 4007, 4026, 4034, 4069, 4072, 4088, 4103, 4117, 4127, 4177, 4193, 4246, 4262, 4262, 4294, 4313, 4334, 4343, 4397, 4418, 4421, 4481, 4481, 4493, 4517, 4548, 4550, 4585, 4603, 4606, 4612, 4643, 4648, 4656, 4661, 4676, 4761, 4763, 4763, 4779, 4811, 4839, 4854, 4893, 4984, 5015, 5024, 5045, 5047, 5049, 5102, 5125, 5144, 5146, 5148, 5192, 5198, 5206, 5238, 5243, 5248, 5249, 5267, 5283, 5308, 5329, 5333, 5343, 5378, 5395, 5405, 5413, 5414, 5430, 5484, 5492, 5494, 5582, 5634, 5643, 5655, 5660, 5678, 5735, 5742, 5746, 5761, 5777, 5783, 5787, 5809, 5837, 5843, 5849, 5873, 5885, 5915, 5917, 5923, 5924, 5975, 5996, 6042, 6060, 6072, 6081, 6101, 6105, 6141, 6170, 6191, 6199, 6238, 6270, 6296, 6299, 6305, 6311, 6311, 6315, 6395, 6434, 6461, 6516, 6529, 6592, 6599, 6603, 6630, 6644, 6690, 6690, 6703, 6716, 6726, 6727, 6746, 6755, 6755, 6768, 6776, 6788, 6795, 6806, 6872, 6932, 6958, 7012, 7019, 7028, 7042, 7070, 7079, 7091, 7096, 7119, 7162, 7195, 7244, 7301, 7324, 7369, 7378, 7390, 7392, 7414, 7454, 7464, 7468, 7474, 7476, 7482, 7575, 7584, 7584, 7586, 7589, 7590, 7596, 7598, 7609, 7624, 7650, 7652, 7710, 7717, 7725, 7734, 7742, 7759, 7776, 7817, 7835, 7842, 7844, 7900, 7903, 7905, 7907, 7907, 7922, 7930, 7958, 7966, 8014, 8019, 8019, 8026, 8042, 8056, 8079, 8152, 8197, 8231, 8238, 8249, 8256, 8293, 8308, 8313, 8314, 8332, 8353, 8365, 8401, 8410, 8443, 8455, 8467, 8480, 8545, 8557, 8582, 8597, 8635, 8641, 8650, 8670, 8680, 8686, 8696, 8721, 8731, 8839, 8859, 8864, 8910, 8916, 8924, 8933, 8962, 8974, 8994, 9029, 9033, 9060, 9092, 9113, 9125, 9167, 9169, 9198, 9201, 9211, 9219, 9232, 9235, 9249, 9304, 9309, 9361, 9385, 9456, 9461, 9536, 9541, 9548, 9565, 9585, 9589, 9592, 9592, 9613, 9625, 9625, 9638, 9699, 9702, 9708, 9709, 9710, 9749, 9781, 9782, 9812, 9830, 9832, 9838, 9843, 9864, 9867, 9904, 9951, 9964, 9964, 9981, 9998]
    0.030916690826416016


### 6.2 选择排序
>**选择排序原理**
>
> 用 Min_pos (最小元素下标标记位) 来标明当前比较轮的最小元素所在列表list内的下标位置，当本轮（第i轮，i>0）比较结束时，就找出了列表中第i小的元素。此时应该下标为(i-1)的元素和(Min_pos)标记的元素互换。接着新一轮(i=1轮)从第i+1个元素开始比较。依次类比，比较完n轮即可排序结束。
>
> **时间复杂度**
>
> 选择排序平均、最好和最坏： 
> ![n2](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADIAAAAXBAMAAAC7cAEHAAAAMFBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAv3aB7AAAAD3RSTlMAEHZmmasi3Ym7RO8yVM0Ml5alAAAACXBIWXMAAA7EAAAOxAGVKw4bAAABOklEQVQoFWVSIU/DQBh9bddyWXtZEwQOGmZwNCELwYGbbFAIRB0JFk1yAoVaUNMoAg7cVCUJZoRgSbNfMAxqyXjfjV0HvOS+77339b772ivwH29Xfz1dWSfKQqN+1+4WMqmDQXIo3NveO7JebSODMrgW3ktxlorORAk2UmwyqYJrQBKLaXEKhGPggc+3p3QOfnz4VQldwHuikcwYjpeVe2SIplCfNPQXw4i5u96rovncADOsyREt6cbq+UuuRRMX6BimuAAibh7vwycVTLCVMe2WPEv29RGKJoaIDdMjl62M0CnJiSFaNYeX3tKNE320xZdu3iVwItTjBEGNfiBCJoDq7pSWc2o/x/OrFZy6wU1Dbd9GvjeU7yxHL9F8UTryRR1U7igvYoUDqw3szbnqrWNY3LbTunKUf8g3TTo9hY+/v0wAAAAASUVORK5CYII=)
>
> **空间复杂度**
> ![1](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACcAAAATBAMAAADhZgm9AAAAMFBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAv3aB7AAAAD3RSTlMAEHZmmasi3Ym7RO8yVM0Ml5alAAAACXBIWXMAAA7EAAAOxAGVKw4bAAAA4ElEQVQYGU2PPQrCQBCF30pMNPFnC8FS0UZEUBA7G2+Q0jKFIDbeQLCxU9BDWNnpPcQj5AAW2liIiG/HbMjA7Hvvy+wkAdJSTbH/U7WGExPzwlATGWnMNV0X8O9AeUBfCNl7mhhu7yMKnDjlP5IJA3eAulBLDMWIxsAjbz6p5RcQUAXSeGadw+uehVWgumYIQmBpYaDRaDL0I+BqoacRrBnO7LqF3OnE/BezN/sitQKmZqiiebzZC3ah3YkoyN2gNt8tMDQpKZdfIHVINBvShwJn/wnH7E7Lv4kdp0BMZM8fNIYoFO8nUDMAAAAASUVORK5CYII=)


```python
import random
import time

class RandomList(object):
    
    def __init__(self,len,random_range):
        self.list = []
        for i in range(len):
            random.seed(random.randint(0,i*len))
            self.list.append(random.randint(0,random_range))
        self.len = len
    
    def select_sort(self):
        l = self.list
        for i in range(self.len - 1, 0, -1):
            min_pos = self.len - 1 - i
            for y in range(i):
                if l[min_pos] > l[self.len - i + y]:
                    min_pos = self.len - i + y
            l[self.len - 1 - i], l[min_pos] = l[min_pos], l[self.len - 1 - i]


l = RandomList(500,10000)
print(l.list)
start_time = time.time()
l.select_sort()
end_time = time.time()
print(l.list)
print(end_time - start_time)
```

    [6311, 6042, 2607, 7930, 6795, 6101, 8314, 737, 388, 4069, 9710, 3811, 890, 8443, 5283, 5761, 6788, 1763, 8910, 6690, 6806, 2045, 745, 5243, 9638, 4088, 8401, 8859, 5809, 3200, 8721, 2018, 8557, 1304, 6726, 5484, 547, 3835, 8308, 8839, 5582, 1397, 4007, 2872, 3220, 1534, 7584, 5678, 7609, 1333, 2052, 9548, 322, 1688, 7369, 9235, 2792, 2125, 603, 4481, 2410, 9781, 5267, 7590, 3386, 6270, 465, 1774, 6238, 5655, 1268, 9625, 8056, 3966, 8696, 1981, 8256, 7710, 428, 127, 1190, 3858, 3996, 5996, 6315, 6311, 360, 3081, 8014, 3977, 7958, 6141, 1517, 4262, 9838, 4763, 7907, 7734, 8197, 7301, 2050, 9830, 2503, 6690, 1362, 136, 9309, 4103, 5643, 9211, 164, 1739, 1685, 1515, 912, 7070, 120, 7414, 3800, 7907, 4034, 2411, 9125, 3511, 9964, 7091, 4763, 7717, 4676, 1577, 2722, 8641, 8686, 3565, 3555, 3136, 7584, 779, 3032, 5783, 6191, 9536, 4648, 9998, 5414, 5917, 7776, 27, 2122, 7759, 8680, 3257, 192, 1028, 2576, 4550, 7324, 4643, 384, 7835, 7012, 885, 57, 5430, 6630, 2411, 5024, 5777, 1864, 129, 7575, 5885, 4177, 1268, 3531, 6703, 6644, 5915, 3245, 997, 5333, 9198, 8365, 7195, 7725, 4262, 7028, 4661, 2414, 4418, 713, 7244, 9585, 5249, 8545, 9033, 3704, 6395, 8238, 4893, 1817, 6746, 1346, 1780, 3418, 1611, 1777, 9782, 7162, 1809, 9232, 9385, 1885, 5329, 762, 1875, 4517, 8933, 4127, 4246, 9749, 1029, 1809, 2255, 5206, 1561, 1278, 7905, 4072, 2435, 8019, 3169, 7903, 4334, 4606, 1799, 9981, 1194, 5873, 8467, 9, 6529, 6592, 7096, 7598, 1581, 9092, 8231, 7378, 9565, 9864, 5742, 4397, 4779, 4421, 4984, 3450, 5660, 8152, 6305, 5413, 8249, 6776, 310, 8731, 6603, 3298, 6105, 2475, 9702, 3980, 7119, 3301, 6716, 8019, 3034, 5192, 35, 8650, 8597, 5923, 3174, 6932, 5924, 7079, 2187, 3752, 1162, 8480, 8353, 5102, 1238, 8026, 7468, 6081, 2282, 7589, 2298, 5395, 156, 3636, 9169, 2078, 7596, 8079, 2466, 2903, 6958, 3048, 6299, 7624, 6170, 3423, 5045, 1837, 5047, 4117, 9113, 7390, 1987, 3455, 5405, 2567, 5837, 3485, 9201, 5735, 9219, 3535, 4761, 4548, 3831, 7476, 9613, 130, 8994, 9361, 2594, 620, 5975, 5238, 1079, 1099, 8332, 8864, 3485, 5125, 3470, 6461, 6872, 9060, 6060, 7966, 4193, 8962, 9832, 9708, 6199, 1816, 2673, 9699, 1694, 5248, 5015, 2737, 6296, 3215, 4585, 2494, 5746, 7742, 5634, 9625, 2224, 839, 3272, 8916, 2138, 3059, 1846, 8924, 5198, 2171, 5049, 9304, 7586, 4481, 6516, 7900, 9843, 4612, 2451, 8410, 8974, 9029, 5378, 8635, 683, 3616, 118, 2266, 8293, 7042, 6599, 4493, 4313, 4294, 7019, 3729, 8042, 5494, 6072, 8582, 6755, 5144, 3059, 2957, 9541, 1259, 7844, 2555, 8313, 9812, 3280, 8455, 5308, 4854, 1333, 4026, 183, 165, 7464, 5843, 9249, 212, 9589, 7392, 8670, 7842, 5148, 897, 4811, 5787, 6727, 3948, 6755, 1068, 6434, 3833, 4656, 4603, 9709, 240, 5343, 40, 3792, 9592, 5492, 556, 9592, 3855, 9904, 9461, 406, 9867, 7652, 2369, 9964, 1459, 6768, 3790, 7474, 4839, 7650, 3318, 1644, 947, 2620, 7482, 9951, 2219, 1016, 9167, 7454, 7922, 3138, 1009, 2665, 544, 1945, 645, 7817, 5146, 3001, 5849, 9456, 2507, 4343, 895, 1140]
    [9, 27, 35, 40, 57, 118, 120, 127, 129, 130, 136, 156, 164, 165, 183, 192, 212, 240, 310, 322, 360, 384, 388, 406, 428, 465, 544, 547, 556, 603, 620, 645, 683, 713, 737, 745, 762, 779, 839, 885, 890, 895, 897, 912, 947, 997, 1009, 1016, 1028, 1029, 1068, 1079, 1099, 1140, 1162, 1190, 1194, 1238, 1259, 1268, 1268, 1278, 1304, 1333, 1333, 1346, 1362, 1397, 1459, 1515, 1517, 1534, 1561, 1577, 1581, 1611, 1644, 1685, 1688, 1694, 1739, 1763, 1774, 1777, 1780, 1799, 1809, 1809, 1816, 1817, 1837, 1846, 1864, 1875, 1885, 1945, 1981, 1987, 2018, 2045, 2050, 2052, 2078, 2122, 2125, 2138, 2171, 2187, 2219, 2224, 2255, 2266, 2282, 2298, 2369, 2410, 2411, 2411, 2414, 2435, 2451, 2466, 2475, 2494, 2503, 2507, 2555, 2567, 2576, 2594, 2607, 2620, 2665, 2673, 2722, 2737, 2792, 2872, 2903, 2957, 3001, 3032, 3034, 3048, 3059, 3059, 3081, 3136, 3138, 3169, 3174, 3200, 3215, 3220, 3245, 3257, 3272, 3280, 3298, 3301, 3318, 3386, 3418, 3423, 3450, 3455, 3470, 3485, 3485, 3511, 3531, 3535, 3555, 3565, 3616, 3636, 3704, 3729, 3752, 3790, 3792, 3800, 3811, 3831, 3833, 3835, 3855, 3858, 3948, 3966, 3977, 3980, 3996, 4007, 4026, 4034, 4069, 4072, 4088, 4103, 4117, 4127, 4177, 4193, 4246, 4262, 4262, 4294, 4313, 4334, 4343, 4397, 4418, 4421, 4481, 4481, 4493, 4517, 4548, 4550, 4585, 4603, 4606, 4612, 4643, 4648, 4656, 4661, 4676, 4761, 4763, 4763, 4779, 4811, 4839, 4854, 4893, 4984, 5015, 5024, 5045, 5047, 5049, 5102, 5125, 5144, 5146, 5148, 5192, 5198, 5206, 5238, 5243, 5248, 5249, 5267, 5283, 5308, 5329, 5333, 5343, 5378, 5395, 5405, 5413, 5414, 5430, 5484, 5492, 5494, 5582, 5634, 5643, 5655, 5660, 5678, 5735, 5742, 5746, 5761, 5777, 5783, 5787, 5809, 5837, 5843, 5849, 5873, 5885, 5915, 5917, 5923, 5924, 5975, 5996, 6042, 6060, 6072, 6081, 6101, 6105, 6141, 6170, 6191, 6199, 6238, 6270, 6296, 6299, 6305, 6311, 6311, 6315, 6395, 6434, 6461, 6516, 6529, 6592, 6599, 6603, 6630, 6644, 6690, 6690, 6703, 6716, 6726, 6727, 6746, 6755, 6755, 6768, 6776, 6788, 6795, 6806, 6872, 6932, 6958, 7012, 7019, 7028, 7042, 7070, 7079, 7091, 7096, 7119, 7162, 7195, 7244, 7301, 7324, 7369, 7378, 7390, 7392, 7414, 7454, 7464, 7468, 7474, 7476, 7482, 7575, 7584, 7584, 7586, 7589, 7590, 7596, 7598, 7609, 7624, 7650, 7652, 7710, 7717, 7725, 7734, 7742, 7759, 7776, 7817, 7835, 7842, 7844, 7900, 7903, 7905, 7907, 7907, 7922, 7930, 7958, 7966, 8014, 8019, 8019, 8026, 8042, 8056, 8079, 8152, 8197, 8231, 8238, 8249, 8256, 8293, 8308, 8313, 8314, 8332, 8353, 8365, 8401, 8410, 8443, 8455, 8467, 8480, 8545, 8557, 8582, 8597, 8635, 8641, 8650, 8670, 8680, 8686, 8696, 8721, 8731, 8839, 8859, 8864, 8910, 8916, 8924, 8933, 8962, 8974, 8994, 9029, 9033, 9060, 9092, 9113, 9125, 9167, 9169, 9198, 9201, 9211, 9219, 9232, 9235, 9249, 9304, 9309, 9361, 9385, 9456, 9461, 9536, 9541, 9548, 9565, 9585, 9589, 9592, 9592, 9613, 9625, 9625, 9638, 9699, 9702, 9708, 9709, 9710, 9749, 9781, 9782, 9812, 9830, 9832, 9838, 9843, 9864, 9867, 9904, 9951, 9964, 9964, 9981, 9998]
    0.019952774047851562


### 6.3 插入排序
>**插入排序原理**
>
> 用 Min_pos (最小元素下标标记位) 来标明当前比较轮的最小元素所在列表list内的下标位置，当本轮（第i轮，i>0）比较结束时，就找出了列表中第i小的元素。此时应该下标为(i-1)的元素和(Min_pos)标记的元素互换。接着新一轮(i=1轮)从第i+1个元素开始比较。依次类比，比较完n轮即可排序结束。
>
> **时间复杂度**
>
> 插入排序平均和最坏： 
> ![n2](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADIAAAAXBAMAAAC7cAEHAAAAMFBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAv3aB7AAAAD3RSTlMAEHZmmasi3Ym7RO8yVM0Ml5alAAAACXBIWXMAAA7EAAAOxAGVKw4bAAABOklEQVQoFWVSIU/DQBh9bddyWXtZEwQOGmZwNCELwYGbbFAIRB0JFk1yAoVaUNMoAg7cVCUJZoRgSbNfMAxqyXjfjV0HvOS+77339b772ivwH29Xfz1dWSfKQqN+1+4WMqmDQXIo3NveO7JebSODMrgW3ktxlorORAk2UmwyqYJrQBKLaXEKhGPggc+3p3QOfnz4VQldwHuikcwYjpeVe2SIplCfNPQXw4i5u96rovncADOsyREt6cbq+UuuRRMX6BimuAAibh7vwycVTLCVMe2WPEv29RGKJoaIDdMjl62M0CnJiSFaNYeX3tKNE320xZdu3iVwItTjBEGNfiBCJoDq7pSWc2o/x/OrFZy6wU1Dbd9GvjeU7yxHL9F8UTryRR1U7igvYoUDqw3szbnqrWNY3LbTunKUf8g3TTo9hY+/v0wAAAAASUVORK5CYII=)
>
> 插入排序最好：
> ![n](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACkAAAATBAMAAAD/rzkOAAAAMFBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAv3aB7AAAAD3RSTlMAEHZmmasi3Ym7RO8yVM0Ml5alAAAACXBIWXMAAA7EAAAOxAGVKw4bAAAA/ElEQVQYGU2PsUoDQRRFz2422bjrmgGFlAbTiI0LIdjY2KVMaTlFIJjCPxDyA4J+hJWddlaWgiDrD8h+QmysLLwzs6s+duaee+fNGxZ+KxoFDBIdTM6c74aQPa9Tw9KIjpq0KAX9udaNoG5SD/fqyzbgW/zBNUSPou1v2LJt750uf8oUX5BLxrvTZ0+pG5loQgqr17KQHehbK83ncAnVCbEoN+yPlB5beJPO6Mqmhnwt96A11HpiYP3cpNZfaZh7rbfhI/MUXcG5QnYMnZpZBy7k+uND69K4Ii55eYeJs0319Hqo2xactubv2KULt6kSEzTsWRX09H8INljJD292JgaQtVzOAAAAAElFTkSuQmCC)
>
> **空间复杂度**
> ![1](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACcAAAATBAMAAADhZgm9AAAAMFBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAv3aB7AAAAD3RSTlMAEHZmmasi3Ym7RO8yVM0Ml5alAAAACXBIWXMAAA7EAAAOxAGVKw4bAAAA4ElEQVQYGU2PPQrCQBCF30pMNPFnC8FS0UZEUBA7G2+Q0jKFIDbeQLCxU9BDWNnpPcQj5AAW2liIiG/HbMjA7Hvvy+wkAdJSTbH/U7WGExPzwlATGWnMNV0X8O9AeUBfCNl7mhhu7yMKnDjlP5IJA3eAulBLDMWIxsAjbz6p5RcQUAXSeGadw+uehVWgumYIQmBpYaDRaDL0I+BqoacRrBnO7LqF3OnE/BezN/sitQKmZqiiebzZC3ah3YkoyN2gNt8tMDQpKZdfIHVINBvShwJn/wnH7E7Lv4kdp0BMZM8fNIYoFO8nUDMAAAAASUVORK5CYII=)


```python
import random
import time

class RandomList(object):
    
    def __init__(self,len,random_range):
        self.list = []
        for i in range(len):
            random.seed(random.randint(0,i*len))
            self.list.append(random.randint(0,random_range))
        self.len = len
    
    def insert_sort(self):
        l = self.list
        for i in range(self.len):
            for y in range(i):
                if l[i] < l[y]:
                    l[i], l[y] = l[y], l[i]

                    
l = RandomList(500,10000)
print(l.list)
start_time = time.time()
l.insert_sort()
end_time = time.time()
print(l.list)
print(end_time - start_time)
```

    [6311, 6042, 2607, 7930, 6795, 6101, 8314, 737, 388, 4069, 9710, 3811, 890, 8443, 5283, 5761, 6788, 1763, 8910, 6690, 6806, 2045, 745, 5243, 9638, 4088, 8401, 8859, 5809, 3200, 8721, 2018, 8557, 1304, 6726, 5484, 547, 3835, 8308, 8839, 5582, 1397, 4007, 2872, 3220, 1534, 7584, 5678, 7609, 1333, 2052, 9548, 322, 1688, 7369, 9235, 2792, 2125, 603, 4481, 2410, 9781, 5267, 7590, 3386, 6270, 465, 1774, 6238, 5655, 1268, 9625, 8056, 3966, 8696, 1981, 8256, 7710, 428, 127, 1190, 3858, 3996, 5996, 6315, 6311, 360, 3081, 8014, 3977, 7958, 6141, 1517, 4262, 9838, 4763, 7907, 7734, 8197, 7301, 2050, 9830, 2503, 6690, 1362, 136, 9309, 4103, 5643, 9211, 164, 1739, 1685, 1515, 912, 7070, 120, 7414, 3800, 7907, 4034, 2411, 9125, 3511, 9964, 7091, 4763, 7717, 4676, 1577, 2722, 8641, 8686, 3565, 3555, 3136, 7584, 779, 3032, 5783, 6191, 9536, 4648, 9998, 5414, 5917, 7776, 27, 2122, 7759, 8680, 3257, 192, 1028, 2576, 4550, 7324, 4643, 384, 7835, 7012, 885, 57, 5430, 6630, 2411, 5024, 5777, 1864, 129, 7575, 5885, 4177, 1268, 3531, 6703, 6644, 5915, 3245, 997, 5333, 9198, 8365, 7195, 7725, 4262, 7028, 4661, 2414, 4418, 713, 7244, 9585, 5249, 8545, 9033, 3704, 6395, 8238, 4893, 1817, 6746, 1346, 1780, 3418, 1611, 1777, 9782, 7162, 1809, 9232, 9385, 1885, 5329, 762, 1875, 4517, 8933, 4127, 4246, 9749, 1029, 1809, 2255, 5206, 1561, 1278, 7905, 4072, 2435, 8019, 3169, 7903, 4334, 4606, 1799, 9981, 1194, 5873, 8467, 9, 6529, 6592, 7096, 7598, 1581, 9092, 8231, 7378, 9565, 9864, 5742, 4397, 4779, 4421, 4984, 3450, 5660, 8152, 6305, 5413, 8249, 6776, 310, 8731, 6603, 3298, 6105, 2475, 9702, 3980, 7119, 3301, 6716, 8019, 3034, 5192, 35, 8650, 8597, 5923, 3174, 6932, 5924, 7079, 2187, 3752, 1162, 8480, 8353, 5102, 1238, 8026, 7468, 6081, 2282, 7589, 2298, 5395, 156, 3636, 9169, 2078, 7596, 8079, 2466, 2903, 6958, 3048, 6299, 7624, 6170, 3423, 5045, 1837, 5047, 4117, 9113, 7390, 1987, 3455, 5405, 2567, 5837, 3485, 9201, 5735, 9219, 3535, 4761, 4548, 3831, 7476, 9613, 130, 8994, 9361, 2594, 620, 5975, 5238, 1079, 1099, 8332, 8864, 3485, 5125, 3470, 6461, 6872, 9060, 6060, 7966, 4193, 8962, 9832, 9708, 6199, 1816, 2673, 9699, 1694, 5248, 5015, 2737, 6296, 3215, 4585, 2494, 5746, 7742, 5634, 9625, 2224, 839, 3272, 8916, 2138, 3059, 1846, 8924, 5198, 2171, 5049, 9304, 7586, 4481, 6516, 7900, 9843, 4612, 2451, 8410, 8974, 9029, 5378, 8635, 683, 3616, 118, 2266, 8293, 7042, 6599, 4493, 4313, 4294, 7019, 3729, 8042, 5494, 6072, 8582, 6755, 5144, 3059, 2957, 9541, 1259, 7844, 2555, 8313, 9812, 3280, 8455, 5308, 4854, 1333, 4026, 183, 165, 7464, 5843, 9249, 212, 9589, 7392, 8670, 7842, 5148, 897, 4811, 5787, 6727, 3948, 6755, 1068, 6434, 3833, 4656, 4603, 9709, 240, 5343, 40, 3792, 9592, 5492, 556, 9592, 3855, 9904, 9461, 406, 9867, 7652, 2369, 9964, 1459, 6768, 3790, 7474, 4839, 7650, 3318, 1644, 947, 2620, 7482, 9951, 2219, 1016, 9167, 7454, 7922, 3138, 1009, 2665, 544, 1945, 645, 7817, 5146, 3001, 5849, 9456, 2507, 4343, 895, 1140]
    [9, 27, 35, 40, 57, 118, 120, 127, 129, 130, 136, 156, 164, 165, 183, 192, 212, 240, 310, 322, 360, 384, 388, 406, 428, 465, 544, 547, 556, 603, 620, 645, 683, 713, 737, 745, 762, 779, 839, 885, 890, 895, 897, 912, 947, 997, 1009, 1016, 1028, 1029, 1068, 1079, 1099, 1140, 1162, 1190, 1194, 1238, 1259, 1268, 1268, 1278, 1304, 1333, 1333, 1346, 1362, 1397, 1459, 1515, 1517, 1534, 1561, 1577, 1581, 1611, 1644, 1685, 1688, 1694, 1739, 1763, 1774, 1777, 1780, 1799, 1809, 1809, 1816, 1817, 1837, 1846, 1864, 1875, 1885, 1945, 1981, 1987, 2018, 2045, 2050, 2052, 2078, 2122, 2125, 2138, 2171, 2187, 2219, 2224, 2255, 2266, 2282, 2298, 2369, 2410, 2411, 2411, 2414, 2435, 2451, 2466, 2475, 2494, 2503, 2507, 2555, 2567, 2576, 2594, 2607, 2620, 2665, 2673, 2722, 2737, 2792, 2872, 2903, 2957, 3001, 3032, 3034, 3048, 3059, 3059, 3081, 3136, 3138, 3169, 3174, 3200, 3215, 3220, 3245, 3257, 3272, 3280, 3298, 3301, 3318, 3386, 3418, 3423, 3450, 3455, 3470, 3485, 3485, 3511, 3531, 3535, 3555, 3565, 3616, 3636, 3704, 3729, 3752, 3790, 3792, 3800, 3811, 3831, 3833, 3835, 3855, 3858, 3948, 3966, 3977, 3980, 3996, 4007, 4026, 4034, 4069, 4072, 4088, 4103, 4117, 4127, 4177, 4193, 4246, 4262, 4262, 4294, 4313, 4334, 4343, 4397, 4418, 4421, 4481, 4481, 4493, 4517, 4548, 4550, 4585, 4603, 4606, 4612, 4643, 4648, 4656, 4661, 4676, 4761, 4763, 4763, 4779, 4811, 4839, 4854, 4893, 4984, 5015, 5024, 5045, 5047, 5049, 5102, 5125, 5144, 5146, 5148, 5192, 5198, 5206, 5238, 5243, 5248, 5249, 5267, 5283, 5308, 5329, 5333, 5343, 5378, 5395, 5405, 5413, 5414, 5430, 5484, 5492, 5494, 5582, 5634, 5643, 5655, 5660, 5678, 5735, 5742, 5746, 5761, 5777, 5783, 5787, 5809, 5837, 5843, 5849, 5873, 5885, 5915, 5917, 5923, 5924, 5975, 5996, 6042, 6060, 6072, 6081, 6101, 6105, 6141, 6170, 6191, 6199, 6238, 6270, 6296, 6299, 6305, 6311, 6311, 6315, 6395, 6434, 6461, 6516, 6529, 6592, 6599, 6603, 6630, 6644, 6690, 6690, 6703, 6716, 6726, 6727, 6746, 6755, 6755, 6768, 6776, 6788, 6795, 6806, 6872, 6932, 6958, 7012, 7019, 7028, 7042, 7070, 7079, 7091, 7096, 7119, 7162, 7195, 7244, 7301, 7324, 7369, 7378, 7390, 7392, 7414, 7454, 7464, 7468, 7474, 7476, 7482, 7575, 7584, 7584, 7586, 7589, 7590, 7596, 7598, 7609, 7624, 7650, 7652, 7710, 7717, 7725, 7734, 7742, 7759, 7776, 7817, 7835, 7842, 7844, 7900, 7903, 7905, 7907, 7907, 7922, 7930, 7958, 7966, 8014, 8019, 8019, 8026, 8042, 8056, 8079, 8152, 8197, 8231, 8238, 8249, 8256, 8293, 8308, 8313, 8314, 8332, 8353, 8365, 8401, 8410, 8443, 8455, 8467, 8480, 8545, 8557, 8582, 8597, 8635, 8641, 8650, 8670, 8680, 8686, 8696, 8721, 8731, 8839, 8859, 8864, 8910, 8916, 8924, 8933, 8962, 8974, 8994, 9029, 9033, 9060, 9092, 9113, 9125, 9167, 9169, 9198, 9201, 9211, 9219, 9232, 9235, 9249, 9304, 9309, 9361, 9385, 9456, 9461, 9536, 9541, 9548, 9565, 9585, 9589, 9592, 9592, 9613, 9625, 9625, 9638, 9699, 9702, 9708, 9709, 9710, 9749, 9781, 9782, 9812, 9830, 9832, 9838, 9843, 9864, 9867, 9904, 9951, 9964, 9964, 9981, 9998]
    0.014961719512939453


### 6.4 快速排序
>**快速排序原理**
> 快排中的排序是将列表中的每个数与列表的边界（比如是右边界，right）元素来比较大小，找出该元素最终在列表中的真实位置（记为pivot），期间需要借助两个下标标志变量i，k。起始时，i和k都在同一位置（左边界，left），依次将list\[i\]与边界元素list\[right\]比较，当list\[i\]\<list\[right\]时，则i+1，k+1（指向下一个位置），当list\[i\]\>list\[right\]时，则i+1，k不变，接着比较，直到找出选定元素，最终的划分位置（pivot），即k值。
> 其利用分治+递归思想，每次进入快排函数，首先调用一次分治比较函数，得出新的pivot位置，再将pivot左右两边区间的列表传递给下两个快排函数。
> 
>
> **时间复杂度**
>
> 快速排序平均和最好： 
> ![nlogn](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAFIAAAATBAMAAADxBkdhAAAAMFBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAv3aB7AAAAD3RSTlMAEHZmmasi3Ym7RO8yVM0Ml5alAAAACXBIWXMAAA7EAAAOxAGVKw4bAAABwElEQVQoFWWSv4vTYBjHP/nRNJc2bcDhBgeDRRAH7XEUnY663RicHG7IoCgi5wmOCoF6o1D/g87WodrNqaMgSG1dXI6AsxCXToXzm7a5S/GFN9/P93me93nz5g1cDCO8wP/AXEWM6/v3c6hs8u6rDZTE6OamE/AkkN7KTT7+rGXrOZdzI82+IC1SfwsoaUM8VD8vA7+9SXgnpYoC3SnGWKa+hJ14E3W7GyiLF+Hme/kLqElaVzoTGmo+uzfB6O0Fys329o8kI6p9iZ1BFZ59a/t9mjF26Iw4Dq5qjfNxzC+VZDQTSS2CY5jexYwYwgEs9Qma8fytb51wQyWfuBZK7sTwXXpIJeQUxhhLnXLohJXETnig1EtqieSz5q7ml3zr3zgLrMxMOa2nVr82QKfQe9qpbid/V53IyTjzWDyvZzRCu6s1uMkL/HSQVxpv4KEKaQRYKYeWkbV5TQc/stRrNzjATto4aua2bsZ5pTnFbPP1B70BT+c6dW82giNa1N+piQLFcKKCCtU9m5N47XaCIip9X+IVVqd8IFxHH5eTj8oGbnOGc36erKOr/7Io8KYFrfTnPLn01uSSRfGW2zIO/ANa8mB4VW8n4wAAAABJRU5ErkJggg==)
>
> 快速排序最坏： 
> ![n2](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADIAAAAXBAMAAAC7cAEHAAAAMFBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAv3aB7AAAAD3RSTlMAEHZmmasi3Ym7RO8yVM0Ml5alAAAACXBIWXMAAA7EAAAOxAGVKw4bAAABOklEQVQoFWVSIU/DQBh9bddyWXtZEwQOGmZwNCELwYGbbFAIRB0JFk1yAoVaUNMoAg7cVCUJZoRgSbNfMAxqyXjfjV0HvOS+77339b772ivwH29Xfz1dWSfKQqN+1+4WMqmDQXIo3NveO7JebSODMrgW3ktxlorORAk2UmwyqYJrQBKLaXEKhGPggc+3p3QOfnz4VQldwHuikcwYjpeVe2SIplCfNPQXw4i5u96rovncADOsyREt6cbq+UuuRRMX6BimuAAibh7vwycVTLCVMe2WPEv29RGKJoaIDdMjl62M0CnJiSFaNYeX3tKNE320xZdu3iVwItTjBEGNfiBCJoDq7pSWc2o/x/OrFZy6wU1Dbd9GvjeU7yxHL9F8UTryRR1U7igvYoUDqw3szbnqrWNY3LbTunKUf8g3TTo9hY+/v0wAAAAASUVORK5CYII=)
>
> **空间复杂度**
> 
> ![logn](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAEcAAAATBAMAAAAwgQ3NAAAAMFBMVEX///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAv3aB7AAAAD3RSTlMAEHZmmasi3Ym7RO8yVM0Ml5alAAAACXBIWXMAAA7EAAAOxAGVKw4bAAABh0lEQVQoFV1QPUvDUBQ9SdukJsZEFHRrsYuoaKAUqyit4tBF6OgYRBQVLP6AQgdFBwv6D1zEwUHRzSmjINQ6uErUP1CX4iDoeUkb0l7ycs/Hfe/e94AwpHQIoyBQpYnsilATwElRgN4Y9WnOwo5FNAUMNXsLBDNs/pJlrnMCDzAt5v7wKNzQ0FrBjuv+AsHrgPTAPPgLDDjAkRD744qdvikabUBn/iLMnAHj2WGhZkZyrm+oYpw426nMrF3FPpQP//y9Z9uga/Kr0dTLwAFHu0PMg+nykm0jX2zOQ6ahW0ilWTTnAA3/orqNlHvL8k1soIQEXdWCXmPRPdcYn8lGxUEBs3yXBhbwCNPxZ4p7fGt2FoOb2+4L8Ik1UY5TpYV3zTekKngwY4itY1DdWBlvKDiQDjlfKQbs0kxmJh1RJDeRXIRSz1Janubxrmzj6RWgEIbCi4RxDMwoHXYRqgRRUoV2KQdmz2ZsdXfInuGh8vcT8LjV1UXWmh1mrOcj+lIEEzq9tMOo/gNxkElXrDONgQAAAABJRU5ErkJggg==)


```python
import random
import time

class RandomList(object):
    
    def __init__(self,len,random_range):
        self.list = []
        for i in range(len):
            random.seed(random.randint(0,i*len))
            self.list.append(random.randint(0,random_range))
        self.len = len
    
    def partition(self, left, right):
        l = self.list
        i = k = left
        while i < right:
            if l[i] < l[right]:
                l[i], l[k] = l[k], l[i]
                i += 1
                k += 1
            else:
                i += 1
        l[k], l[right] = l[right], l[k]
        return k
    
    def quick_sort(self,left,right):
        if left < right:
            pivot = self.partition(left, right)
            self.quick_sort(left, pivot - 1)
            self.quick_sort(pivot + 1, right)
            

l = RandomList(500,10000)
print(l.list)
start_time = time.time()
l.quick_sort(0,l.len - 1)
end_time = time.time()
print(l.list)
print(end_time - start_time)
```

    [6311, 6042, 2607, 7930, 6795, 6101, 8314, 737, 388, 4069, 9710, 3811, 890, 8443, 5283, 5761, 6788, 1763, 8910, 6690, 6806, 2045, 745, 5243, 9638, 4088, 8401, 8859, 5809, 3200, 8721, 2018, 8557, 1304, 6726, 5484, 547, 3835, 8308, 8839, 5582, 1397, 4007, 2872, 3220, 1534, 7584, 5678, 7609, 1333, 2052, 9548, 322, 1688, 7369, 9235, 2792, 2125, 603, 4481, 2410, 9781, 5267, 7590, 3386, 6270, 465, 1774, 6238, 5655, 1268, 9625, 8056, 3966, 8696, 1981, 8256, 7710, 428, 127, 1190, 3858, 3996, 5996, 6315, 6311, 360, 3081, 8014, 3977, 7958, 6141, 1517, 4262, 9838, 4763, 7907, 7734, 8197, 7301, 2050, 9830, 2503, 6690, 1362, 136, 9309, 4103, 5643, 9211, 164, 1739, 1685, 1515, 912, 7070, 120, 7414, 3800, 7907, 4034, 2411, 9125, 3511, 9964, 7091, 4763, 7717, 4676, 1577, 2722, 8641, 8686, 3565, 3555, 3136, 7584, 779, 3032, 5783, 6191, 9536, 4648, 9998, 5414, 5917, 7776, 27, 2122, 7759, 8680, 3257, 192, 1028, 2576, 4550, 7324, 4643, 384, 7835, 7012, 885, 57, 5430, 6630, 2411, 5024, 5777, 1864, 129, 7575, 5885, 4177, 1268, 3531, 6703, 6644, 5915, 3245, 997, 5333, 9198, 8365, 7195, 7725, 4262, 7028, 4661, 2414, 4418, 713, 7244, 9585, 5249, 8545, 9033, 3704, 6395, 8238, 4893, 1817, 6746, 1346, 1780, 3418, 1611, 1777, 9782, 7162, 1809, 9232, 9385, 1885, 5329, 762, 1875, 4517, 8933, 4127, 4246, 9749, 1029, 1809, 2255, 5206, 1561, 1278, 7905, 4072, 2435, 8019, 3169, 7903, 4334, 4606, 1799, 9981, 1194, 5873, 8467, 9, 6529, 6592, 7096, 7598, 1581, 9092, 8231, 7378, 9565, 9864, 5742, 4397, 4779, 4421, 4984, 3450, 5660, 8152, 6305, 5413, 8249, 6776, 310, 8731, 6603, 3298, 6105, 2475, 9702, 3980, 7119, 3301, 6716, 8019, 3034, 5192, 35, 8650, 8597, 5923, 3174, 6932, 5924, 7079, 2187, 3752, 1162, 8480, 8353, 5102, 1238, 8026, 7468, 6081, 2282, 7589, 2298, 5395, 156, 3636, 9169, 2078, 7596, 8079, 2466, 2903, 6958, 3048, 6299, 7624, 6170, 3423, 5045, 1837, 5047, 4117, 9113, 7390, 1987, 3455, 5405, 2567, 5837, 3485, 9201, 5735, 9219, 3535, 4761, 4548, 3831, 7476, 9613, 130, 8994, 9361, 2594, 620, 5975, 5238, 1079, 1099, 8332, 8864, 3485, 5125, 3470, 6461, 6872, 9060, 6060, 7966, 4193, 8962, 9832, 9708, 6199, 1816, 2673, 9699, 1694, 5248, 5015, 2737, 6296, 3215, 4585, 2494, 5746, 7742, 5634, 9625, 2224, 839, 3272, 8916, 2138, 3059, 1846, 8924, 5198, 2171, 5049, 9304, 7586, 4481, 6516, 7900, 9843, 4612, 2451, 8410, 8974, 9029, 5378, 8635, 683, 3616, 118, 2266, 8293, 7042, 6599, 4493, 4313, 4294, 7019, 3729, 8042, 5494, 6072, 8582, 6755, 5144, 3059, 2957, 9541, 1259, 7844, 2555, 8313, 9812, 3280, 8455, 5308, 4854, 1333, 4026, 183, 165, 7464, 5843, 9249, 212, 9589, 7392, 8670, 7842, 5148, 897, 4811, 5787, 6727, 3948, 6755, 1068, 6434, 3833, 4656, 4603, 9709, 240, 5343, 40, 3792, 9592, 5492, 556, 9592, 3855, 9904, 9461, 406, 9867, 7652, 2369, 9964, 1459, 6768, 3790, 7474, 4839, 7650, 3318, 1644, 947, 2620, 7482, 9951, 2219, 1016, 9167, 7454, 7922, 3138, 1009, 2665, 544, 1945, 645, 7817, 5146, 3001, 5849, 9456, 2507, 4343, 895, 1140]
    [9, 27, 35, 40, 57, 118, 120, 127, 129, 130, 136, 156, 164, 165, 183, 192, 212, 240, 310, 322, 360, 384, 388, 406, 428, 465, 544, 547, 556, 603, 620, 645, 683, 713, 737, 745, 762, 779, 839, 885, 890, 895, 897, 912, 947, 997, 1009, 1016, 1028, 1029, 1068, 1079, 1099, 1140, 1162, 1190, 1194, 1238, 1259, 1268, 1268, 1278, 1304, 1333, 1333, 1346, 1362, 1397, 1459, 1515, 1517, 1534, 1561, 1577, 1581, 1611, 1644, 1685, 1688, 1694, 1739, 1763, 1774, 1777, 1780, 1799, 1809, 1809, 1816, 1817, 1837, 1846, 1864, 1875, 1885, 1945, 1981, 1987, 2018, 2045, 2050, 2052, 2078, 2122, 2125, 2138, 2171, 2187, 2219, 2224, 2255, 2266, 2282, 2298, 2369, 2410, 2411, 2411, 2414, 2435, 2451, 2466, 2475, 2494, 2503, 2507, 2555, 2567, 2576, 2594, 2607, 2620, 2665, 2673, 2722, 2737, 2792, 2872, 2903, 2957, 3001, 3032, 3034, 3048, 3059, 3059, 3081, 3136, 3138, 3169, 3174, 3200, 3215, 3220, 3245, 3257, 3272, 3280, 3298, 3301, 3318, 3386, 3418, 3423, 3450, 3455, 3470, 3485, 3485, 3511, 3531, 3535, 3555, 3565, 3616, 3636, 3704, 3729, 3752, 3790, 3792, 3800, 3811, 3831, 3833, 3835, 3855, 3858, 3948, 3966, 3977, 3980, 3996, 4007, 4026, 4034, 4069, 4072, 4088, 4103, 4117, 4127, 4177, 4193, 4246, 4262, 4262, 4294, 4313, 4334, 4343, 4397, 4418, 4421, 4481, 4481, 4493, 4517, 4548, 4550, 4585, 4603, 4606, 4612, 4643, 4648, 4656, 4661, 4676, 4761, 4763, 4763, 4779, 4811, 4839, 4854, 4893, 4984, 5015, 5024, 5045, 5047, 5049, 5102, 5125, 5144, 5146, 5148, 5192, 5198, 5206, 5238, 5243, 5248, 5249, 5267, 5283, 5308, 5329, 5333, 5343, 5378, 5395, 5405, 5413, 5414, 5430, 5484, 5492, 5494, 5582, 5634, 5643, 5655, 5660, 5678, 5735, 5742, 5746, 5761, 5777, 5783, 5787, 5809, 5837, 5843, 5849, 5873, 5885, 5915, 5917, 5923, 5924, 5975, 5996, 6042, 6060, 6072, 6081, 6101, 6105, 6141, 6170, 6191, 6199, 6238, 6270, 6296, 6299, 6305, 6311, 6311, 6315, 6395, 6434, 6461, 6516, 6529, 6592, 6599, 6603, 6630, 6644, 6690, 6690, 6703, 6716, 6726, 6727, 6746, 6755, 6755, 6768, 6776, 6788, 6795, 6806, 6872, 6932, 6958, 7012, 7019, 7028, 7042, 7070, 7079, 7091, 7096, 7119, 7162, 7195, 7244, 7301, 7324, 7369, 7378, 7390, 7392, 7414, 7454, 7464, 7468, 7474, 7476, 7482, 7575, 7584, 7584, 7586, 7589, 7590, 7596, 7598, 7609, 7624, 7650, 7652, 7710, 7717, 7725, 7734, 7742, 7759, 7776, 7817, 7835, 7842, 7844, 7900, 7903, 7905, 7907, 7907, 7922, 7930, 7958, 7966, 8014, 8019, 8019, 8026, 8042, 8056, 8079, 8152, 8197, 8231, 8238, 8249, 8256, 8293, 8308, 8313, 8314, 8332, 8353, 8365, 8401, 8410, 8443, 8455, 8467, 8480, 8545, 8557, 8582, 8597, 8635, 8641, 8650, 8670, 8680, 8686, 8696, 8721, 8731, 8839, 8859, 8864, 8910, 8916, 8924, 8933, 8962, 8974, 8994, 9029, 9033, 9060, 9092, 9113, 9125, 9167, 9169, 9198, 9201, 9211, 9219, 9232, 9235, 9249, 9304, 9309, 9361, 9385, 9456, 9461, 9536, 9541, 9548, 9565, 9585, 9589, 9592, 9592, 9613, 9625, 9625, 9638, 9699, 9702, 9708, 9709, 9710, 9749, 9781, 9782, 9812, 9830, 9832, 9838, 9843, 9864, 9867, 9904, 9951, 9964, 9964, 9981, 9998]
    0.002993345260620117


## 7、完成二叉树的层次建树，并实现前序遍历，中序遍历，后序遍历


```python
from collections import deque

class TreeNode(object):
    def __init__(self):
        self.node_val = None
        self.lchirld = None
        self.rchirld = None

class Tree(object):
    
    def __init__(self):
        self.root = None
        #辅助队列
        self.arr = deque()
    
    def add_tree_node(self,val):
        node = TreeNode()
        node.node_val = val
        
        #利用辅助队列，始终可以让arr[0]指向添加的位置的父节点。
        self.arr.append(node)
        
        #此时应先判断树是否为空树。
        if self.root == None:
            self.root = node
            return
        
        # 若树根不为空时，则利用辅助队列arr[0]来帮助判断现在插入的节点那个位置是空的。
        else:
            #判断左孩子是否为空。
            if self.arr[0].lchirld == None:
                self.arr[0].lchirld = node
            #判断右孩子是否为空。
            elif self.arr[0].rchirld == None:
                self.arr[0].rchirld = node
                #当该节点的左右孩子节点都加了节点后，
                #此时可以说明当前节点的叶子位置都满了，
                #应该将该节点pop出，指向下一个有空余位置的节点。
                self.arr.popleft()
        return

    
    #前序遍历
    def preorder_traversal(self, node):
        if node:

            print(node.node_val, end=',')
            self.preorder_traversal(node.lchirld)
            self.preorder_traversal(node.rchirld)
            
    
    #中序遍历
    def inorder_traversal(self, node):
        if node:

            self.inorder_traversal(node.lchirld)
            print(node.node_val, end=',')
            self.inorder_traversal(node.rchirld)
    
    #后序遍历
    def postorder_traversal(self, node):
        if node:

            self.postorder_traversal(node.lchirld)
            self.postorder_traversal(node.rchirld)
            print(node.node_val, end=',')

            
            
tree = Tree()
for i in range(16):
    tree.add_tree_node(i)

tree.preorder_traversal(tree.root)
print()
tree.inorder_traversal(tree.root)
print()
tree.postorder_traversal(tree.root)
```

    0,1,3,7,15,8,4,9,10,2,5,11,12,6,13,14,
    15,7,3,8,1,9,4,10,0,11,5,12,2,13,6,14,
    15,7,8,3,9,10,4,1,11,12,5,13,14,6,2,0,

# 难度作业：
_______
**有时间的同学预习一下红黑树**

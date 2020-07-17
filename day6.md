# day6

## 1、返回数字列表中的最大值和最小值


```python
def list_max_num(numList):
    nunmList = numList.sort()
    print(numList[-1])
    
    
numList = [22, 33, 44, 551, 2, 0.1, 3.1, 2, 22, 43, 59]
list_max_num(numList)
```

    551


## 2、求两个有序数字列表的公共元素


```python
result = []


def find_list_comm_elem(orderedNumberList1, orderedNumberList2):
    for i1 in range(len(orderedNumberList1)):
        for i2 in range(len(orderedNumberList2)):
            if orderedNumberList1[i1] == orderedNumberList2[i2]:
                result.append(orderedNumberList1[i1])
    print(result)


haha = [1, 7, 14, 16, 25, 29, 30, 38]
hehe = [1, 2, 3, 4, 5, 6]

find_list_comm_elem(hehe, haha)

```

    [1]


## 3、给定一个n个整型元素的列表a，其中有一个元素出现次数超过n / 2，求这个元素


```python
def find_mode_in_list(l):
    b = l.sort()
    print(l[len(l)//2])

a = [4, 2, 3, 4, 45, 4, 5, 4, 4, 4, 5]

find_mode_in_list(a)
```

    4


## 4、统计一个整数对应的二进制数的1的个数。输入一个整数（可正可负，负数就按64位去遍历即可）， 输出该整数的二进制包含1的个数


```python
intNum = -1

print(str(bin(intNum & 0xffffffffffffffff)).count('1'))

```

    64

****
* 会异或的做下面的题，不会的等下周一再做

## 5、（1）.有101个整数，其中有50个数出现了两次，1个数出现了一次， 找出出现了一次的那个数。（大家使用7个数即可）（2）有102个整数，其中有50个数出现了两次，2个数出现了一次， 找出出现了一次的那2个数。（大家使用8个数即可）（第5题提醒，两个相等的数异或为0，一个数和零异或是其自身）


```python
numList = [3, 4, 5, 6, 3, 4, 5, 6, 7]
numList.sort(reverse=True)
l = numList

for i in range(0, len(l), 2):
    if i+1 < len(l):
        if l[i] != l[i+1]:    #可以改成， l[i] ^ l[i+1] != 0
            print(l[i])
            break
    else:
        print(l[i])

```

    7



```python
numList = [3, 4, 5, 6, 3, 4, 5, 6, 1, 2]

numList.sort(reverse=True)
l = numList

for i in range(0, len(l), 2):
        if l[i] != l[i+1]:   #可以改成， l[i] ^ l[i+1] != 0
            print(l[i],l[i+1])
            break


```

    2 1


## 6、给定含有1001个元素的列表，其中存放了1-1000之内的整数，只有一个整数是重复的，请找出这个数


```python
RepeatedNum = 886
l = list(range(1,1001))
l.append(RepeatedNum)
l.sort(reverse=True)
for i in range(len(l)):
    if i+1 < len(l):
        if l[i] == l[i+1]:    #可以改成， l[i] ^ l[i+1] == 0
            print(l[i])
            break
    else:
        print(l[i])
```

    886


## 难度作业
****

## 7、有103个整数，其中有50个数出现了两次，3个数出现了一次， 找出出现了一次的那3个数。（大家使用9个数即可）


```python

```

## 8、给定一个含有n个元素的整型列表，找出列表中的两个元素x和y使得abs(x - y)值最小


```python

```


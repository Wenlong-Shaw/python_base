# day5

## 1、自己定义变量赋值不同的数据类型并打印，并使用type，id等。


```python
(tupleX, tupleY) = ('yes', 'no')
strX = 'this is a string'
intNum = 1
floatNum = 1.234
listX = [1,2,3]
dictX = {"name":"LiMing","age":18}
print(tupleX,strX,intNum,floatNum,listX,dictX)
print(type(tupleX),type(tupleY),type(strX),type(intNum),type(floatNum),type(listX),type(dictX))
```

    yes this is a string 1 1.234 [1, 2, 3] {'name': 'LiMing', 'age': 18}
    <class 'str'> <class 'str'> <class 'str'> <class 'int'> <class 'float'> <class 'list'> <class 'dict'>


## 2、练习课件上的读取标准输入，实现一个简单的个人名片题目。


```python
"""
个人名片实现
需求依次输入：姓名、公司、职位、电话和邮箱
"""
staffName = input("请输入职工姓名：")
companyNmae = input("请输入公司名称：")
staffTitle = input("请输入职工职位：")
phoneNum = input("请输入电话号码：")
email = input("请输入email")

print("*"*30)
print(companyNmae,"\n")
print("{0}\t{1}".format(staffName,staffTitle))
print("Email: %s"%email)
print("电话号码：%s"%phoneNum)
print("*"*30)
```

    请输入职工姓名：Li
    请输入公司名称：hahaha
    请输入职工职位：Boss
    请输入电话号码：1234567
    请输入email123@123.com
    ******************************
    hahaha 
    
    Li	Boss
    Email: 123@123.com
    电话号码：1234567
    ******************************


## 3、实现从1到100之间的奇数求和


```python
sum = 0
for num in range(1,101):
    if (num % 2) ==1:
        sum = sum + num
print(sum)
```

    2500


## 4、打印九九乘法表


```python
sumStr = ['']*9
sumXY = 0
for x in range(1,10):
    for y in range(1,x+1):
        sumXY = x * y
        sumStr[x-1] += str(str(y)+'×'+str(x)+'='+str(sumXY)+'\t')
    print(sumStr[x-1])
```

    1×1=1	
    1×2=2	2×2=4	
    1×3=3	2×3=6	3×3=9	
    1×4=4	2×4=8	3×4=12	4×4=16	
    1×5=5	2×5=10	3×5=15	4×5=20	5×5=25	
    1×6=6	2×6=12	3×6=18	4×6=24	5×6=30	6×6=36	
    1×7=7	2×7=14	3×7=21	4×7=28	5×7=35	6×7=42	7×7=49	
    1×8=8	2×8=16	3×8=24	4×8=32	5×8=40	6×8=48	7×8=56	8×8=64	
    1×9=9	2×9=18	3×9=27	4×9=36	5×9=45	6×9=54	7×9=63	8×9=72	9×9=81	


## 5、打印如下图形：

### 5.1、实心菱形


```python
for i in range(1, 10):
    if i <= 5:
        i = i
    if i > 5:
        i = 10 - i
    if (i % 5) == 0:
        print('* * * * *')
    if (i % 5) == 1:
        print('    *    ')
    if (i % 5) == 2:
        print('   * *   ')
    if (i % 5) == 3:
        print('  * * *  ')
    if (i % 5) == 4:
        print(' * * * * ')
```

        *    
       * *   
      * * *  
     * * * * 
    * * * * *
     * * * * 
      * * *  
       * *   
        *    


### 5.2、空心菱形


```python
for i in range(1, 10):
    if i <= 5:
        i = i
    if i > 5:
        i = 10 - i
    if (i % 5) == 0:
        print('*       *')
    if (i % 5) == 1:
        print('    *    ')
    if (i % 5) == 2:
        print('   * *   ')
    if (i % 5) == 3:
        print('  *   *  ')
    if (i % 5) == 4:
        print(' *     * ')
```

        *    
       * *   
      *   *  
     *     * 
    *       *
     *     * 
      *   *  
       * *   
        *    


### 5.3、实心心形


```python
str = "*"
allStr = []
for y in range(14, -14, -1):
   row = []
   lst_con = ''
   for x in range(-35, 35):
        formula = ((x*0.05)**2+(y*0.1)**2-1)**3-(x*0.05)**2*(y*0.1)**3
        if formula <= 0:
            lst_con += str[(x) % len(str)]
        else:
            lst_con += ' '
   row.append(lst_con)
   allStr += row
print('\n'.join(allStr))
```


​                                                                          
                         *********           *********                    
                     *****************   *****************                
                   *****************************************              
                  *******************************************             
                 *********************************************            
                 *********************************************            
                 *********************************************            
                 *********************************************            
                 *********************************************            
                 *********************************************            
                  *******************************************             
                   *****************************************              
                   *****************************************              
                     *************************************                
                      ***********************************                 
                       *********************************                  
                         *****************************                    
                           *************************                      
                             *********************                        
                                ***************                           
                                   *********                              
                                      ***                                 
                                       *                                  


​                                                                          
​                                                                          
​    


```python

```

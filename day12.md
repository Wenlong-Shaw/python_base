# day12

## 1、通过readline依次读取文件每一行并打印


```python
with open('text', mode='a+', encoding='utf-8') as f:
    while True:
        cont = f.readline()
        
        #判断是否读取到内容
        if not cont:
            break
        print(cont)
    f.close()
```

## 2、读取readme文件内容，复制到readme1中


```python
#对于小文件可以一次性全部读取至内存，再写入其他文件。
#分别打开两个文件
fr = open('readme')
fw = open('readme1')

#读取readme文件内容，并写入readme1中
cont = fr.read()
fw.write(cont)

#操作完毕，需要关闭文件
fr.close()
fw.close()

#对于大文件则可以一次读取部分文件内容至内存，再新增方式写入至其他文件。
#分别打开两个文件
fr = open('readme')
fw = open('readme1', 'a+')

#每次读取一行内容，并写入
while True:
    cont = fr.readline()
    
    #判断是否读取到内容
    if not cont:
        break
    fw.write(cont)

#操作完毕，需要关闭文件
fr.close()
fw.close()
```

## 3、通过seek从文件开头偏移5个字节，然后把文件剩余内容读取


```python
with open('text',mode='r+',encoding='utf-8') as f:
    f.seek(5,0)
    txt = f.read()
    print(txt)
```

    n
    Python
    Python
    Python
    Python
    Python


​    

## 4、练习open的a+，w+模式，感受他们与r+的区别


```python
#a+模式：以读写方式打开文件。如果该文件已存在，
#文件指针将会放在文件的结尾。
#如果文件不存在，创建新文件进行写入
with open('text', mode='a+', encoding='utf-8') as f:
    #对于打开过的文件一定要记得用seek将文件指针复位至内容开头位置，才能把文件内容重新全部读取。
    f.seek(0,0)
    while True:
        txt = f.readline()
        if not txt:
            break
        print(txt)
    f.close()

    
#以读写方式打开文件。如果文件存在会被`覆盖`（即使什么操作也不做，只要以这种方式打开文件就会被覆盖（清空））。
#如果文件不存在，创建新文件。
with open('text', mode='w+', encoding='utf-8') as f:
    #对于打开过的文件一定要记得用seek将文件指针复位至内容开头位置，才能把文件内容重新全部读取。
    f.seek(0,0)
    while True:
        txt = f.readline()
        if not txt:
            break
        print(txt)
    f.close()

#以读写方式打开文件。文件的指针将会放在文件的开头（每次打开文件指针都在开头位置）。
#如果文件不存在，抛出异常  
with open('text', mode='r+', encoding='utf-8') as f:
    #对于打开过的文件一定要记得用seek将文件指针复位至内容开头位置，才能把文件内容重新全部读取。
    f.seek(0,0)
    while True:
        txt = f.readline()
        if not txt:
            break
        print(txt)
    f.close()
```

    Python
    
    Python
    
    Python
    
    Python
    
    Python
    
    Python


​    

## 5、练习rb+模式，感受与r+模式的区别


```python
# rb+ 模式与r+，不同的是读写的文件内容是以字节形式。
with open('text', mode='rb+', encoding='utf-8') as f:
    #对于打开过的文件一定要记得用seek将文件指针复位至内容开头位置，才能把文件内容重新全部读取。
    f.seek(0,0)
    while True:
        txt = f.readline()
        if not txt:
            break
        print(txt)
    f.close()
```

## 6、对文件进行改名并删除文件


```python
import os

dirs = os.listdir()
pwd = os.getcwd()
os.rename(pwd+'\\test1',pwd+'\\test')
os.remove(pwd+'\\test')
```

## 7、创建文件夹，删除文件夹（均使用相对路径），改变程序执行路径，获取程序当前路径


```python
import os
os.mkdir('./testdir')
pwd = os.getcwd()
print(pwd)
os.chdir('./testdir')
pwd = os.getcwd()
print(pwd)
```

    C:\Users\xwl00\notebook\wangdaopython
    C:\Users\xwl00\notebook\wangdaopython\testdir


## 8、对今天学习的内容通过思维导图进行总结


```python

```

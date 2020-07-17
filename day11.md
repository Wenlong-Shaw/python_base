# day11

## 1、编写类方法，静态方法，并列出他们差异

**类方法与静态方法的定义：**
* 类方法就是针对类对象定义的方法
 - 在类方法内部可以直接访问类属性或者调用其他的类方法

* 静态方法是指，在开发时，如果需要在类中封装一个方法(比如打印输出某些固定句子)，这个方法: .
 * 既不需要访问实例属性或者调用实例方法
 * 也不需要访问类属性或者调用类方法

**类方法与静态方法的差异：**
1. 实例方法--方法内部需要访问实例属性
 * 实例方法内部可以使用类名.访问类属性
2. 类方法--方法内部只需要访问类属性
3. 静态方法--方法内部，不需要访问实例属性和类属性



```python
class Game(object):
    #历史最高分
    top_score = 0
    def __init__(self, player_name):
        self.player_name = player_name
    
    @staticmethod
    def show_help():
        print("帮助信息:让僵尸进入大门")
    
    @classmethod
    def show_top_score(cls):
        print("历史记录%d" % cls.top_score)    #cls.top_score 是类属性。
    
    def start_game(self):
        print("%s开始游戏啦..."% self.player_name)  #self.player_name 是实例属性。

              
# 1.查看游戏的帮助信息
Game.show_help()
#2.查看历史最高分
Game.show_top_score()
# 3.创建游戏对象
game = Game("小李")
game.start_game()

```

    帮助信息:让僵尸进入大门
    历史记录0
    小李开始游戏啦...


## 2、实现单例模式

**单例设计模式**

* 目的：让类创建的对象，在系统中**只有唯一**的一个实例。

* 每一次执行类名()返回的对象，**内存地址是相同的。**



```python
class MusicPlayer(object):
    
    #建立一个实例空间的记录属性
    instance = None
    #建立一个object基类的初始化方法（__init__）调用的标志属性
    initFlag = False
    
    #重写基类的__new__方法，让它在初始化时，优先被调用
    #__new__ 是静态方法，所以应该加 cls。
    def __new__(cls, *args, **kwargs):
        print('开始给对象申请空间')
        
        #判断该对象的实例是否已经申请了空间
        if cls.instance is None:
            #用super调用上一级基类的__new__方法来申请空间。
            cls.instance = super().__new__(cls)
        #先判断，再返回cls.instance，这样就不必重复给实例申请空间了。
        return cls.instance
    
    def __init__(self):
        #判断初始化标志是否为假，判断是否有初始化过实例。
        if not MusicPlayer.initFlag:
            print('开始初始化MusicPlayer')
            #初始化操作...
            
            #初始化操作完毕后记得将initflag置为True。
            MusicPlayer.initFlag = True

player1 = MusicPlayer()
player2 = MusicPlayer()
player3 = MusicPlayer()

#三个先后初始化的实例player对象所再内存空间地址都是一样的。
print(player1,'\n',player2,'\n',player3)
```

    开始给对象申请空间
    开始初始化MusicPlayer
    开始给对象申请空间
    开始给对象申请空间
    <__main__.MusicPlayer object at 0x000001F9A57F0E48> 
     <__main__.MusicPlayer object at 0x000001F9A57F0E48> 
     <__main__.MusicPlayer object at 0x000001F9A57F0E48>


## 3、通过try进行异常捕捉，确保输入的内容一定是一个整型数，然后判断该整型数是否是对称数，12321就是对称数，123321也是对称数，否则就不是。


```python
def judge_num(num):
    s = str(num)
    s_len = len(s)
    if s_len % 2 == 0:
        s1 = list(s[s_len//2:])
        s1.reverse()
        if list(s[0:s_len//2]) == s1:
            return print('这是一个对称数。')
        else:
            return print('这不是一个对称数。')
    else:
        s2 = list(s[(s_len//2):])
        s2.reverse()
        if list(s[0:(s_len//2+1)]) == s2:
            return print('这是一个对称数。')
        else:
            return print('这不是一个对称数。')


flag = True
while flag:
    try:
        num = int(input('请输入一个整型数：'))
        print('您输入的整型数为：', num)
        flag = False
    except TypeError:
        print('请输入正确的整数！')
    except ValueError:
        print('输入的值错误！')
    except Exception as error:
        print('Unkonw error: ', error)
    else:
        print('输入正常。')
        judge_num(num)
    finally:
        print('本次输入结束。')
```

    请输入一个整型数：123321
    您输入的整型数为： 123321
    输入正常。
    这是一个对称数。
    本次输入结束。


## 4、编写wd_message，将其通过setup打包，发布，安装


```python

```

## 5、以可读可写打开一个文件，然后写入“人生苦短 我用Python”，关闭文件


```python
with open('text', mode='r+', encoding='utf-8') as t:
    #write 会从头覆盖原有的文本内容。
    #需要以追加的方式些内容应该在访问方式 mode='a'
    length = t.write('人生苦短，我用Python。')
    print(length)
    
    #使用seek方法，修改已经在写操作指向文件末尾的指针。
    #否则将从上次写操作结束的指针位置开始读，这样就是从末尾读，什么内容都读不到。
    t.seek(0,0)
    print(t.read())
    #用with open()的格式可以不用在结束时写close()，因为当退出当前域时，会自动关闭文件。
    f.close()
```

    14
    人生苦短，我用Python。


# 难度作业
-------

## 6、有时间的同学预习明天的内容，可以提前自行写一下深度优先遍历


```python

```

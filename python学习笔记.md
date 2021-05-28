### python学习笔记

***python是一门解释性语言

拓展库安装使用清华镜像

`pip install matplotlib -i https://pypi.tuna.tsinghua.edu.cn/simple`

1.简单数据类型

```python 
整数： integer int 浮点数：float 字符串：string str 布尔型：boolean bool
列表[]:
    列表(list)是容纳一系列元素的容器。
    特点：
    1.列表可以同时容纳不同类型的元素
    2.正向从0下标开始递增，逆向从-1开始递减。
    3.列表可以嵌套视作二维数组
    4.名字绑定，不同的引用指向同一个列表时作用即会同一化。
    方法：
    	添加：
    	列表名.append(参数) #往后追加元素
        列表名.insert(index,参数) #在指定下标插入元素
        
        删除：
        del 列表名[index]
        列表名.pop(index) #pop函数将列表视作一个栈，若index为null则默认删除最后一个元素，否则删除指定 		下标元素
        列表名.remove(列表中的元素)
        
        排序：
        列表名.sort(?)	
        特点：原列表内部元素会发生改变。
        """
         ?: null 元素按非递减顺序排列
         ?: reverse=True	元素按递减顺序排列
         ?: key=len 按元素长度生成的key值进行排序
         ?: key=def() 自定义排序
        """
        列表名.sorted()
        特点：原列表内部元素不会发生改变。
     二维列表：
    	前一个括号指列数 后一个指行数
    	matrix = [[r * c for c in range(8)] for r in range(10)]
     列表运算：
    	# 列表+列表 = 两个列表的拼接
        # 列表*n = 生成新列表，原列表重复n次
        # 字符串*n  = 表示生成一个新字符串，原字符串重复n次
```

```python
**元组：
	# 特点：元组是只读的列表，因此会使列表发生改变的成员函数不适用于元组，如remove(),sort()等。
    表示：tuple() 或()
    
```

```python
	集合：
    特点：集合内不允许有重复的元素
    	 集合内的元素是无序的，不分前后顺序。
         集合内的元素必须是可哈希类型，这些元素的对象一般是只读的。
    创建：可用{}和set()函数来实现。创建空集合必须使用set()函数来完成。
```

2.与字符串常用的有关方法

```python
title() #将字符串的个首字母大写，非首字母小写，并返回。
upper() #将字符串的各个字母该为大写。
lower() #将字符串的各个字母改为小写。
rstrip()#将字符串右端的空格去掉。
lstrip()#将字符串左端的空格去掉。
strip() #将字符串的空格去掉。
find()  #输出字符串中含有参数字符或子串的第一个下标。
center()#返回字符串在指定宽度内居中摆放后的新字符串。
 	#例："string".center(width,"填充字符")
rfind() #寻找字符串中指定字串最后一次出现的下标。
join()  #将序列里的多个字符串中指定的间隔字符串拼接起来。
	#例：
    dirs = ["","home","pi"]
    print("/".join(dirs))
```

3.数值运算及其优先级

除：//

x**y : 表示求x的y次方，优先级高于乘除。

4.时间

```python
import time
totalSecond = time.time()	#获取当前总秒数
import datetime
curDate = datetime.datetime.now()
datetime模块datetime类型的now()函数返回当前系统时间给curDate,包含了年月日时分秒等属性
```

5.数值列表

```python
range() #函数用于创建一个整数列表
range(x,y) # [x,y)
k = range(x,y)
range(x,y,z) #z为相邻元素的间隔
```

6.序列缝合与循环解包

```python
 """
 zip()函数可以将任意序列缝合起来，并返回一个由元组构成的序列,当序列长度不一样长时，缝合完最短的序列即停止
 """
names = ['tim','andy','alex','dorothy']
salarys = [1200,1050,1600,2010]
zipped = zip(names,salarys) 	//缝合
for name,salary in zip(names,salarys):	//解包
    print(name,salary)
"""
enumerate()函数是一种特殊形式的缝合，他将序列元素与元素下标缝合成一个元组。
"""
```

##### 7.python支持多继承

```python
class object1(父类1，父类2) #优先级 左边>右边
"""
在子类的构造函数中执行父类的构造函数是必须的，否则子类对象将会缺失父类构造函数中的部分属性。
"""
私有方法：
	特点：1,在属性和方法名前加两个下划线 2，私有的外部无法访问,可以在公开的方法或接口中调用。
	def ——privateMethod()
```

##### 8.面向对象

*** function()函数中没有指定self参数，表示它不是实例化方法，而是所有对象共享的方法，也称为静态成员方法。 使用方式为：类名.function()

```python
类属性    类方法：所有成员所共享的，值不随实例化对象而改变。定义：不加self
实例化属性 实例化方法：实例化对象具有单独的内存地址，随实例化对象的改变而改变。定义：需加self
```

##### 9.字符串进阶

```python
format():
    "{score:.3f}".format(score) score:替代字段名
    f'{score:.3f}' 简写
    {i:.2f} :表示替代字段从format函数中第i个参数取值（从0始计，i为整数）
```

##### 10.文件读写

```python
open(file,mode) file:指文件路径可以是绝对路径或相对路径 mode:表明文件的工作模式
        "r" :读模式
        "w" :写模式
        "x" :独占写模式，不允许其他应用程序在该文件未关闭时使用该文件
        "a" :附加模式
        "b" :二进制模式
        "t" :文本模式
        "+" :读写模式，必须与r,w,a等配合使用
```

##### 11.自定义异常

```python
try except else finally
try:找出错误 except:捕获错误信息 else:执行无错误时语句 finally:必定执行语句
自定义：
class myexcept(Exception): #自定义异常基类，继承异常类超类
    pass
class specificError(myexcept):#具体异常
    def ——init——(self,参数)：
    def ——str——(self): #具体错误信息
        return str
def function():
    try:
        可能含有错误的语句
    except Exception as e:
        print(e) #打印错误信息
    else:
        无错误时执行正确语句
    finally:
        最终执行语句
```


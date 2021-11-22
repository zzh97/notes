### Python自学手册
Python是一种解释性的高级语言，这使得它的运行速度与加密都成为了劣势，相对的它有一个很棒的特点——语法精炼，同样的一个程序Python实现起来可能是100行，而别的语言有可能是1000行。

所以说，人生苦短，我选PY（双关语）

目前的Python，有两个版本，Python2与Python3，显而易见，我们选择的Python3（Python2已经不更新了）

关于Python的安装、创建、运行等，略
关于编译器的选择，我个人喜欢Visual Studio Code

好，我们现在正式开始进入Python语法的学习！
### 1.输入与输出
#### （1）输出
```
print ('hello world!') # 输出hello world！
```
python与JavaScript有些类似，Python语句再末尾也不需要加分号; 而且Python中的'单引号'与"双引号"都可以表示String类型（字符串）

但是，不同的是，在Python中用#号用于表示注释，这与JavaScript就不同了
```
print ('1+1=', 1+1) # 输出1+1= 2
```
Python中的print函数，可跟多个参数，逗号相当于一个空格，而且对表达式（1+1）Python会自动计算
#### （2）输入
```
name = input () # 将用户输入的值赋给name变量
```
Python中使用一个变量，无需事先声明，在第一次使用时，解释器会自动帮你声明

在运行了上述代码后，程序将会等待用户输入，当用户输入完成后（敲下回车），name变量就接受到了输入的值
```
Print (name) # 输出name里的值
```
此时，在执行Print (name)，就会输出用户输入的值

有人说，为什么不直接写name，答：那是在dos窗口（黑底白字）中才可以这么做，写一句，按一下回车，它解释一句；如果封装成一个.py文件，就必须用print

需要注意的是Python与C/C++、JavaScript等大多数语言一样，大小写敏感，与之例外的便是"天下第一"的PHP（斜眼笑
```
Name # 会报错：'Name' is not defined
```
所以，使用Name就会报错，因为Name ≠ name
#### （3）小例子
```
print ("What's your name?") # 你叫啥
name = input () # 用户输入 张三
print (name) # 输出 张三
```
需要注意的是，'What's your name?'这种写法会出错，因为解释器会把'what'看成一个String，那样的话s your name?'就少了一个单引号；这便是JavaScript与Python都采用单/双引号的原因

其次，还需要注意，在Python中用缩进（空格）的对齐与否，来表示'块'这个概念
```
print ("What's your name?")
    name = input () # 会报错：unexpected indent
print (name)
```
所以，这么写是错的
### 2.数据类型与运算符
#### （1）数据类型
Python与JavaScript一样是动态语言（运行时才检查类型），这表明它们在定义变量的时候，无需指定该变量的类型（不过，JavaScript还需要用var或者let关键字就是了）
```
# 整数
a = 1
# 浮点数
b = 1.2
# 布尔值
c = True
# 字符串
d = '静夜思'
# 多行字符串
f = '''窗前明月光,
疑是地上霜;
举头望明月,
低头思故乡.'''
print (a)
print (b)
print (c)
print (d)
print (f)
```
请注意，在Python中布尔值的首字母要大写（True与False），而在JavaScript中是小写的

还有，在Python中多行字符串是用'''来围起来的，而在JavaScript中是用`来围起来的
```
# python
a = '''我是猪
我舍友是狗
你连我和我舍友都不如'''
```
```
// JavaScript
a = `我是猪
我舍友是狗
你连我和我舍友都不如`
```
注：由于Python没有多行注释，所以常用多行字符串来替代
#### （2）运算符
```
# Python的算术运算符
print (1 + 1) # 加：2
print (3 - 1) # 减：2
print (2 * 3) # 乘：6
print (6 / 2) # 除：3.0（结果为浮点数）
print (8 % 3) # 取模：2
print (7 // 2) # 整除：3
print (2 ** 3) # 幂次：8
```
整除//与幂次**是Python独有的，JavaScript没有这些运算符，相对的，自增++与自减--这种C/C++、JavaScript等大多数语言都有的运算符，Python反而没有

在算术运算符后加等号=，就能变成赋值运算符，如：
```
# Python的赋值运算符（部分）
a = 1
print (a) # 1
a += 2
print (a) # 1 + 2 = 3
a **= 3
print (a) # 3 ** 3 = 27
```
关于Python的条件运算符（!=、>=等）、位运算符(~、&等)与C语言一致，别不做赘述
```
# Python的逻辑运算符
print (True and False) # False
print (True or False) # True
print (not False) # True
```
Python的逻辑运算符与C/C++、JavaScript不一致，不用&&、||和！，而是用更加语义化的and、or与not
#### （3）数组
在Pyhton中，没有数组这个概念，与之对应的，用list(列表)与tuple(元组)来代替，我们先来介绍list
```
students = ['Tom', 'Alice', 'Taylor']
print (students) # 全打印：['Tom', 'Alice', 'Taylor']
print (students[0]) # 第一个：Tom
print (students[-1]) # 倒数第一个：Taylor

students.append ('Bob') # 末尾添加一个
print (students) # 全打印：['Tom', 'Alice', 'Taylor', 'Bob']
students[0] = 'Aim' # 修改第一个
print (students) # 全打印：['Aim', 'Alice', 'Taylor', 'Bob']
students.insert (1, 'Jack') # 在第二个位置插入一个
print (students) # 全打印：['Aim', 'Jack','Alice', 'Taylor', 'Bob']
students.pop() # 弹出(删除)最后一个
print (students) # 全打印：['Aim', 'Jack','Alice', 'Taylor']
students.pop(0) # 弹出(删除)第一个
print (students) # 全打印：['Jack','Alice', 'Taylor']

print (len(students)) # list的长度：3
```
list与数组基本一致，但也有不同之处，比如list不要求元素类型相同，再比如list不需要这样students[]定义

需要注意的是，pop弹出是会自动打印的

对了，在C/C++中数组的元素是用花括号包起来的
```
int arr[3] = {1, 2, 3}
```
在JavaScript中是用方括号（与Python一致）
```
var arr[] = [1, 2, 3]
```
现在我们来看tuple
```
students = ('Tom', 'Alice', 'Taylor')
print (students) # 全打印：['Tom', 'Alice', 'Taylor']
print (students[0]) # 第一个：Tom
print (students[-1]) # 倒数第一个：Taylor
```
tuple中的元素是用圆括号包起来的，而且重要的是，tuple相当于常量，一旦定义后，便不可修改，不可添加。。
### 3.控制语句与键值对
#### （1）分支语句
```
print ("What's your score?")
# 由于input()返回的结果为String，所以用int()进行强制转换
score = int (input())
if score >= 90:
    print ('奖学金有望')
elif score >= 60:
    print ('不愧是我')
else:
    print ('等着补考吧你')
```
与C/C++、JavaScript不同的是，if后没有()，而是在末尾加上冒号:，也没有用{}来表示'块'，而是用缩进

注：Python没有switch语句，总所周知，if语句没有switch语句高效（相当于链表与数组在取第i个元素的区别）
#### （2）循环语句
以下是while循环的应用
```
i = 0
s = 0
while i < 100:
    i = i + 1
    s = s + i
print ('1+2+3+...+100 =', s) # 5050
```
break（终止）的使用
```
i = 0
s = 0
while i < 100:
    i = i + 1
    if i > 50:
        break
    s = s + i
print ('1+2+3+...+50=', s) # 1275
```
continue（跳过本次）的使用
```
i = 0
s = 0
while i < 100:
    i = i + 1
    if i == 50:
        continue
    s = s + i
print ('1+2+...+49+51+...+100=', s) # 5000
```
更常见的还是for循环
```
for i in [1,2,3,4]:
    print (i)
'''
这是输出结果：
1
2
3
4
'''
```
fot..in语句用于遍历数组，与C、JavaScript里的for不同，所以如果需要计算1+2+...+100的值，就需要定义一个[1,2,...,100]这样1~100的数组

好在，Python有一个range函数，可以用来快速创建一个整数数组，哦不准确地说是整数列表（Python里叫列表，列表内元素无需同种类型）
```
a = range (5, 10 , 2)
print (a) # 输出range(5, 10 , 2)这个对象
```
不过，上述的是Python2中是说法了，在Python3中，range函数返回的是一个Object，如果你想要看清楚它的内容，可以把它转为一个list
```
a = list (range(5, 10 , 2))
print (a) # 输出从5~50的奇数[5,7,9]
```
现在，我们把range函数用到for..in语句中，实现1+2+...100这个功能
```
s = 0
for i in range(100):
    i = i + 1
    s = s + i
print ('1+2+3+...+100 =', s) # 5050
```
#### （3）键值对
什么是键值对呢？

就是由key（键）到value（值）的映射所形成的集合，举个例子，数组就是一种键值对，数组下标是key，下标对应的数组元素是value

而Python里的键值对，被称为dict（字典），相当于JavaScript里的JSON
```
ASCII = {'A': 65, 'B': 66, 'C': 67}
print (ASCII['A']) # 查找'A'所对应的值
```
我稍微提一句，JSON的本质是一种数据格式，只不过JSON的语法刚好符合JavaScript中Object的语法，所以JavaScript中的JSON可以如果Python中的dict一样，key使用单引号，甚至key不为String

但是别忘了，JSON的本质是一种数据结构，也就是说对于其
他语句，如Python而言，JSON只是一个String，所以必须用双引号来做key

上述的这个两段话，对于Python基础的学习，没有什么影响，所以也可以暂时不去管JSON是个啥，我们搞清楚dict是啥就好了，在Python中dict是一种数据类型，它与list、tuple这些一样

需要注意的是，dict里的key可以是任何常量，如String、数字、tuple里的元素等，但不能是list里的元素，因为它可变

现在，我们来看set（集合），只有key没有value的一种数据类型，并且要求不重复，因为key不能重复
```
a = [1, 1, 2, 3]
b = set (a)
print (b) # 输出{1, 2, 3}
```
set与tuple一样是不可修改的，不过set不可修改是因为set里存的都是key，key是不可修改的

但不同于tuple，set是可以添加与删除
```
a = [ 1, 2, 3]
b = set (a)
b.add (4)
b.remove (1)
print (b) # 输出{2, 3, 4}
```
### 4.函数与语法糖
#### （1）定义函数
```
def add (a, b):
    return a + b
print (add(1, 2)) # 输出3
```
与C/C++、JavaScript不同，Python用def来定义函数

有时，我们可能会需要一个什么都不做的函数，称其为空函数
```
# 定义一个空函数
def nop():
        pass
```
Python与JavaScript一样可以为参数提供默认值，而且方法都是用等号
```
def add (a, b = 1):
    return a + b
print (add(1)) # 输出2
```
需要注意的是，这种默认参数，用的是同一指针，即一个默认参数有一个指针，并不会因为函数调用次数而改变

所以要避免以下这种情况
```
def add (a = []):
    a.append('A')
    return a
print (add()) # 输出['A']
print (add()) # 输出['A', 'A']
```
在大多数编程语言中，如果想返回多个值，一般用一个数组来存放这些值，然后返回这个数组，但是在Python中，可以简写（本质上返回的是一个tuple）：
```
def add_or_times (a, b):
    return a+b, a*b
print (add_or_times(2, 3)) # 返回的是(5, 6)
```
并且Python和JavaScript一样可以动态接受多个参数，只不过JavaScript用的是arguments，而Python用的：
```
def sum (*numbers):
    s = 0
    for i in numbers:
        s = s + i
    return s
print (sum(1,2,3)) # 输出1+2+3的值，也就是6
```
本质也是一种简写，实则numbers这参数是一个tuple，只不过与多个返回值不同的是，这种简写有一个前提，需要在参数名前加*星号，以表示使用简写（类似于C语言中的星号，取值，这样就没有括号了）
#### （2）四大特性
##### 重载

所谓重载，就是指同一函数根据不同参数（个数/类型），执行不同语句

Python是不支持重载的，所以要实现重载功能，就只能借助它法，如使用动态参数
```
def fun (*numbers):
    if len(numbers) == 0:
        print ('没有参数')
    elif len(numbers) == 1:
        if type(numbers[0]) == int:
            print ('只有一个参数，且类型为int')
        else:
            print ('只有一个参数，且类型不为int')
    else:
        print ('有两个以上的参数')  
fun(1) # 输出：只有一个参数，且类型为int
```
再如使用默认参数
```
def fun (a=-1, b=-1):
    if a == -1:
        print ('没有参数')
    elif b == -1:
        if type(a) == int:
            print ('只有一个参数，且类型为int')
        else:
            print ('只有一个参数，且类型不为int')
    else:
        print ('有两个参数')  
fun(1) # 输出：只有一个参数，且类型为int
```
##### 递归

所谓递归，就是指函数自己调用自己，从而实现循环，在递归中最重要的是停止条件，如果没有停止条件，就会陷入死循环，哦对了，递归算法不利于空间复杂度
```
def fac (n):
    # 停止条件
    if n <=1:
        return 1
    # 基本语句
    return n * fac(n-1)
print (fac (5)) # 输出5的阶乘，也就是120
```
##### 回调

所谓回调，是指以函数为参数，当条件成立是执行该参数

```
def fun (a, callback):
    if a == 1:
        callback ()
def call ():
    print ('这是回调函数')
fun (1, call) # 输出：这是回调函数
```
不过更多的时候，为了提高内聚，会使用匿名函数，因为匿名函数可以作为参数
```
def fun (a, callback):
    if a == 1:
        callback ()
# lambda是匿名函数
fun (1, lambda:
    print ('这是回调函数')
) # 输出：这是回调函数
```
##### 闭包

在函数作用域下，函数内的定义变量，函数外不能使用
```
def fun ():
    a = 1
print (a) # 报错：name 'a' is not defined
```
如果我们想要使用a这个局部变量就需要，return出来
```
def fun ():
    a = 1
    return a
print (fun ()) # 输出：1
```
但这得到的，其实是a的值，而非a这个变量（谁叫我们没有指针呢）

这样的话，当fun函数调用完后，变量a就会被'垃圾回收机制'给回收了

我们想要延迟a的生命周期，就必须在fun函数结束后，还能使用变量a

于是，闭包出现了
```
def fun1 ():
    # 隶属于fun1的局部变量
    a = 1
    def fun2 ():
        # fun2使用父级fun1的局部变量
        print (a)
    return fun2
# 获取fun2这个函数
fun = fun1()
# 调用fun2（此时，fun1已经结束，但因为a被fun使用，故a的生命周期得到延迟）
fun ()
```
所谓闭包，就是一个包含环境的函数，这里的环境通常指的是其他函数的局部变量

所以说，闭包是一个函数，它的作用是使用和延长某些局部变量，比如：在调用fun2()时，使用了属于fun1()的局部变量a，相当于fun1把a借给了fun2
#### （3）语法糖
上文中的匿名函数和闭包其实都属于语法糖

所谓语法糖，就是一些语言制造者为了方便程序员编程而设计的一些小技巧

切片
```
a = [1,2,3,4,5]
print (a[2:4]) # 第2个到第4个（不包含第2个）：[3, 4]
print (a[-3:-1]) # 倒数第3个到倒数第1个（不包含倒1个）：[3, 4]
print (a[0:4]) # 第1个到第4个：[1, 2, 3, 4]
print (a[:]) # 全部：[1, 2, 3, 4, 5]
```
迭代与迭代器
```
A = [1,2,3,4,5]
# 变量A中的元素
for a in A:
    # 不换行打印
    print (a, end='') # 输出：12345
```
这种遍历数组中的元素，便叫迭代
```
# 导入Iterable模块
from collections.abc import Iterable
# 定义一个list
a = [1,2,3]
# 判断是否是Iterable对象
yes_or_no = isinstance(a, Iterable)
print (yes_or_no) # 输出：True
# 把list转换为Iterator（迭代器）
b = iter(a)
print (next (b)) # 输出：1
print (next (b)) # 输出：2
```
而迭代器是一个可迭代的对象，list、tuple、dict、String都是可迭代的，但是只有迭代器可以使用next函数

生成与生成器
```
a = list (range (1, 10)) # 生成一个1到9的list
print (a) # [1, 2, 3, 4, 5, 6, 7, 8, 9]

b = [x for x in range (1, 10)] # 用生成器来生成
print (b) # [1, 2, 3, 4, 5, 6, 7, 8, 9]

c = [x * x for x in range (2, 6)] # 由2到5的平方数组成的list
print (c) # [4, 9, 16, 25]
```
a就是生成，也叫列表生成式，它是用range来生成的，这样有一个缺点，就是不灵活，比如我只想要其中的偶数，所以就出现了一个东西叫生成器，b和c都是生成器的例子，在c中我们的生成规则就是x * x
### 5.函数式编程
所谓函数式编程是面向过程编程的一种，顾名思义就是用函数来作为程序的主体，而不使用变量，所以没有全局变量，最外层只能是函数；这就使得在函数式编程中，如果函数的输入的确定的，那它的输出就也是确定的（没有全局变量的干扰）

想要实现函数式编程，就要求函数与变量有同等地位，可以像变量一样，作为其他函数的参数与返回值，也要求函数可以接受其他函数当参数

前者被称为头等函数（能当参数与返回值），后者被称为高阶函数（能收函数当参数）

我有一个好消息和一个坏消息，你想听哪个？

好消息：Python支持头等函数和高阶函数，所以Python可以进行函数式编程
坏消息：Python里有变量，所以它的函数式编程不纯粹，如果你想体验纯粹的函数式编程，请选择lisp类的编程语言
#### （1）高阶函数
来介绍一些已经写好的，常用的高阶函数吧

map（映射）
```
def f(x):
    return x + 1
# map的第一个参数是函数，第二个要求可迭代
a = map (f, [1,2,3])
# map返回的是迭代器，不能直接打印
print (list(a)) # 输出：[2, 3, 4]
```
map函数的出现让Python更适合科学计算，它的语义更贴近数学，[1,2,3]在规则f下映射成a，如同:
$$ y = f(x) $$

对了，JavaScript在ES6后，也有map函数呦！

reduce（累加器）
```
# 导入reduce
from functools import reduce
def f(x, y):
    return x + y
a = reduce (f, [1,3,5])
print (a) # 输出：9
'''
其工作原理是：
x = 1, y = 3, x+y = 4
x = 4, y = 5, x+y = 9
'''

def f2(x, y):
    return x*10 + y
b = reduce (f2, [1,3,5])
print (b) # 输出：135
'''
其工作原理是：
x = 1, y = 3, x*10+y = 13
x = 13, y = 5, x*10+y = 135
'''
```
发现没，reduce并不是单纯地用来做累加的，它是一种降维映射，把数组映射成了数，或者说是把向量映射成了一个数（这样显得专业一点）

如果说map是对集合中的元素进行批量修改，那么reduce就是把集合根据某种规则两两合并成最终变成一个元素

对了，JavaScript也有reduce哦，别学混了

Python中还有一个常见的高阶函数，那就是sorted
```
a = [5,3,1,2,4]
# 排序（升序）
b = sorted (a)
print (b) # 输出[1, 2, 3, 4, 5]
# 排序（降序）
c = sorted (a, reverse=True)
print (c) # 输出[5, 4, 3, 2, 1]
# 排序（按平方来）
d = sorted (a, key = lambda x: x * x)
print (d) # 输出[1, 2, 3, 4, 5]
```
需要注意的是，按平方来，指的是按平方后的大小来排序，但是不改变元素的值

这里我们用到了匿名函数lambda，匿名函数在只有一个表达式的时候，不用写return，要记住它的写法哦，匿名函数在函数式编程里是经常用到的
#### （2）装饰器与偏函数
先来介绍装饰器
```
def fun1 ():
    # 环境
    a = 1
    # 函数
    def fun2 ():
        print (a)
    return fun2
# 这是一个闭包（有环境的函数）
fun = fun1 ()
fun () # 输出 a
```
这是我们之前学过的闭包，装饰器其实就是一种闭包

假设我们现在有一个需求：在不改变fun2的情况下，在fun2前执行fun1
```
def fun2 ():
    print ('这是第二句')

def fun1 ():
    print ('这是第一句')
    fun2 ()

fun1 () # 输出：这是第一句 \n 这是第二句
```
上述做法，便是运用函数的二次封装，函数里套函数

不过为了灵活，不单单只装饰fun2这个函数，于是改成如下代码
```
def fun2 ():
    print ('这是第二句')

def fun1 (fun):
    print ('这是第一句')
    fun ()

fun1 (fun2) # 输出：这是第一句 \n 这是第二句
```
最后将其改成闭包形式（能返回一个带环境函数），不过这个例子中的环境为空就是了
```
# 被装饰的函数
def fun2 ():
    print ('这是第二句')
# 装饰器（返回装饰好的函数）
def fun1 (fun):
    # 要返回的函数
    def temp():
        print ('这是第一句')
        fun ()
    return temp

f = fun1 (fun2)
f () # 输出：这是第一句 \n 这是第二句
```
这便是装饰器，它长的和闭包一样，区别在与侧重点不同，闭包的作用是跨函数使用变量并延长其生命周期，而装饰器的作用是在不过修改某个函数的情况下对其进行修改

现在介绍偏函数
```
# 把1000转换为二进制
print (int ('1000', base = 2)) # 输出：8
```
我希望默认就是二进制，不用写base = 2
```
# 默认二进制
def int2 (o, base = 2):
    return int (o, base)

print (int2 ('1000'))
```
用偏函数来实现
```
import functools
# 使用偏函数来修改参数默认值
int2 = functools.partial(int, base=2)

print (int2 ('1000')) # 输出：8
```
#### （3）面向过程与函数式
面向过程编程是我们最早接触的一种程序设计方法，比如大一学的C语言，而函数式编程则是面向过程中的一种，函数式对于面向过程而言，可以说是男人与人的关系

我们先来看面向过程：

假设有这么一个需求，我要制作一个计算器，目前先暂定它能做加法运算

现在思考这个需求要怎么实现：首先，需要操作数a和b，然后把它俩加起来，最后输出给用户，OK来看代码
```
print ('请输入操作数a的值：', end = '')
a = int (input ())
print ('请输入操作数b的值：', end = '')
b = int (input ())
print (a, '+', b, '=', a + b)
```
这样的一种依照时间的线性思考过程，便是面向过程编程，先怎么怎么样，再怎么怎么样

现在已经实现了这个需求，为了能够不断地复用，我们把它封装成一个函数
```
def add ():
    print ('请输入操作数a的值：', end = '')
    a = int (input ())
    print ('请输入操作数b的值：', end = '')
    b = int (input ())
    print (a, '+', b, '=', a + b)

add ()
```
这边是函数式编程（勉强来说），最外层只有函数，所有的数据都在函数内部或者函数之间交互，我们想要实现什么功能就使用什么函数

我们把需求扩展一下，不仅要实现加法，还要乘法
```
def add ():
    print ('请输入操作数a的值：', end = '')
    a = int (input ())
    print ('请输入操作数b的值：', end = '')
    b = int (input ())
    print (a, '+', b, '=', a + b)

def times ():
    print ('请输入操作数a的值：', end = '')
    a = int (input ())
    print ('请输入操作数b的值：', end = '')
    b = int (input ())
    print (a, 'x', b, '=', a * b)

def computer ():
    print ('请选择运算规则（加法/乘法）')
    print ('选择加法输入1，乘法输入2：', end = '')
    f = int (input ())
    if f == 1:
        add ()
    elif f == 2:
        times ()
    else:
        print ('选择加法输入1，乘法输入2')
        print ('请选择运算规则（加法/乘法）：')

computer ()
```
虽然还符合函数式编程的定义，但是不是发现了有很多重复的地方，我们把每一个功能都封装成了一个函数，确实满足了低耦合，但不符合高内聚

```
def computing (f):
    print ('请输入操作数a的值：', end = '')
    a = int (input ())
    print ('请输入操作数b的值：', end = '')
    b = int (input ())
    if f == 1:
        print (a, '+', b, '=', a + b)
    elif f == 2:
        print (a, 'x', b, '=', a * b)
    else:
        print ('选择加法输入1，乘法输入2')
        print ('请选择运算规则（加法/乘法）：')

def computer ():
    print ('请选择运算规则（加法/乘法）')
    print ('选择加法输入1，乘法输入2：', end = '')
    f = int (input ())
    computing (f)

computer ()
```

```

```

但是，有时需要全局变量，最外层并非只有函数，这时要么把全局变量改为局部变量，通过闭包或指针等方式，要么就只能不使用函数式编程了

总所周知，全局变量不是个好东西，因为它大大地占用命名空间，所以我们希望减少全局变量的存在，如果不使用函数式编程的话，还有一种选择，那就是面向对象


### 6.面向对象编程
如果说函数是对语句的封装，那么对象就是对函数的封装，这样能使代码更加符合高内聚低耦合的原则

面向对象编程（OOP），就是以对象为程序的主体，最外层只有对象，而变量与函数都放到对象里面，这被称为OOP的'封装'特性

除此之外OOP还有两个特性就是多态与继承，这使得代码具有更强的扩展性，代码更加简洁，相似的代码不需要重复地写
#### （1）封装
封装
```
# 定义学生类
class Student:
    name = 'Tom'
    def say (self, words):
        print (self.name, ':', words)
# 实例化一个学生对象
a = Student ()
# 调用对象里的say方法（函数）
a.say ('Hello world!') # 输出：Tom : Hello world!
# 修改对象里的name属性（变量）
a.name = 'Alice'
a.say ('Hi, guys.') # 输出：Alice : Hi, guys.
```
再来看看构造方法与私有属性
```
# 定义学生类
class Student:
    name = 'Tom'
    # 私有属性
    __age = 20
    # 构造方法
    def __init__ (self, n):
        self.name = n
    def say (self, words):
        print (self.name,self.__age,'岁', ':', words)
# 实例化一个学生对象
a = Student ('Tom')
# 修改age属性（修改失败）
a.__age = 18
# 调用对象里的say方法（函数）
a.say ('Hello world!') # 输出：Tom 20 岁 : Hello world!
# 修改对象里的name属性（变量）
a.name = 'Alice'
a.say ('Hi, guys.') # 输出：Alice 20 岁 : Hi, guys.

```
#### （2）继承
```
# 定义人类
class Person:
    name = '人名'
    def __init__ (self, name):
        self.name = name
    def who (self):
        print (self.name)

# 实例化人对象
Tom = Person ('Tom')
Tom.who () # 输出：Tom

# 定义学生类（括号里是父类）
class Student (Person):
    def __init__ (self, name):
        # 调用父类的构造函数
        Person.__init__ (self, name)
    def say (self, words):
        # self.name的name其实是Person里的name借给了Student用
        print (self.name, ':', words)

# 实例化学生对象
Alice = Student ('Alice')
Alice.say ('Get out!') # 输出：Alice : Get out!
```
#### （3）多态
### 7.模块化管理与错误调试
#### （1）自定义模块
介绍
所谓模块，其实就是一个.py的文件，是一种更高一级的封装，对文件的封装

那为什么需要模块了，函数做了一层封装，对象又做了一层封装，模块还来。。

主要原因有两个，①为了是文件中的代码减少，②规范命名空间（避免命名冲突）

封装
```
# a.py
a = 1
def f():
    print ('这是a文件')
```
导入模块a
```
# b.py
import a
print (a.a) # 输出：1
a.f() # 输出： 这是a文件里的函数
```
另外一种导入方法
```
# b.py
from a import f
f() # 输出： 这是a文件里的函数
```
__name__的用法
```
# a.py
print ('这里是a.py')
# __name__是文件名属性
if __name__ == '__main__':
    print ('a.py是一个程序')
else:
    def f():
        print ('a.py是一个模块')
```
```
# b.py
import a # 输出：这里是a.py
a.f() # 输出：a.py是一个模块
```

#### （2）其他模块与包
使用系统模块
```
import sys
```
安装第三方模块
```
pip install 模块名
```
包（解决模块同名）
```
# 导入a文件夹里的b.py
import a.b
# 调用b.py里的f函数
a.b.f()
```
#### （3）错误调试
调试常见的方法有两种，①把可以出错的语句注释起来，②打印某个时刻某个变量

可喜的是，在Python中，我们有更优异的解决方案，针对①可以使用try语句，针对②可以使用assert语句
```
try:
    print (1 / 0)
except:
    print ('出错了')
else:
    print ('代码正常')
```
把可能出错的语句，放到try里面，若真出错了，就会执行except里的语句，反之执行else里的语句并继续执行后续代码

assert断言，顾名思义就是对某个条件打包票
```
a = 2
# 我断定a一定等于1，否则就不运行了并抛出错误
assert a == 1, '出错了：a不等于1'
print (a) # 出错后，这句就不执行了
```
### 8.文件I/O与GUI

### 9.进程线程与异步

### 11.TCP与UDP
### 12.Web框架
### 13.数据库操作
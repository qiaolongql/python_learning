# python_learning

0、杂项

    缩进使用4个空格不要使用制表符
    每行行宽不要超过80个字符
    在比较运算符的两边各加一个空格
    函数名小写，且只使用字母数字下划线，函数之间两个空行 
    类的首字母大写,采用驼峰命名法
    __xxx/_xxx命名 一般是private函数或变量,但__xxx一般是通过_类名__xxx来访问的
    __xxx__命名 一般有特殊用途(特殊变量,自己一般不要用)
    模块中__name__是一个特殊的全局变量，当直接执行是__name__=__main__,
        当从别的地方调用此模块时__name__就是模块名
    __doc__全局变量可以调用模块定义的文档注释
        *任何模块代码的第一个字符串都被视为模块的文档注释 

    输入
        使用input(提示字符)来获取用户输入，并将其赋值给一个变量来保存
    输出
        r"" 可使引号内的字符不转意按原样输出
        '''...''' 用此格式可以写成多行 
    
    python中空值定义为None，真值True，假值False(首字母都大写)
    
    python是动态语言不用声明变量类型，java等是静态语言必须为变量声明类型
    None是数据类型NoneType的唯一值，可用于不需要返回值的函数的return语句，如print函数
```python
spam = print("hello")    //打印hello ==> hello
print(spam)              //打印spam  ==> None
```

    递归层数较多时会出现栈溢出stackoverflow，可通过for循环替代实现

    type(x)返回对象的类型(直接类型)，不适用于父继承链比较    
    判断一个对象是否为某类型，或在该类型的父继承链上，可以用isinstance(对象,类型)
        如:isinstance((x for x in range(10)),Iterator)    返回True
           isinstance((x for x in range(10)),Iterable)    返回False

    对于多项赋值：如a,b=b,a+b这种
        其右边相当于元组(b,a+b),在赋值前右边所有的值都已经确定
        
    lambda x: x == 5 相当于函数
        def fun(x):
          return x == 5
    filter(函数,list) filter将作为参数的函数作用于list的每一个元素，
        若函数返回值为True,则筛选出该元素,最后返回一个包含筛选元素的新列表
    

0.1、编码

    ASCII码 1字节(Byte)包括英文字母、数字、符号
    Unicode 支持所有语言类型，一般大于等于两个字节，用两个字节表示一个字符(不同语言占空间不同)
    UTF-8   可变长编码，把一个unicode编码成1-6个字节 英文1个字节 汉字3个字节 特殊6个字节
    
    计算机中存储的编码格式为Unicode类型，python中字符串也是Unicode编码
    如:编辑记事本文件时将utf-8转换为unicode加载到内存，编辑完成后再转换为utf-8存储到记事本文件中

    ord() 返回字符的数字表示形式
    chr() 把数字形式转换为字符表示 如:A->65 中->20013

    磁盘存储、网络传输的是bytes,需要将unicode转换为bytes
        字符串.encode("ascii/utf-8")  #英文用ascii  中文用uhf-8
    从磁盘、网络上读取的是bytes流，转换成字符串需要用
        字节流.decode("utf-8")
 

1、字符串

    .lower() 小写
    .upper() 大写
    .title() 单词首字母大写
    .lstrip() 剔除左边空白
    .rstrip() 剔除右边空白
    .strip() 剔除两边空白

    .format(参数1,参数2...)  用传入的参数替换字符串中的占位符{0},{1}等  #用于print是的字符串格式化

2、数字

    应显式的用str()将数字转换为字符串再使用，用int()/float()将字符数值转换成数字后使用
    在python2中3/2=1会舍弃小数部分，若想正确输出小数需将其中之一置为浮点数
    在python3中/的结果永远是浮点数，//(地板除)的结果永远是整数
    python中没有常量，一般用全大写变量表示常量，但其值实际是可以修改的
    整数和浮点数(存储长度)没有大小限制，浮点数超出一定范围表示为无限大inf
    bin(5) 返回数字的二进制表示(字符串) 0b110
        oct() 八进制  hex() 十六进制
    int("110",2)的第二个参数表示要转换数的进制
        上面返回数字5 如果没有第二个参数返回数字110
    与或(^) 相同返回0 不同返回1 (一个数与全1与或等于对其每一位取反)

3、列表 []

    格式:  列表=[元素,元素,...]  liebiao=[]
    给列表指定一个复数名称
    列表以[]表示，元素用逗号分割
    列表第一个元素索引为0,最后一个元素索引为-1
    先判断列表是否为空后再访问元素
    列表的赋值会使变量关联到同一个列表(作为函数参数传递是也是如此)，如list2=list则list和list2指向同一个列表

    .append() 在末尾添加元素
    .insert(位置,元素值) 在定义位置添加元素(不是前面也不是后边，是定义位置)
    del 列表[x] 删除列表索引为x的元素    
    .pop() 弹出并返回最后一个元素
    .pop(x) 弹出并返回列表索引x位置的元素
    .remove(元素值) 从列表中删除找到的第一个匹配元素值

    .sort() 按字母顺序排序列表(本体)参数reverse=true为相反顺序
    sorted(列表) 返回排序后列表而不改变原列表
    .reverse() 反转列表(本体)
    len(列表) 返回列表大小 

    list(序列) 将一个序列创建为列表
    set(序列) 将一个序列创建为元素唯一的列表，也叫集合(元素不重复的列表)

    向列表中添加列表元素时候需要特别注意，如x.append(y),y是列表，此时x[-1]和y同时指向这个元素列表
        所以当y未被新地址赋值之前改变y中元素的值会同时改变x[-1]中的值，应特别注意

4、循环

    for x in 列表:
      代码体(循环代码体必须缩进)

    遍历列表中的每个元素并将其赋值给x
    python中用缩进来表示其他语言中的{}

    while 条件:
        循环体

5、条件判断

    关键字in和not in用于判断一个元素是否在一个列表中
    格式：  if 判断条件：
                执行语句
            elif 判断条件：
                执行语句
            else：
                执行语句
    因为else条件包含的范围太广，一般会用相应的elif语句代替以显示声明条件

6、创建数字列表

    range(start,end,step) 以步step创建一系列数字(不包括end)
      用for x in range(s,e):来遍历生成的数字
      或者用list(range(s,e))来生成列表
    min(列表) 数字列表最小值
    max(列表) 数字了表最大值
    sum(列表) 数字列表所有元素和

    列表解析： 列表名=[value**2 for value in range(1,11)]      #也叫列表生成式
        遍历数字系列并将value的平方作为列表的元素
        相当于： nums=[]
                 for value in range(1,11):
                   nums.append(value**2)
                 列表名=nums
        **注意:列表解析创建了一个新的列表，并把列表赋值为新变量即列表名

    列表[start:end] 返回一个列表的切片(不包括end)，start默认第一个元素，end默认包括最后一个元素
    列表[:] 复制列表(因为不写start和end默认为从头到尾)

7、元组（元素不能改变的列表）()

    定义： 元组名=(元素，元素...)    yuanzu=(200,10)
    元组同列表一样，不过元组内的元素不能改变
    若想改变元组内的元素值，需要重新给元组变量赋值一次
    为了消除歧义(与运算符中的括号区分)，定义只有一个元素的元组时需要加上一个逗号，如yuanzu=(200,)

8、字典（元素是键值对的列表）{}

    格式： 字典={键:值,键:值,...}   zidian={}
            from collection import OrderedDict加载有序字典类
            然后通过zidian=OrderedDict()创建有序字典(根据添加顺序)
    访问：zidian[键]  
    添加或修改：zidian[键]=值
    删除： del zidian[键]  或者 zidian.pop(key)

    .items()  返回字典中所有键值对
    .keys()  返回字典中所有键
    .values()  返回字典中所有值
    遍历键值对： for key,value in zidian.items():   #遍历键值对并将他们分别赋值给key 和 value俩个变量，从而遍历键值对
    通过key来查找value的算法叫hash算法，作为key的对象必须是不可变的如字符串、数字等

9、函数

    格式：    def 函数名(参数列表):
                  函数体...
    形参：函数定义时括号中定义的参数
    实参：函数调用时实际传递的变量

    参数列表中可以为参数提供默认值，如（参数1,参数2...，参数n=值）
    形参默认值可以被当作可选参数
    关键字实参：是在调用时传递的名称-值对,此时可以不安参数列表顺序传递参数，如 fun(参数2=值，参数1=值)
    命名关键字参数：同关键字参数，要求必须传递参数名，参数列表中位于*,/*参数,后边的参数是命名关键字参数
    任意数量参数：*参数名 可以接受任意多个参数的传递(实参值)，它被定义为一个元组
                  **参数名 可以接受任意多个关键字实参(键值对),它是一个dict字典
    有默认值的参数(或可选参数)、任意数量参数必须放在参数列表的最后，来保证前面的参数优先匹配

    导入模块：    import 模块名 as 别名    #使用 模块名/别名.hanshu() 来调用模块内的函数
    导入模块内函数：    from 模块名 import 函数名 as 别名    #直接使用 hanshu() 或 别名() 调用函数
    导入模块内所有函数:   from 模块名 import *
    #尽量只导入用到的函数，或者导入整个模块用.操作函数
    
    关于函数参数:
        所有传入函数的参数都是响应对象的引用,传入函数后函数会创建一个此引用的副本在函数中使用.
        对于不可变类型如numbers、strings、tuples，一旦对象被创建，其内容就不可以在改变，当
            我们用=再为其赋值时，其实是创建了一个新对象，并改变了原来变量的引用.所以如果将不
            可变类型的当做参数传入函数，若在函数中改变其值，则函数变量将指向新的引用而与原引用无关
        对于可变类型如list、dict、set等可修改对象,传入引用后若在函数中修改引用的内容，则会反映到
            原引用指向的对象中
    
10、函数进阶

    在python中一切都是对象，函数也不例外，所有函数都是一个function类的实例
    函数是一等对象: 
        ·运行时创建
        ·能赋值给变量或列表中的元素(f=foo 和 f=foo()不同，前者是赋值后者是执行并返回结果)
        ·能作为参数传递给函数
        ·能够作为函数的返回结果
    高阶函数：
        接受函数作为参数 或 把函数作为结果返回的
        map/filter/reduce是常见的高阶函数
    map/filter/reduce的现代替代
        list(map(fact,filter(lamda x: x%2,range(6))))等价于列表推导
        [fact(x) for x in range(6) if x%2]
        reduce(add,range(6))函数用于叠加数值，取代函数为sum(range(6))
    内置函数all(),any()
        all(iterable) 可迭代对象的每个元素都为真值是返回True
        any(iterable) 可迭代对象中有元素为真时就返回True
    匿名函数/lambda表达式
        将函数当做函数参数传递是匿名函数的通常使用场景
        lambda表达式语句只能使用纯表达式
        如lambda x: x[::-1]  接受参数x，返回x的反转
        
    可调用对象(方法指类中的函数)
        调用运算符()可以作用的对象就是可调用对象,python中有以下7种:
            ·自定义函数
            ·内置函数 (如len())
            ·内置方法 (内置对象中的方法如dict.get)
            ·方法 (用户自定义类中的方法)
            ·类 (调用类实际就是调用__new__方法创建实例,然后调用__init__方法初始化)
            ·类的实例 (如果类定义了__call__方法,那么它的实例可以当做方法调用)
            ·生成器函数 (使用yield关键字的函数和方法,返回生成器)
        使用内置方法 callable(名字) 来判断对象是否可调用

11、迭代 生成器 迭代器

    可迭代对象：可以用for循环来遍历的，或可以用in/not in 关键自的都是可迭代的
        list、tuple、dict、set、str等都是可迭代对象

    生成器:一边循环一边计算，不用一次生成所有元素，generator也是可迭代的
        *如果元素可通过某种算法推算，我们可以使用生成器，而不用一次存储所有元素
        *生成器存储的是算法，通过next(生成器对象)来访问计算下一个元素
        *生成器创建：
            <1>同列表解析模式:(value**2 for value in range(1,10))  #()取代[]
               它返回一个generator,是指向第一个元素的地址，可用next(g)取得计算
               下一个元素
            <2>yield模式:如果一个函数包含yield关键字，那么这个函数就是一个生成器
               如：def fib(max):              #斐波拉契数列
                       n, a, b = 0, 0, 1
                       while n < max:
                           yield b
                           a, b = b, a + b
                           n = n + 1
                       return 'done'
                   函数fib是一个生成器，f=fib(6),print(f)时候会打印f的地址，此时函数不会被执行
                   f中的元素只能通过next或通过for循环迭代计算出来
                   当用next或for迭代时函数开始执行，并在遇到yield时返回(这里相当于返回b),下次执行next
                   或者下次迭代时从yield返回处继续开始执行，再次遇到yield时返回
                   当使用next是最后会返回StopIterator异常，可通过StopIterator.value获得return中的值
                   用for循环迭代不会出现此异常，从而不能得到return返回值
   
    迭代器：Iterator表示一个数据流，其中的元素未知，只能通过被next()函数不断调用来返回下一个元素，它可以是无限大
        *区分Iterable(可迭代)和Iterator(迭代器)
            Iterable:意思是可迭代的，凡是可以用for迭代/in/not in访问的都是可迭代的对象(list/dict/tuple/set/str)
            Iterator:迭代器，只有可通过next()函数调用的才是迭代器(generator:元素未知，长度未知)
            Iterable通过iter()函数可以转化为Iterator
        迭代器一定可迭代，可迭代的不一定是迭代器;生成器是迭代器，可迭代对象不一定是迭代器;
            范围：生成器(generator)>迭代器(Iterator)>可迭代对象(Iterable)                


12、类

    格式：  class Man(object):                       #定义类,首字母必须大写python3中默认继承object
                count=0                             #类属性，为类所有，在内存中只创建一次，所有实例都可访问
                def __init__(self,name,age...):     #此方法为必须,调用Man()会先调用__new__()创建实例,然后调用__init__()初始化实例
                    self.name=name                  #self必须且放在第一个,它是创建实例的引用,在创建实例时自动赋值
                    self.age=age                    #从而让实例可以引用类的属性和方法,这里定义的属性为name和age,赋值语句
                    self.hair="black"               #是为实例的属性赋值，如my_man=Man("qiao",18)时执行了__init__(my_man,"qiao",age)
                    Man.count+=1                    #每次创建实例都会执行__init__，这条语句统计创建的实例个数
                                                    #对于没有在参数中列出的属性，则必须在函数内部显式的赋默认值 
                                                    #创建实例时参数必须于__init__中的参数匹配，否则会报错
                def run(self):                      #方法中传入self参数才能通过self.访问实例中的其他属性和方法
                    函数体

    子类：  class Child(Man):                       #括号中填写父类,表示继承哪里,子类定义必须位于其继承的父类之后,默认继承object
                def __init__(self,属性列表...):
                    super().__init__(父类属性列表)  #调用父类构造函数初始化继承属性
                    赋值自定义属性                  #为自定义属性赋值


                def run(self):                      #与父类同名的方法会被复写
                    函数体

                def yeld(self):                     #定义的自有方法
                    函数体

    实例属性:self.属性名,是实例的一部分，跟随实例一同创建。或实例创建后用 man.high=180 来创建
    类属性：直接定义属性名，为类所有，在内存中只创建一次，所有实例均可以访问
    
    在类中用__xxx的变量名表示private属性，在外部一般解释器会将其解析为 _类名__xxx 作为属性名，也就是也是可以访问的
        但一般建议对这种默认为private不要在外部访问，应该添加getter和setter方法作为对外访问的接口
    
    用dir("类名")可以返回一个包含字符串的list，它包含了类的所有属性和方法
    
    通过在子类中定义相同的方法来override父类中的方法
      若在override之后想在子类中使用父类的方法可以通过如下格式通过super方法访问：
         class B(A):
           ......
           def method(self, x)
             return super(B,self).method(x)  //python3中可以省略super中的参数
    
    instance.method(参数列表)  //通过实例调用方法
    class.method(instance,参数列表)  //通过类名调用方法
    实际上第一种调用会转化为第二种，当通过类实例来调用方法时，python会搜索继承树来确定方法所属的类
        如果是父类中继承来的方法，则通过父类名调用方法，并传入当前实例的引用。
        #即用方法所属的类调用方法，然后传入当前实例的引用，从而完成方法调用
    
    对于类属性，若为不可变类型(number,string,tuple),则在用实例调用类属性并修改时，由于改变了引用，这个
        引用将不再指向类属性，而会变成一个实例属性如 man.count=5时Man.count不变，man实例中的count属性为5

13、多态和动态语言的鸭子类型

    多态:一个类的子类，在对其共有属性和方法进行操作时，子类可作为其父类类型进行传递，根据传入的类型不同进行子类的
        动态调用，从而保持了接口在面对不同子类时保持同样的接口，同时还能根据不同动态调用
    鸭子类型:静态语言如java类型是严格匹配的，在python中并不要求严格的继承关系，一个对象只要看起来想鸭子，即实现了
            对象的某些方法即可当作某种对象进行传递使用(看起来像鸭子，走起路来像鸭子，就可以被当作鸭子)

14、同步IO

    流stream是单向的,input stream是从网络/磁盘->内存,output stream内存->网络/磁盘
    由于cpu和内存的存取速度远大于网络或磁盘,所以就出现了同步IO和异步IO
    <1>文件操作(操作系统一般不允许外部直接操作磁盘,一般通过请求系统打开文件对象并通过系统提供的接口进行读取,python在内部进行了封装)
        打开文件对象：
            with open(路径,“打开方式rwab+”) as name:     #with块用于让系统在合适时候自动关闭文件,也可手动用close()关闭
                文件的相关操作                           #open返回打开的文件对象，as name用于给此对象命名之后就可以
                                                       #用name访问此文件对象(对文件操作必须先打开文件并获得文件对象)
                                                       #w写入操作  a追加操作 r只读操作 b二进制方式
        读取文件:
            .read(size) 用于读取文件所有内容/size大小的内容   #文件小是可以一次读取
            .readline() 返回一行                           
            .readlines() 以行读取文件内容(返回列表)          #读取配置文件时按行读取
            或者用for line in file_object: 来遍历文件对象中的每一行
            open中可选参数还有:encoding="unicode",errors="ignore"
        写入文件：
            .write() 写入内容(不会自动添加回车)
        文件内置属性和方法：
          属性：
              file.closed 文件是否关闭
              file.mode  文件打开方式
              file.name  文件名
              file.softspace  末尾是否强制加空格
          方法：    
              打开文件会调用file object的内置方法__enter__()
              关闭文件会调用file object的内置方法__exit__()
              .seek(offset[,from]) 用于定位，offset要偏移的字节
                  from：相对位置 0从开头 1从当前位置 2从末尾
              .tell() 返回文件中指针当前位置
      <2>内存读写
         StringIO:在内存中读写str,需要from io import StringIO
                  需要常见以个StringIO对象f=StringIO()/用字符串作为初始化参数
         BytesIO：在内存中读写bytes,需要from io import BytesIO
                  先创建BytesIO对象f=BytesIO()/二进制作为初始化参数
         之后二者就可以像文件一样使用了
15、异常

    格式：try:                                      #try-except-else异常处理块一般用于依赖外部条件的处理
              可能出现异常的代码块                  #由于外部条件的不定导致可能出现异常，如用户输入、指定文件、网络连接等
          except excption：                       #except块可以有多个用于捕获不同的异常
              异常时的处理块/pass                   #pass语句用于不做反映时使用
          else:
              未发生异常时候的处理块
          finally:                                #finally块可以没有
              一定会被执行的代码
    错误也是类:错误类之间的派生关系如下--
              BaseException                       #所有错误类的基类/父类
              +-- SystemExit
              +-- KeyboardInterrupt
              +-- GeneratorExit
              +-- Exception(其他所有类都是它的子类)
              
              所以我们也可以定义自己的错误类,只需要让它继承上述错误类既可,捕获一个错误
                  就是捕获一个错误类的实例,对于自定义错误类,想要抛出一个错误我们需要使
                  用-> raise 错误类实例  的方式抛出一个错误类实例
                  不带参数的实例会原样抛出except模块捕获的错误
              常见exception： ZeroDivisionError 除0异常
                             FileNotFoundError 文件未找到异常
                             TypeError  类型错误异常
    调用栈：错误如果没有被捕获,它会被一致向上抛出,最后被python解释器捕获,这些信息会被放在栈中
           所以出现错误时,我们一定要分析错误的调用栈信息,才能定位错误的位置.
           我们也可以使用模块logging来记录错误信息,使程序可以继续执行(通过配置可输出到日志文件)
               import logging                       #导入logging模块
               except Exception as e:
                   logging.exception(e)             #将捕获的错误信息输出到logging
16、调试

    <1>断言assert
        语句:assert 判断表达式, 异常时输出信息               #当表达式为真时是true,否着抛出异常
                                                         #AssertionError，其输出信息为定义
        通过加-O参数来关闭断言
        
    <2>logging
        logging可以指定记录信息的级别,也可以将信息输出到文件等不同地方
        改变级别:logging.basicConfig(level=logging.INFO/DEBUG/WARNING/ERROR)
        输出:logging.info(信息)/debug()/warning()/error()
        
    <3>pdb调试
        通过在命令行(python -m pdb 文件名) 来使用pdb调试工具
        import pdb  ->选定地点pdb.set_trace()来设置断点
        l:查看代码 
        n:单步执行下一条代码(默认显示的是要执行的下一条代码) 
        p 变量名:打印变量值

17、存储python数据结构(持久化python对象存储)

    使用json存储或读取配置文件等数据信息是比较常用的做法
    首先import json
        json.dump(数据,文件对象)  存储数据到文件中,一般json数据文件以.json后缀(应先打开文件)
        json.load(文件对象)     从文件对象中加载数据
        
    使用pickle
        pickle模块将内存中的Python对象转化成可以写入任意文件类型的序列化字节流
          也可以根据文件中的序列化字节流重新构建内存中的Python对象
        import pickle
        file = open("filename","wb")  //二进制方式打开文件返回文件描述符
        pickle.dump(对象,file)        //持久化对象到文件中
        对象=pickle.load(file)        //从文件中重构对象
        file.close()
        #对于Python的内置数据类型可以直接使用pickle序列化，自定义类对象需要手动处理
        #使用pickle的缺点是需要一次pickle进或出文件中的所有数据
        #很多应用程序用网络传输pickle后的Python对象来做为SOAP和XML-RPC等网络服务的简单替代
        
    使用shelve
        shelve就像一个存储持久化对象的持久化字典，它自动将对象pickle进和出键访问文件系统
            打开shelve文件后你可以像字典一样通过键访问每条记录，shelve会自动分隔记录
            
        import shelve
        bob={...}/对象实例
        sue={...}/对象实例
        db = shelve.open("shelve_file")  //会创建已shelve_file问文件名的.bak .dir .dat
        db["bob"] = bob      //shelve会自动pickle化为一条记录{"bob":{...bob对象...}}
        db["sue"] = sue
        
        db["bob"]["name"]    //shevle会反pickle出键值为bob的记录
        db.close()           //关闭shelve对象

18、代码测试

    通过标准库中的unittest库来进行代码测试
    单元测试用于测试函数某个方面，测试用例由多个单元测试组成
    步骤：  先导入unittest库                   import unittest
            再导入需要测试的函数               from 模块 import 函数名
            创建类继承unittest.TestCase类      class 类名(unittest.TestCase):
            定义多个单元测试函数                   def test_测试函数(self):
                                                       ...
                                                       self.assertEqual(数据1,数据2)  #断言 数据12相等是打印ok否则打印Failed
            让python运行测试                   unittest.main()                        #所有以test_ 打头的方法都会被自动执行
    
    对于类的测试： 一般测试类就是测试类的方法,通过在类中定义 def setUp(self):方法并在其中实例化要测试的类对象
                   就可以在测试类中的其它单元测试上使用这个类对象了。
                   测试类先执行setUp()方法-->然后执行test_ 开头的测试方法-->最后执行tearDown()方法
                   setUp()和tearDown()方法会在每个调用的测试方法前后分别执行
    
    运行单元测试:1、在代码中添加if __name__=__main__： unittest.main()来把测试文件当作正常python脚本执行
               2、通过命令行python -m unittest 文件名
    
    常用断言：  assertEqual(a,b)     核实a==b
                assertNotEqual(a,b)  
                assertTrue(x)        核实x为True
                assertFalse(x)
                assertIn(item,list)  核实item在list中
                assertNotIn(item,list)

19、python解释器

    Cpython 默认的自带解释器，用C语言编写
    Ipython 以Cpython为底层的交互性解释器
    pypy    用JIT技术对python代码进行动态编译(代码执行结果可能不同)
    Jython  java平台的python解释器，python代码->java字节码
    IronPython  .Net平台python解释器，python代码->.Net字节码
    在java和.Net平台上最好使用网络调用，确保各程序之间的独立性

20、linux下的python版本切换

    使用工具update-alternatives
    update-alternatives --list python3   #列出与python3相关的列表
    如果没有关联，用一下命令关联(2的优先级较高)
        sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.5 1    
        sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.6 2
    update-alternatives --config python3 #此命令用来配置默认python3启动的版本
    (mint下默认python3.6会出现黑屏、终端打不开，此时需要在tty中重新设为3.5版本)  

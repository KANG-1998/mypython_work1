
# 第一章：数据类型（基本数据类型和组合数据类型）

![image.png](attachment:image.png)

# (1)基本数据类型

# 1.数字类型


```python
分类：整数，浮点数，复数
```

# 1.1整数


```python
进制包括：10进制（无引导符号）默认进制；2进制（0b或0B开头，eg：0b101）；
                8进制（0o或0O前一个是0后一个是欧，eg：0o711，0O711）；16进制（0x或0X，0-9,10-15用a-f或A-F，eg：0xabc）。
    错误示范：每位上的数值超过进制表达范围则报错SyntaxError
```


```python
0b102    #二进制中不能超过1
```


```python
0o78    #八进制中值不能超过7
```


      File "<ipython-input-16-38e63d621149>", line 1
        0o78
           ^
    SyntaxError: invalid syntax
    



```python
进制转换算法：
```


```python
def transfer(num,base):#输入的十进制数num转化位base进制数，结果以字符串形式输出
    ls=[]
    strs=''
    while num//base!=0:#整数商为零表明，上一次计算所得的整数商的值已小于base-1即进制所能表达的数
        ls.append(num%base)
        num=num//base
    ls.append(num)#小于base-1即进制所能表达的数，直接添加在列表末尾
    ls.reverse()#余数反序得进制转化后的列表
    for i in ls:
        strs+=str(i)
    print(strs)
transfer(8,2)  
     
```

    1000
    


```python
len(10002)#len函数不能计算整数的位数，要计算整数的位数，只需将整数转换位字符串类型，通过计算字符串长度确定整数长度
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-30-5375f7096c0a> in <module>
    ----> 1 len(10002)
    

    TypeError: object of type 'int' has no len()



```python
len(str(10002))#请叫我陈独秀
```




    5




```python
ls=[1,2]
str(ls)
```




    '[1, 2]'



# 1.2浮点数


```python
表示方法:
（1）十进制表示：数学类型表示eg：0.0，-3.14，1000.0
    （高能预警：当小数点后为0的时候可以省略不写eg：77.）
```


```python
-77.
```




    -77.0




```python
（2）科学计数法表示：<a>e<b>=a*pow(10,b)#10的b次方不会输入
    eg：4.2e2，12e1
```


```python
12e1
```




    120.0



（此处有雷，请慢行：1.0.0与0表示不同且处理不同；
                    2.浮点型数据最多输出17位数字（不包括小数点），但只能保证15位精度，二进制计算结果存在误差
                    整数运算能确保其准确性，故可以先以整数计算后表示为浮点数，内置库Decimal的处理方案；
                    3.部分小数二进制无法表示，只能以最接近的数表示，还是推荐Decimal库处理）


```python
3+0.2+0.1
```




    3.3000000000000003



# 1.3复数


```python
表示方法：a+bj    eg：12.3+4j，-5.6+7j
（雷区慢行：复数类型中，实数部分和虚数部分都是！！！‘浮。。。。。点。。。。。数’浮点数牛x！！！！！！）
 取出复数的实部虚部方法：那当然是 （复数）.real ,（复数）.imag
```


```python
print((12.3+4j).real)
print((12.3+4j).imag)#虚部的系数是按浮点型处理的（虽然是整数4），浮点数牛x
```

    12.3
    4.0
    

# 1.4数字类型的操作


```python
9大操作符：+x,-x,x+y,x-y,x*y,x/y,x//y,x%y,x**y
即，正，负，加，减，乘，除，整除（整数商），取余，幂次
```


```python
对整数num取高位数和低位数的方法：
取低n位（取余运算）：num%pow(10,n)#10的n次方是n+1位，取到的是低n位
取高n位（整数商运算）：num//pow(10,len(str(num))-n)#len(str(num))计算出整数的位数
取中间自右第n位：先求出低n位，再求出最高位
```


```python
print(10001%10)
print(19000//pow(10,len(str(19000))-3))
num=19876#取倒数第三位的值8
num1=num%pow(10,3)
num2=num1//pow(10,len(str(num1))-1)
print(num2)
```

    1
    190
    8
    

![image.png](attachment:image.png)


```python
print()函数的小心思
```


```python
print(num='123')#print()当中不能有表达式但print('a',end='')第二个参数例外
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-41-41ef99bf1ae9> in <module>
    ----> 1 print(num='123')
    

    TypeError: 'num' is an invalid keyword argument for print()



```python
print(12)#整数
print(12.2)#浮点数
print('a')#字符串
print([0,1])#列表
print((0,1))#元组
print({1:2})#字典
print({1,2})#集合
```

    12
    12.2
    a
    [0, 1]
    (0, 1)
    {1: 2}
    {1, 2}
    


```python
for i in range(5):
    print('a',end='')
```

    aaaaa

# 1.5内置的数字类型的运算函数与数字类型转换

# 1.5.1内置运算函数


```python
abs(x):取绝对值；
pow(x,y[,z]):z是对幂次取余；
round(x[,ndight]):对x经行四舍五入，可选参数ndight位保留小数位数
divmod(x,y):(x//y,x%y)x与y的整数商和余数的二元组
min(x1,x2....,x3)不说也知道啊
max(x1,x2...,x3)
```


```python
print(pow(10,2))
print(pow(10,2,6))
print(round(3.1415926))
print(round(3.1415926,2))#保留两位小数位👌
divmod(10,3)#整数商和余数的元组d
```

    100
    4
    3
    3.14
    




    (3, 1)



# 1.5.2内置数值类型转化


```python
int(x):可将，整型，浮点数，和字符串😱转化为整数,整型数也可以处理
float(x):整数，浮点数，字符串（只包括整型，浮点型字符串）
complex(re[,im]):实部可以为整型，浮点型，和字符串（只包括整型，浮点型字符串）😁
```


```python
int('12.2')#不可以处理整形字符串以外的字符串
```


    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    <ipython-input-16-d3ba0f7fd590> in <module>
    ----> 1 int('12.2')
    

    ValueError: invalid literal for int() with base 10: '12.2'



```python
print(int(12))#处理整形数试试
print(int('12'))#只可以处理整数字符串😂
print(int(float('12.2')))#如果是浮点型字符串，则先通过float（）转化成浮点数在转化为整数
```

    12
    12
    12
    


```python
int([1,2,3])#测试一下列表果然不能用😁
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-24-b245c803b39f> in <module>
    ----> 1 int([1,2,3])
    

    TypeError: int() argument must be a string, a bytes-like object or a number, not 'list'



```python
print(float(12))
print(float(12.2))
float('12')#测试的字符串，如我所料不包括字符型字符串
float('12.2')
float('abc')
```

    12.0
    12.2
    


    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    <ipython-input-29-dfdf917b4fa5> in <module>
          3 float('12')#测试的字符串，如我所料不包括字符型字符串
          4 float('12.2')
    ----> 5 float('abc')
    

    ValueError: could not convert string to float: 'abc'



```python
print(complex('12.2'))
print(complex('12'))
print(complex('abc'))#只有整型，浮点型字符串可以作为实部
```

    (12.2+0j)
    (12+0j)
    


    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    <ipython-input-33-4b53f46bc156> in <module>
          1 print(complex('12.2'))
          2 print(complex('12'))
    ----> 3 print(complex('abc'))
    

    ValueError: complex() arg is a malformed string


# 1.6math库的使用（内置库）


```python
库的引用方法：import 库名
              from 库名 import 函数名
```

# 1.6.1math的数学常数


```python
常数：math.pi;math.e;math.inf(正无穷大，-math.inf为负无穷大）math.nan(非浮点数标记)
```


```python
import math
a=math.nan#非浮点数标记是一个浮点型型
print(a)
print(type(a))#
print(math.isnan(a))
b=math.inf
print(b)
print(type(b))#无穷大标记是一个浮点数类型
print(math.isinf(b))
```

    nan
    <class 'float'>
    True
    inf
    <class 'float'>
    True
    


```python
print(float('inf'))
print(float('-inf'))
print(float(inf))
```

    inf
    -inf
    


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-76-7e44e826aa1b> in <module>
          1 print(float('inf'))
          2 print(float('-inf'))
    ----> 3 print(float(inf))
    

    NameError: name 'inf' is not defined



```python
print(float('nan'))
print(float(nan))
```

    nan
    


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-77-33b9da6a0992> in <module>
          1 print(float('nan'))
    ----> 2 print(float(nan))
    

    NameError: name 'nan' is not defined


# 1.6.2math的数值函数（幂对函数以后再聊）


```python
#math.fsum([x1,x2,...x3]):浮点数精确求和
import math
print(0.1+0.1+0.1)
print(math.fsum([0.1,0.1,0.1]))# 事实证明math.fsum()函数对0.3是无效的，0.3NB
print(math.fsum([0.1,0.2,0.3]))
```

    0.30000000000000004
    0.30000000000000004
    0.6
    


```python
math.ceil(x):大于等于此值的最小整数
math.floor(x):小于等于x的最大整数
```


```python
print(math.ceil(4))#对于整数而言两者的取值结果相同👌，吾真乃神人也
print(math.floor(4))
print(math.ceil(4.1))#应得5
print(math.floor(4.1))#应得4
math.ceil('a')#显然不能比较字符串只限数值类型，
```

    4
    4
    5
    4
    


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-4-4e6a53ec2357> in <module>
          3 print(math.ceil(4.1))#应得5
          4 print(math.floor(4.1))#应得4
    ----> 5 math.ceil('a')
    

    TypeError: must be real number, not str



```python
math.factorial(x):返回x的阶乘（小数和负数没有阶乘，报错ValueError）
```


```python
print(math.factorial(4))
math.factorial(4.1)# 就是这样婶的
```

    24
    


    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    <ipython-input-5-e3cbdce11abf> in <module>
          1 print(math.factorial(4))
    ----> 2 math.factorial(4.1)
    

    ValueError: factorial() only accepts integral values



```python
math.modf(x):返回x的整数和小数部分
```


```python
result=math.modf(4.1)
math.fsum(result(0))
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-7-630d111bb522> in <module>
          1 result=math.modf(4.1)
    ----> 2 math.fsum(result(0))
    

    TypeError: 'tuple' object is not callable


# 1.7字符串类型及其操作


```python
表达方式：单引号形式eg：'范韩宁牛B'
          双引号形式eg："范韩宁牛B"
          （🐷单双引号都是单行字符串）
          三引号形式eg：'''范韩宁牛B'''   '''范韩宁牛B
                          范韩宁牛B'''
          （三引号并非三对单引号，也可以是三对双引号。三种引号之间是可以相互嵌套的，可以互相包含😱妈妈耶我简直是个天才）
```

# 新的风暴已经出现（字符串的三引号与注释的三引号）
多行注释本质还是多行字符串，依然会被执行，python只包括#一种注释方法。


```python
'范韩宁   # 单行字符串表示多行出现错误🙃佩服的五体投地
牛逼'
```


      File "<ipython-input-8-4e2ff55c1d51>", line 1
        '范韩宁
            ^
    SyntaxError: EOL while scanning string literal
    



```python
print('''范韩宁牛B''')
print('''范韩宁牛B
                          范韩宁牛B''')
print("""范韩宁牛B""")
```

    范韩宁牛B
    范韩宁牛B
                              范韩宁牛B
    范韩宁牛B
    


```python
'范韩宁"牛"B'# 事实证明单引号当中是可以有双引号的🙃对自己佩服的五体投地
'范韩宁"""牛"""B'
```




    '范韩宁"""牛"""B'



# Python内置的字符串处理函数


```python
chr(x):x(Unicode编码)对应的字符
ord(x):x单字符对应的Unicode编码
hex(x):x(整数)对应的十六进制的字符串
oct(x):x(整数)对应的八进制的字符串
```


```python
print(chr(10004))
print(chr(9801))
print(ord('✔'))
print(ord('♉'))
```

    ✔
    ♉
    10004
    9801
    


```python
ord(♉)#说明♉被看作一个变量来看😁，是这样婶滴
```


      File "<ipython-input-9-1240f6955caa>", line 1
        ord(♉)
            ^
    SyntaxError: invalid character in identifier
    



```python
hex(255)#返回的是对应16进制数值的字符串
```




    '0xff'



# 字符串内置的处理函数（stringname.function()类型不是通用，只限字符串）

str.lower()
str.upper()
str.islower()#有一个判断小写就够判断大小写了
str.isprintable()#师傅都是可打印的内容
str.isnumeric()#（🐷🐷两头猪表示震惊）判断整数字符串
str.isspace()#判断🐷🐷只含空格字符串，🐷🐷而不是空字符串

![image.png](attachment:image.png)


```python
a="12.2"
a.isnumeric()
```




    False




```python
b='12'
b.isnumeric()
```




    True




```python
c=''
c.isspace()
```




    False




```python
c='  '#包含两个空格
c.isspace()
```




    True



str.endswith(substr[,start[,stop])#判断在片段中师傅🙃以substr结尾
str.startswith(substr[,start[,stop])#开头


```python
a='abcd'
a.endswith('d',0,len(a))#不空时
a.endswith('d',0,)#可以空着最后一个参数
a.endswith('d')#空两个时的形式
```




    True




```python
a.endswith('d',,len(a))#不能空着中间
```


      File "<ipython-input-12-f0be3961f025>", line 1
        a.endswith('d',,len(a))#不能空着中间
                       ^
    SyntaxError: invalid syntax
    



```python
a.endswith('d'，，)#后两个空着时不要写逗号，否则出错
```


      File "<ipython-input-15-6ed9038d87af>", line 1
        a.endswith('d'，，)#后两个空着时不要写逗号，否则出错
                       ^
    SyntaxError: invalid character in identifier
    


str.split(splitflg,maxsplit=-1)#maxsplit（分割次数）可不写（😱震惊😱默认为-1即全部分割）


```python
d=' abc def '#😱震惊😱当分隔符位于字符串两端时，😱分割后得到的是空串😱
d.split(' ',-1)
```




    ['', 'abc', 'def', '']




```python
d.split(' ',1)
```




    ['', 'abc def ']



str.count(substr[,start[,stop])#字串出现的次数


```python
d.count(' ')#有三个空格，后两个参数默认
```




    3



str.replace(oldstr,newstr[,count])#替换次数可设置


```python
d.replace(' ','#',2)
```




    '#abc#def '




```python
d.replace(' ','#',)#同以上空最后一个时，可以加逗号
```




    '#abc#def#'




```python
d.replace(' ','#')
```




    '#abc#def#'



str.center(width[,fillchar])#居中化函数,自身长度len(str)>=所要求长度width时，不用填充


```python
a='a'
a.center(4,"#")#😁事实证明其并不一定在中心，不在两边就行😁
```




    '#a##'




```python
a.center(1,'#')#😁长度相等时也不填充
```




    'a'



str.zfill(width)#格式化数字字符串（大于等于目标长度时，返回字符串，小于时在左侧补0（有+-时补后面）


```python
a='123'
a.zfill(4)
```




    '0123'




```python
a='+123'
a.zfill(5)#加减号也算长度
```




    '+0123'




```python
a.zfill(3)#len(a)>=width时返回原字符串
```




    '+123'



str.strip(strings)#strings末端可能含有的字符组成字符串（不分顺序）


```python
d.strip('f a')#😱说明包含两端字符删除后继续重复执行，直到两端不含strings中所有的字符😱
```




    'bc de'




```python
d.strip('a')
```




    ' abc def '



str.join(iterable)#


```python
m='nb'
m.join(['人生苦短','我学python'])
```




    '人生苦短nb我学python'




```python
m='-'
m.join(['人生苦短','我用python'])
```




    '人生苦短-我用python'



![image.png](attachment:image.png)

# str.format()#不多说:字符串类型的格式化

其中的str中{}内包括：<参数序号（从0开始）>:<格式控制标记>
格式控制参数：填充|对齐（<左对齐,>右对齐,^居中对齐）|宽度|,(千分位)|"."+"精度"(浮点数时表示小数点的精度;字符串时表示字符串的最大输出长度)
                |类型（整数类型时b,c,d,o,x,X;浮点数类型时e,E,f,%）
                类型：
                   1. 整数类型的输出格式：
                    b:输出整数的二进制方式
                    c:输出整数对应的Unicode字符
                    d:输出整数的十进制fangshi
                    o:以八进制格式输出
                    x:以小写十六进制输出
                    X:以大写十六进制输出
                    浮点数的输出格式：
                    2.浮点类型的输出格式：
                    e:小写字母e的指数格式
                    E:大写字母E的指数格式
                    %:浮点数的百分数形式


```python
s='python'
t='great'
'{1:-^30}{0:.4}'.format(s,t)#测试1 "."+"精度"控制字符输出长度；2填充字符+居中方式+宽度（组团使用）
```




    '------------great-------------pyth'




```python
'{0:,}'.format(1234567)
```




    '1,234,567'




```python
'{0:.4}'.format(1234567)#精度设置不允许使用在整数上0-1114111以外
```


    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    <ipython-input-17-a24283e54c79> in <module>
    ----> 1 '{0:.4c}'.format(1234567)
    

    ValueError: Precision not allowed in integer format specifier



```python
'{0:c}'.format(1234567)#以Unicode格式输出时有其转化范围
```


    ---------------------------------------------------------------------------

    OverflowError                             Traceback (most recent call last)

    <ipython-input-19-4d4f7f681d0d> in <module>
    ----> 1 '{0:c}'.format(1234567)
    

    OverflowError: %c arg not in range(0x110000)



```python
pow(16,4)+pow(16,5)
```




    1114112



测试浮点数输出格式


```python
'{0:e}{0:E}{0:f}{0:%}{}'.format(3.14)#输出与槽数不匹配
```


    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    <ipython-input-21-d34bad619d6b> in <module>
    ----> 1 '{0:e}{0:E}{0:f}{0:%}{}'.format(3.14)
    

    ValueError: cannot switch from manual field specification to automatic field numbering



```python
'{0:e}，{0:E}，{0:f}，{0:%}'.format(3.14)#😱只要标注参数序号相同可以一个变量多种输出😱
```




    '3.140000e+00，3.140000E+00，3.140000，314.000000%'




```python
print("{}{}".format(（1,2）))元组不拆包将作为一个元组看待
```


      File "<ipython-input-59-06d434e001d2>", line 1
        print("{}{}".format(（1,2）))
                             ^
    SyntaxError: invalid character in identifier
    



```python
print("{}{}".format((1,2),3))
```

    (1, 2)3
    

![image.png](attachment:image.png)

# 字符串的索引与切片


```python
😱😱敲黑板划重点了！！！！！字符串索引方法：stringname[index]😱索引用的是[]!!!!!!!!中括号!!!!!!!!😱
```


```python
a='abc'
a(1)#用小括号索引，错了吧😜
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-15-ad3cb171d633> in <module>
          1 a='abc'
    ----> 2 a(1)
    

    TypeError: 'str' object is not callable



```python
字符串的切片stringname[N:M:k]：k为步数，🐷特例：1代表依次向右（顺序），-1代表依次向左（逆序）可以借此获得string反转的副本🐷
```


```python
c='abc'
print(c[::1])
print(c[::-1])
```

    abc
    cba
    


```python
print(id("abc"))
print(id(strs[::-1]))#说明反转后返回的是一个副本，进而证明了字符串类型是不可变类型
```

    1921410852376
    1921451866296
    

# 1.8序列类型的通用操作符和函数

![image.png](attachment:image.png)


```python
通用操作符（造作啊）系列
x in s      #返回的时True或False
x not in s #返回的时True或False
s+t        #连接s和t，合二为一
s*n或n*s   #
s[i]       
s[i:j]     #分片
s[i:j:k]   #步骤分片，注意k=-1时的反转操作
通用函数系列l
len(s)      #测定元素个数
s.count(x)  #序列s中x的个数：🐷（一定要说明哪一个元素在那个列表中的个数）🐷
s.index(x[,i[,j]])#序列中从i到j范围内x🐷（第一次出现的位置）🐷
min(s)    #序列中的最小元素!!!!!!!!!!!!!!!!!!!!!!依据什么比较大小？？？？？？？？？？？？？？？？？ASCII？？？？
max(s)    #最大元素

```


```python
s='abc'#测试连接
t="def"
s+t
```




    'abcdef'




```python
print(s*2)#测试复制
print(2*s)
```

    abcabc
    abcabc
    


```python
len(s)#测试元素个数
```




    3




```python
s.index('a',0,3)#测试元素位置
```




    0




```python
strs='125b#'
min(strs)
```




    '#'




```python
列表的ls1.extend(ls2)方法与s+t连接
```


```python
ls=['abc','abb1']#看来不是依据元素长度
min(ls)
```




    'abb1'



# 区分可变类型和不可变类型的方法


```python
print(id("abc"))
print(id(strs[::-1]))#说明反转后返回的是一个副本，进而证明了字符串类型是不可变类型
```

    1921410852376
    1921451866296
    

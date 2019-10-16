
# 第二章

组合类型包括：1序列类型（字符串，元组，列表），2集合类型（集合），3映射类型（字典）

# 1序列类型（存在顺序关系）

# 1.1元组（tuple）

元组表示：逗号和圆括号（可选）
特点：1有序。2内容不可改变。


```python
a=1,2,3,4
b=1,2,3,4
print(id(a))#元组该咋解释？
print(id(b))
a1='a'
a2='a'
print(id(a1))#字符串
print(id(a2))
c=1
d=1
print(id(c))#整数
print(id(d))
e=12.2
f=12.2
print(id(e))#浮点数
print(id(f))
```

    1928693303080
    1928693301400
    1928652302464
    1928652302464
    140733399995200
    140733399995200
    1928692696312
    1928692696576
    


```python
a[0]=1#元组不可改变
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-15-f9da761c742a> in <module>
    ----> 1 a[0]=1
    

    TypeError: 'str' object does not support item assignment



```python
a=([1,2],)#凡是都有特例，元组不可变但元组可变元素可以改变
a[0][0]=2
print(a)
```

    ([2, 2],)
    


```python
a=()#空括号创建一个空元组
print(a)
type(a)
```

    ()
    




    tuple



元组嵌套可以用多级索引查询


```python
color=('red','blue',('cat','dog','tiger'))
color[2][2]
```




    'tiger'



适用情况：1函数多返回值
       2多变量同步赋值（拆包）
       3循环遍历（拆包实现）


```python
def tester(x):
    return x,x**3
a,b='cat','dog'
a,b=b,a#同步赋值实现两数的值互换
print(a,b)#
print((a,b))
for x,y in ((1,2),(3,4),(5,6)):
     print(x,y)
```

    dog cat
    ('dog', 'cat')
    1 2
    3 4
    5 6
    

关于print()函数：
1可以输出多个值，
2默认输出的值之间以空格间隔，
3所有值输出以后有一个换行符'\n'


```python
help(print)
```

    Help on built-in function print in module builtins:
    
    print(...)
        print(value, ..., sep=' ', end='\n', file=sys.stdout, flush=False)
        
        Prints the values to a stream, or to sys.stdout by default.
        Optional keyword arguments:
        file:  a file-like object (stream); defaults to the current sys.stdout.
        sep:   string inserted between values, default a space.
        end:   string appended after the last value, default a newline.
        flush: whether to forcibly flush the stream.
    
    


```python
len(a)
```




    3



# 1.2列表（list）

列表：包含0个或多个😱对象引用😱的有序序列
表示：[]表示
列表复制需要显式赋值（整数和字符串可以隐式赋值eg:a=1 b=a）
列表不会预分配存储空间


```python
a=1
print(id(a))
a=2
print(id(a))
la=[1,2]
print(id(la))
la.append(3)
print(id(la))
la.append(4)
print(id(la))
```

    140733405369152
    140733405369184
    1773640287560
    1773640287560
    1773640287560
    

列表类型的函数

ls.extend(lt):等价于ls+=lt,合并两个列表ls在前lt在后
ls.append(x):在末尾添加元素


```python
ls1=[1,2]
print(id(ls1))
ls2=[3,4]
ls1.extend(ls2)#合二为一
print(ls1)
print(id(ls1))
```

    1773640871112
    [1, 2, 3, 4]
    1773640871112
    

ls.insert(pos,x):在第pos位置插入x


```python
ls1.insert(0,0)
print(ls1)
```

    [0, 1, 2, 3, 4]
    

ls.clear():删除所有元素


```python
ls1.clear()
print(ls1)#删除后为空列表
```

    []
    

ls.remove(x):删除列表中第一个出现的元素x


```python
a=[1,1,2,2]
a.remove(1)
print(a)
a.remove(3)#若删除不存在的元素则报错
```

    [1, 2, 2]
    


    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    <ipython-input-14-36bbbff3c853> in <module>
          2 a.remove(1)
          3 print(a)
    ----> 4 a.remove(3)
    

    ValueError: list.remove(x): x not in list


ls.pop(pos):将第pos位置(此位置为元素的序号)元素取出并删除


```python
a=[1,2,3]
result=a.pop(0)
print(result)
print(a)
```

    1
    [2, 3]
    


```python
ls.copy():将表复制到一个新列表，并返回这个新列表（）
```


```python
a=[1,2]
b=a.copy()
print(b)
print(id(a))
c=a
print(c)
print(id(c))
🐷🐷#id一样说明隐性复制的变量c并不是一个新变量而是一个引用🐷🐷
```

    [1, 2]
    1773641561224
    [1, 2]
    1773641561224
    

ls.reverse()#反转不能有参数


```python
a.reverse(1)
print(a)
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-26-a3605f217a56> in <module>
    ----> 1 a.reverse(1)
          2 print(a)
    

    TypeError: reverse() takes no arguments (1 given)


# ls.sort()#列表有sort()函数其他类型没有
高能预警：ls.sort()不会返回，所以，ls=ls.sort(),使得原列表为None


```python
ls=['a','b','c']
ls.sort()#列表有sort()函数其他类型没有
print(ls.sort())#无返回输出None
a='abc'
a.sort()
```

    None
    


    ---------------------------------------------------------------------------

    AttributeError                            Traceback (most recent call last)

    <ipython-input-67-3c3d0c5301a5> in <module>
          3 print(ls.sort())
          4 a='abc'
    ----> 5 a.sort()
    

    AttributeError: 'str' object has no attribute 'sort'


# 通用函数sorted(),重点🐲返回列表类型


```python
ls=[1,4,3,2]
print(sorted(ls))#列表排序
a='bca'
print(sorted(a))#字符串排序
dict={'a':1,'c':3,'b':2}
print(sorted(dict))#字典排序默认对🔣键排序

```

    [1, 2, 3, 4]
    ['a', 'b', 'c']
    ['a', 'b', 'c']
    

引自https://www.cnblogs.com/pankypan/p/11074372.html

ls.sort([key=None[, reverse=False]])和sorted(iterable[, cmp[, key[, reverse]]])
参数说明：🚎
iterable -- 可迭代对象
cmp -- 比较的函数，这个具有两个参数，参数的值都是从可迭代对象中取出，此函数必须遵守的规则为，大于则返回1，小于则返回-1，等于则返回0
key -- 主要是用来进行比较的元素，只有一个参数，具体的函数的参数就是取自于可迭代对象中，指定可迭代对象中的一个元素来进行排序
reverse -- 排序规则，reverse = True 降序 ， reverse = False 升序（默认）

单个排序法则：


```python
students = [('john', 'A', 15), ('jane', 'B', 12), ('dave', 'B', 10)]
new_students = sorted(students, key=lambda s: s[2])
print(new_students)  # [('dave', 'B', 10), ('jane', 'B', 12), ('john', 'A', 15)]
```

    [('dave', 'B', 10), ('jane', 'B', 12), ('john', 'A', 15)]
    

多种排序法则：


```python
s = 'asdf234GDSdsf234578'  # 排序：小写-大写-奇数-偶数
new_s1 = "".join(sorted(s, key=lambda x: [x.isdigit(), x.isdigit() and int(x) % 2 == 0, x.isupper(), x]))
print(new_s1)  # addffssDGS335722448
```

    addffssDGS335722448
    


```python
原理：

print(sorted([True, False]))  # [False, True]
# Boolean 的排序会将 False 排在前，True排在后  
x.isdigit()的作用把iterable分成两部分，数字和非数字，数字在后，非数字在前

new_s1 = "".join(sorted(s, key=lambda x: [x.isdigit()]))
print(new_s1)  # asdfGDSdsf234234578
x.isdigit() and int(x) % 2 == 0的作用是将数字部分分成两部分，偶数（在后）和奇数（在前）

new_s1 = "".join(sorted(s, key=lambda x: [x.isdigit(), x.isdigit() and int(x) % 2 == 0]))
print(new_s1)  # asdfGDSdsf335724248
x.isupper()的作用是在前面基础上,保证字母小写在前大写在后

new_s1 = "".join(sorted(s, key=lambda x: [x.isdigit(), x.isdigit() and int(x) % 2 == 0, x.isupper()]))
print(new_s1)  # asdfdsfGDS335724248
最后的x表示在前面基础上,对所有类别数字或字母排序

new_s1 = "".join(sorted(s, key=lambda x: [x.isdigit(), x.isdigit() and int(x) % 2 == 0, x.isupper(), x]))
print(new_s1)  # addffssDGS335722448
```

一道面试题
lst = [7, -8, 5, 4, 0, -2, -5]
要求:
正数在前负数在后
正数从小到大
负数从大到小


```python
lst = [7, -8, 5, 4, 0, -2, -5]
new_lst1 = sorted(lst, key=lambda x: [x < 0, x < 0 and -x, x >= 0 and x])  # -3 < 0 and -(-3) ==> 3
new_lst2 = sorted(lst, key=lambda x: [x < 0, abs(x)])
print(new_lst1)  # [0, 4, 5, 7, -2, -5, -8]
print(new_lst2)  # [0, 4, 5, 7, -2, -5, -8]
```

    [0, 4, 5, 7, -2, -5, -8]
    [0, 4, 5, 7, -2, -5, -8]
    

# 3映射类型（字典map）

预警：😱字典是键值对的🐷集合🐷（集合的特例最重要的应用）😱
     字典无序，但可遍历for key in dict:(遍历的是键)
     {}会创建一个新字典而不是集合eg：dict={}
     可以通过增删键值对来修改键值对eg：要修改键就创建新的键值对


```python
a={}
type(a)
```




    dict




```python
a={"-":"fu","1":"yi","2":"er","3":"san","4":"si","5":"wu"\#反斜杠表示延长一行
      ,"6":"liu","7":"qi","8":"ba","9":"jiu"}
num=input()
for i in num:
    if i!=num[-1]:
        print(a[i]+" ",end="")
    else:
        print(a[i])

```

集合只能包括固定数据类型：基本和元组类型；
所以字典（也是集合）同样不能有上述四者以外的类型


```python
d={[1,2]}
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-7-a35d614720af> in <module>
    ----> 1 d={[1,2]}
    

    TypeError: unhashable type: 'list'


字典函数与操作


```python
d={'a':1,'b':2,'c':3}
```

dict.keys()#返回键值
dict.values()
dict.items()
可用list()使其返回一个列表


```python
print(d.keys())#返回的不是列表而是特殊的东西😱
print(d.values())
print(d.items())
print(list(d.keys()),list(d.values()),list(d.items()))
```

    dict_keys(['a', 'b', 'c'])
    dict_values([1, 2, 3])
    dict_items([('a', 1), ('b', 2), ('c', 3)])
    ['a', 'b', 'c'] [1, 2, 3] [('a', 1), ('b', 2), ('c', 3)]
    

dict.get(key[,default])#获得键对应的值,default默认为None


```python
print(d.get('a'))
print(d.get('d'))
print(d.get('d','NO'))
```

    1
    None
    NO
    

dict.popitem()#随机取出一组键值对以🐷元组🐷形式返回(并不删除)


```python
d.popitem()
```




    ('c', 3)



dic.pop(key[,default])#默认的default为KeyError报错


```python
#print(d.pop('a'))
print(d.pop('a',"NO"))#default设置为“NO"
print(d.pop('a'))
```

    NO
    


    ---------------------------------------------------------------------------

    KeyError                                  Traceback (most recent call last)

    <ipython-input-25-60ba613efe5d> in <module>
          1 #print(d.pop('a'))
          2 print(d.pop('a',"NO"))
    ----> 3 print(d.pop('a'))
    

    KeyError: 'a'



```python
del dict[key]#删除确定键值对
```


```python
print(del d['a'])#没有返回值则错误
```


      File "<ipython-input-31-56398a392cbf>", line 1
        print(del d['a'])
                ^
    SyntaxError: invalid syntax
    



```python
del d['a']#默默滴就给删除了
```


```python
type(print())#空也可以执行
```

    
    




    NoneType



dict.clear()#和列表相同

key (not)in dict#操作


```python
'b' in d
```




    True



遍历字典的操作（造作）


```python
for key in d:#遍历的是键
    print(key)#等同于d.keys()造作
    print(d[key])#等同于d.values()造作
```

覆盖特性（键不可重复的特点）：同样的键已经存在，再添加同键的键值对会覆盖前者

# 2集合类型（集合set）

定义：不可重复的固定数据类型（有哈希函数判断）（整型，浮点，字符串，元组四大件）
set(squeue)用于生成集合,是组合数据类型之间的转化(整型，浮点不能为参数)


```python
a=set()#可以空
print(a)
a=set(1)#参数必须是一个序列类型
```

    set()
    


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-42-9498b980df95> in <module>
          1 a=set()
          2 print(a)
    ----> 3 a=set(1)
    

    TypeError: 'int' object is not iterable



```python
print(set([1,2]))
print(set((1,2)))
```

    {1, 2}
    {1, 2}
    

# 集合逻辑处理造作与函数


```python
S={'A','B','C',1,2,3}
T={1,2,3}
```

S-T,S.difference(T)#🐷返回新集合🐷S去除T后的剩余元素集合😱差运算😱
S-=T,S.difference_update(T)#更新集合


```python
S-T
```




    {'A', 'B', 'C'}




```python
S-=T
print(S)
```

    {'B', 'A', 'C'}
    

S&T或S.interaction(T)#返回新集合S,T共有部分😱交运算😱
S&=T或S.intersection_update(T)#更新S为S,T共有部分


```python
S&T
```




    {1, 2, 3}




```python
S&=T
print(S)
```

    {1, 2, 3}
    

S|T#并运算
S|=T#

S^T#新集合S,T排除共有部分后的元素
S^=T

# 集合的操作函数

S.add(x)
S.remove(x)#在集合内移除，否则报错
S.discard(x)#在集合内移除，否则不报错
S.clear()#全部删除(😱可以删除空集合😱)
S.pop()#pop（无参）不再是删除返回，而是随机取出一个，若集合为空报错（死性不改）


```python
M={}
M.clear()
```


```python
S.pop(1)
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-61-7d64849b49be> in <module>
    ----> 1 S.pop(1)
    

    TypeError: pop() takes no arguments (1 given)



```python
S.copy()#返回一个副本
S.isdisjoint(T)#判断两级和没交集
x (not)in S
```


```python
ls=['a','b','c']
ls.sort()
print(ls)
a='abc'
a.sort()
```

    ['a', 'b', 'c']
    


    ---------------------------------------------------------------------------

    AttributeError                            Traceback (most recent call last)

    <ipython-input-66-9212dde3230a> in <module>
          3 print(ls)
          4 a='abc'
    ----> 5 a.sort()
    

    AttributeError: 'str' object has no attribute 'sort'


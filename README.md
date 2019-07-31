### 欢迎大家关注我的公众号『Python3X』，扫描下方二维码( 或微信搜索：python3xxx)。即可关注。

> 主要分享Python类技术干货，包括不限于Python技术、Web开发、爬虫、数据分析等，当然还有不定期的工具干货分享。

<iframe height=500 width=500 src="https://github.com/python3xxx/Python-Every-Day/image_/python3xxx.gif">


![Image text](https://github.com/python3xxx/Python-Every-Day/image_/qr_code.jpg)



# 目录索引：

[001、Python中的可变对象与不可变对象](#001python中的可变对象与不可变对象)

[002、类的定义和装饰器@classmethod与@staticmethod](#002类的定义和装饰器classmethod与staticmethod)

[003、删除列表中的重复元素](#003删除列表中的重复元素)

[004、Python中的lambda表达式](#004python中的lambda表达式)

[005、Python中的可变参数](#005python中的可变参数)

[006、Python中的super()用法](#006python中的super用法)
      
      
      
## 001、Python中的可变对象与不可变对象

对象分为 **可变对象** 和 **不可变对象**。 可通过函数 id() 查看对象的内存地址是否改变


- 可变对象：该对象所指向的内存中的值是可以被改变的，如：String、Tuple、Number。他们本身的值是不可以被改变，修改的时候，会复制一个新的对象，并开辟一份新的内存空间，变量再去指向新的值。
```python
a = 1
print(id(a)) # 4543532032
a = 1 + 2
print(id(a)) # 4543532096
# 证明字符串是可变对象
```


- 不可变对象：该对象所指向的内存中的值是不会被改变的，如：List、Dict、Set。对其进行修改时，并不会像可变对象那样重新复制一份。而是在原有的基础上进行修改。
```python
a = [1, 2]
print(id(a)) # 4362993544
a.append(3)
print(id(a)) # 4362993544
a[1] = 5
print(id(a)) # 4362993544
# 列表是不可变对象
```

## 002、类的定义和装饰器@classmethod与@staticmethod

参考此文：https://mp.weixin.qq.com/s/t1T_K5wbovOAIdzgKjIwhg



## 003、删除列表中的重复元素

1、通过set方法
```python
a = [1, 2, 3, 1, 1, 1, 7, 9, 5]
print(list(set(a)))
```
2、通过fromkeys方法
```python
a = [1, 2, 3, 1, 1, 1, 7, 9, 5]
b = {}
# fromnkeys 创建一个新的字典，已a中的元素作为字典的键
b = b.fromkeys(a)
print(b)  # {1: None, 2: None, 3: None, 7: None, 9: None, 5: None}
c = list(b.keys())
print(c)  # [1, 2, 3, 7, 9, 5]
```
3、逻辑判断
```python
a = [1, 2, 3, 1, 1, 1, 7, 9, 5]
b = []

for i in a:
    if i not in b:
        b.append(i)

print(b) # [1, 2, 3, 7, 9, 5]
```

## 004、Python中的lambda表达式

lambda又称为匿名函数，可以不再去定义函数，使代码更加简洁。
```python
def m(x):
    return x ** 2
print(m(2))
# 等同于函数m()
m1 = lambda x: x ** 2
print(m1(2))
```
更多用法，请参考此文：https://mp.weixin.qq.com/s/CsBpTh0cDyyOT0BZ5cUHwg


## 005、Python中的可变参数

可变参数的形式有

- *args  : 元组类型参数
```python
def fun_arr(name, *args):
    print(name)
    print(args)

if __name__ == '__main__':
    fun_arr('tom')  # 输出 tom 、()
    # tom
    # (20, 'man', '篮球', 'pythoner', '17766666666')
    fun_arr('tom', 20, 'man', '篮球', 'pythoner', '17766666666')
```

- **kwargs ：字典类型参数
```python
def fun_dict(**kwargs):
    for k, v in kwargs.items():
        print(k, v)
    # 也可通过get的方式取参数的值
    # my name is tom i'am 18 years old, my phone number is 17766666666
    print("my name is %s i'am %s years old, my phone number is %s"
          % (kwargs.get('name'), kwargs.get('age'), kwargs.get('mobile')))

if __name__ == '__main__':
    fun_dict(name='tom', age=18, mobile='17766666666')
```

可变参数允许多个任意参数，也允许不传参数。

两个可变参数同时存在是，一定要将 *参数 放在 **参数 之前！！！否则编译错误。

通常情况下，都是将可变参数写在最后面。

> 如果写在前面则会将后面的参数也会收集到列表中。如果将可变参数写在前面，则需要指定后面的参数名

## 006、Python中的super()用法

super()是Python中内置的一个函数，用于调用父类的方法。
```python
class A():
    def eat(self):
        print('i eat food')

class B(A):
    def run(self):
        print('i can run')

b = B()
# 调用父类的eat
b.eat() # i eat food
```

 **如果一个子类继承了两个父类，并且父类中的方法名相同。那究竟会调用哪个类呢？**
 
 这个问题可以通过类的内置属性 __mro__ 去查看调用顺序。这个方法主要是在多继承时判断方法、属性的调用路径。
 ```python
class A:
    num = 1
    def method(self):
        print('A ..method')

class B:
    num = 2
    def method(self):
        print('B .. method')


class C(A, B):
    num = 3
    pass

if __name__ == '__main__':
    c = C()
    print(C.__mro__)  # (<class '__main__.C'>, <class '__main__.A'>, <class '__main__.B'>, <class 'object'>)
    print(c.num)  #  3
    c.method()  # A ..method
```
如上，C.__mro__ 打印结果可以执行顺序为 C -> A - >B

因此print(c.num)。因为c中有num属性，所以会打印3.

执行c.method时 。因为c中没有method属性，会去A中查找，则输出 A..method。

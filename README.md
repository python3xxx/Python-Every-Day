[TOC]

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
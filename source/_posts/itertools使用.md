---
title: itertools使用
type: categories
date: 2021-05-14 15:47:52
categories: 
- python
tags:
 - generate
---



```python
import itertools
```


```python
# accumulate
x1 = itertools.accumulate(range(10))
print(list(x1))
```

    [0, 1, 3, 6, 10, 15, 21, 28, 36, 45]



```python
# chain 连接多个列表的方法
x2 = itertools.chain(range(3), range(4), [3,2,1])
print(list(x2))
```

    [0, 1, 2, 0, 1, 2, 3, 3, 2, 1]



```python
# 列表或生成器中指定数目的元素不重复的所有组合
x3 = itertools.combinations(range(4), 3)
print(list(x3))
```

    [(0, 1, 2), (0, 1, 3), (0, 2, 3), (1, 2, 3)]



```python
# 允许重复元素的组合
x4 = itertools.combinations_with_replacement('ABC', 2)
print(list(x4))
```

    [('A', 'A'), ('A', 'B'), ('A', 'C'), ('B', 'B'), ('B', 'C'), ('C', 'C')]



```python
# 按照真值表筛选元素
x5 = itertools.compress(range(5), (True, False, True, True, False))print(list(x5))
```

    [0, 2, 3]



```python
# 一个计数器,可以指定起始位置和步长
x6 = itertools.count(start=20, step=-1)print(list(itertools.islice(x6, 0, 10, 1)))
```

    [20, 19, 18, 17, 16, 15, 14, 13, 12, 11]



```python
# 循环指定的列表和迭代器
x7 = itertools.cycle('ABC')print(list(itertools.islice(x7, 0, 10, 1)))
```

    ['A', 'B', 'C', 'A', 'B', 'C', 'A', 'B', 'C', 'A']



```python
# 按照真值函数丢弃掉列表和迭代器前面的元素
x8 = itertools.dropwhile(lambda e: e < 5, [i for i in range(10)])print(list(x8))
```

    [5, 6, 7, 8, 9]



```python
# 保留对应真值为False的元素
x9 = itertools.filterfalse(lambda e: e < 5, (1, 5, 3, 6, 9, 4))print(list(x9))
```

    [5, 6, 9]



```python
# 按照分组函数的值对元素进行分组
x10 = itertools.groupby(range(10), lambda x: x < 5 or x > 8)
for condition, numbers in x10:
    print(condition, list(numbers))
```

    True [0, 1, 2, 3, 4]False [5, 6, 7, 8]True [9][]



```python
# 对迭代器进行切片
x11 = itertools.islice(range(10), 0, 9, 2)
print(list(x11))
```

    [0, 2, 4, 6, 8]



```python
# 产生指定数目的元素的所有排列(顺序有关)
x12 = itertools.permutations(range(4), 3)
print(list(x12))
```

    [(0, 1, 2), (0, 1, 3), (0, 2, 1), (0, 2, 3), (0, 3, 1), (0, 3, 2), (1, 0, 2), (1, 0, 3), (1, 2, 0), (1, 2, 3), (1, 3, 0), (1, 3, 2), (2, 0, 1), (2, 0, 3), (2, 1, 0), (2, 1, 3), (2, 3, 0), (2, 3, 1), (3, 0, 1), (3, 0, 2), (3, 1, 0), (3, 1, 2), (3, 2, 0), (3, 2, 1)]



```python
# 产生多个列表和迭代器的(积)
x13 = itertools.product('ABC', range(3))
print(list(x13))
```

    [('A', 0), ('A', 1), ('A', 2), ('B', 0), ('B', 1), ('B', 2), ('C', 0), ('C', 1), ('C', 2)]



```python
# 简单的生成一个拥有指定数目元素的迭代器
x14 = itertools.repeat(0, 5)
print(list(x14))
```


```python
# 类似map
x15 = itertools.starmap(str.islower, 'aBCDefGhI')
print(list(x15))
```

    [True, False, False, False, True, True, False, True, False]



```python
# 与dropwhile相反，保留元素直至真值函数值为假。
x16 = itertools.takewhile(lambda e: e < 5, range(10))
print(list(x16))
```

    [0, 1, 2, 3, 4]



```python
# 生成指定数目的迭代器
x17 = itertools.tee(range(10), 2)
for letters in x17:
    print(list(letters))
```

    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]



```python
# 类似于zip，不过已较长的列表和迭代器的长度为准
x = itertools.zip_longest(range(3), range(5))
y = zip(range(3), range(5))
print(list(x))
print(list(y))
```

    [(0, 0), (1, 1), (2, 2), (None, 3), (None, 4)]
    [(0, 0), (1, 1), (2, 2)]


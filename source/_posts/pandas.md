---
title: pandas操作
date: 2021-06-03 15:56:19
type: categories
categories: 
 - python
tags:
 - pandas
---

[TOC]

# pandas

## 关于iloc与loc

`iloc`:以number为编号获取值。

`loc`:以key获取值。

### 取值操作

```python
df1.loc[1,'pubmedid'] # 同等a = df1.loc[1]['pubmedid'] # 先行值后列值
df1.iloc[0,0] # 同等df1.iloc[0][0]和df1.iat[0,1] # 先行值后列值
```

### 赋值操作

```python
df1.loc[1,'pubmedid'] = 'sdfdf' # df1.loc[1]['pubmedid'] = 'sdfdf' # 报错
df1.iloc[0,-2] = '111111111' # df1.iloc[0][-2] = '111111111' # 报错
```

### 降重操作

```python
df1 = df.drop_duplicates(['paper'])
```

### 计数统计

```python
result = df['Census_OSInstallLanguageIdentifier'].value_counts().plot(kind='bar')
```

### 选取特定值行

```python
df1 = df[df['year']=='2016'] # 选取年份为2016 的行，注意2016的类型是int还是str
```

## 统计

### 根据列值长度筛选

```python
df = df[df['Residue_name1'].str.len()==3]
```

### 查看数目统计信息

```python
df['区域'].value_counts()
print(df['区域'].value_counts(ascending=True)) # 升序
```

## 连接

### 相同信息连接

```python
res = pd.concat(reslist,join='inner') # reslist为含有dataframe的列表 并且只连接相同列
```

## 快速筛选的方法

### query(类似SQL)

```python
df1 = df.query('LigandName in ("HEC","NAG","SF4","HEM","FAD","FES","F3S","FE2")')
```



## 参考

[reference](https://www.cnblogs.com/mrwuzs/p/11325205.html)

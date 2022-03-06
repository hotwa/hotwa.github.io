---
title: PBD文件学习
type: categories
date: 2021-04-06 21:32:13
categories: 
- [warhead,晶体结构]
tags:
 - PDB
 - 生物信息学
---

[pdb文件参考](http://pdb101.rcsb.org/learn/guide-to-understanding-pdb-data/dealing-with-coordinates)

In PDB file format, the temperature factor is given in columns 61 - 66.

alternate conformations are given in column 17 

alternate location indicator and occupancy is given in columns 55 - 60

PDB格式文件使用MODEL / ENDMDL关键字指示单个文件中的多个分子。最初创建该文件是为了存储包括相同结构的多个不同模型的坐标集，例如在NMR分析中获得的结构集合。当您查看这些文件时，您会看到数十个相似的分子全部重叠。现在，还将MODEL关键字用于生物组装文件中，以分隔从不对称单元生成的分子的许多对称拷贝

[PDBX python解析器](https://mmcif.wwpdb.org/docs/sw-examples/python/html/)

[了解PDB数据的指南](http://pdb101.rcsb.org/learn/guide-to-understanding-pdb-data/primary-sequences-and-the-pdb-format)



## [PDB数据简介](http://pdb101.rcsb.org/learn/guide-to-understanding-pdb-data/introduction)

PDB档案库是原子坐标和其他描述蛋白质和其他重要生物大分子的信息的存储库。结构生物学家使用诸如[X射线晶体学，NMR光谱和低温电子显微镜等方法](http://pdb101.rcsb.org/learn/guide-to-understanding-pdb-data/methods-for-determining-structure)来确定每个原子在分子中相对于彼此的位置。然后，他们存储此信息，然后由wwPDB对其进行批注并公开发布到存档中。



## [PDB结构和PDBx/mmCIF格式的关系](http://pdb101.rcsb.org/learn/guide-to-understanding-pdb-data/beginner%E2%80%99s-guide-to-pdb-structures-and-the-pdbx-mmcif-format)

### PDBx/mmCIF格式（使用ASCII字符集）

CIF（晶体学信息文件）扩展（mmCIF）

支持代表大型结构，复杂化学反应以及新的和混合实验方法的数据。

PDBx / mmCIF功能强大。PDBx / mmCIF明确记录了通用数据项（例如原子和残基标识符）之间的所有关系。

> The tabular style is used when there are multiple values for each token. In this style, a loop_ token is followed by rows of data item names and then white-space delimited data values. 
>
> 使用空格分隔

优点：

>可以在单个PDB条目中表示的原子，**残基或链的数量没有任何限制**



## [PDB文件](http://pdb101.rcsb.org/learn/guide-to-understanding-pdb-data/dealing-with-coordinates)

在PDB文件格式中，TER记录用于分隔蛋白质和核酸链。

PDB格式文件使用MODEL / ENDMDL关键字指示单个文件中的多个分子。



由于PDB规范来自于PDBx/mmCIF一些晶体结构信息，所以大致与PDB相当其中不同在于

PDB文件没有loop_字段的描述信息

TER分隔蛋白与核酸链

MODEL / ENDMDL关键字指示单个文件中的多个分子



#### 温度因素

对于储存的温度系数值影响，autodock vina计算过程中温度的影响。

PDB的结构在温度的影响下原子是否发生移动，电子云密度是否发生变化，影响其共价键的距离，从而影响活性。

> 这些运动以及由此产生的电子密度的拖尾，通过B值或温度因子被合并到原子模型中。拖影的量与B值的大小成正比。小于10的值会创建一个非常清晰的原子模型，表明该原子移动不多，并且在晶体中所有分子中的位置相同。大于50左右的值表示原子正在移动太多以至于几乎看不到原子。蛋白质表面的原子经常发生这种情况，其中长的侧链可在周围的水中自由摆动。
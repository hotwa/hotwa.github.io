---
title: PDB文件
date: 2021-05-16 17:03:03
type: categories
categories: 
- PDB文件
tags:
 - 详解
---

[TOC]

# 什么是PDB文件

一种基于晶体衍射测定的分子结构，是一种蛋白质数据库文件。

**PDB**(Protein Data Bank)是一种标准文件格式, 其中包含原子的坐标等信息, 提交给 Protein Data Bank at the Research Collaboratory for Structural Bioinformatics (RCSB) 的结构都使用这种标准格式.

完整的PDB文件提供了非常多的信息, 包括作者, 参考文献以及结构说明, 如二硫键, 螺旋, 片层, 活性位点. 在使用PDB文件时请记住, 一些建模软件可能不支持那些错误的输入格式.

PDB格式以文本格式给出信息, 每一行信息称为一个 记录(record). 一个PDB文件通常包括很多不同类型的记录, 它们以特定的顺序排列, 用以描述结构.

[pdb文件参考](http://pdb101.rcsb.org/learn/guide-to-understanding-pdb-data/dealing-with-coordinates)

In PDB file format, the temperature factor is given in columns 61 - 66.

alternate conformations are given in column 17 

alternate location indicator and occupancy is given in columns 55 - 60

PDB格式文件使用MODEL / ENDMDL关键字指示单个文件中的多个分子。最初创建该文件是为了存储包括相同结构的多个不同模型的坐标集，例如在NMR分析中获得的结构集合。当您查看这些文件时，您会看到数十个相似的分子全部重叠。现在，还将MODEL关键字用于生物组装文件中，以分隔从不对称单元生成的分子的许多对称拷贝

[PDBX python解析器](https://mmcif.wwpdb.org/docs/sw-examples/python/html/)

[了解PDB数据的指南](http://pdb101.rcsb.org/learn/guide-to-understanding-pdb-data/primary-sequences-and-the-pdb-format)



## [PDB数据简介](http://pdb101.rcsb.org/learn/guide-to-understanding-pdb-data/introduction)

PDB档案库是原子坐标和其他描述蛋白质和其他重要生物大分子的信息的存储库。结构生物学家使用诸如[X射线晶体学，NMR光谱和低温电子显微镜等方法](http://pdb101.rcsb.org/learn/guide-to-understanding-pdb-data/methods-for-determining-structure)来确定每个原子在分子中相对于彼此的位置。然后，他们存储此信息，然后由wwPDB对其进行批注并公开发布到存档中。

column：

https://www.rbvi.ucsf.edu/chimera/docs/UsersGuide/tutorials/pdbintro.html



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




## 电子云理论与PDB文件之间的关系

在实际原子与原子之间中化学键连接中电子不断运动的，而基于晶体衍射产生的结果只是蛋白某个瞬间的电子状态。在真实过程中电子云不断运动，蛋白同时结构也是一个柔性结构，是一个**动态的**视频。基于晶体衍射的结果得到的结果是一个**静态的**结果，类似一张照片。

## 标题部分

### HEADER

分子类, 公布日期, ID号

### OBSLTE

: 注明此ID号已废弃, 改用新ID号

### TITLE

: 说明实验方法类型

### CAVEAT

: 可能的错误警告

### COMPND

: 化合物分子组成

### SOURCE

: 化合物来源

### KEYWDS

: 关键词

### EXPDTA

: 测定结构所用的实验方法

### AUTHOR

: 结构测定者

### REVDAT

: 修订日期及相关内容

### SPRSDE

: 已撤销或更改的相关记录

### JRNL

: 发表坐标的期刊

## 氨基酸编号

| 希腊字母 | 英文字母 | 发音    | Alternate_location_indicator |
| -------- | -------- | ------- | ---------------------------- |
| α        | A        | Alpha   | A                            |
| β        | B        | Beta    | B                            |
| γ        | C        | Gamma   | G                            |
| δ        | D        | Delta   | D                            |
| ε        | E        | Epsilon | E                            |
| ζ        | F        | Zeta    | Z                            |
| η        | G        | Eta     |                              |
| θ        | H        | Theta   |                              |
| ι        | I        | Iota    |                              |
| κ        | J        | Kappa   |                              |
| λ        | K        | Lambda  |                              |
| μ        | L        | Mu      |                              |
| ν        | M        | Nu      |                              |
| ξ        | N        | Xi      |                              |
| ο        | O        | Omicron |                              |
| π        | P        | Pi      |                              |
| ρ        | Q        | Rho     |                              |
| σ        | R        | Sigma   |                              |
| τ        | S        | Tau     |                              |
| υ        | T        | Upsilon |                              |
| φ        | U        | Phi     |                              |
| χ        | V        | Chi     |                              |
| ψ        | W        | Psi     |                              |
| ω        | X        | Omega   |                              |
|          | Y        |         |                              |
|          | Z        |         |                              |

### PDB原子表示

总结：对于在PDB文件第三列包含原子的元素名称(**Atom name**)以及原子的定位表述(**Alternate_location_indicator**),对于原子的定位表述为希腊字母的第一个字母的大写，上述表中已经整理部分并验证。对于Epsilon和Eta手写字母相同，暂不知具体在PDB表述。对于在后原子的定位表述中的阿拉伯数字，常常为化学结构具有对称性结构，其原子有同位等效性。在环中出现多。与IUPAC 名称命名一致，系统命名法。


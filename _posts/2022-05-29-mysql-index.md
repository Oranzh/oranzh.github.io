---
title: Mysql InnoDB 索引模型
author:
  name: Friday
  link: https://github.com/oranzh
date: 2022-05-31 22:00:00 +0800
categories: [Mysql]
tags: [Mysql]
render_with_liquid: false

---



## InnoDB引擎

InnoDB现在是mysql的默认引擎 ，而引擎的作用是储存和查询数据。相应就会有效率问题，查更为突出，也有就了索引，就是为了提高查询效率，好比现代汉语字典的目录一样。InnoDB的索引模型是B+树。

## 索引为什么可以提高查询效率？

读数据的时候，需要将数据从磁盘读到内存中，访问的单位是页，Mysql的页是 16K，这其中就有IO操作，非常耗时，读取一笔记录的时候大概是10ms。所以说减少IO次数，就会提高查询效率。


## 索引类型

- **主键索引**  **<id, row>**

  1. Primary Key  

     *如果有，则为主键索引*

  2. Unique Key ( first)   

     *如果没有1，且有uk，则为主键索引*

  3. Row ID (6 byte)     

     *如果没有pk且没有合适的uk，则Row ID为主键索引* 

  

- **辅助索引** **<index, id>**

  ​	*除了主键索引，其他的都是辅助索引。*

  

## 索引模型

#### 哈希 

*优点：适合等值查询*

*缺点：范围查询*

#### B树 vs B+树

*B+树有B树的所有特点*

*但是B+树范围查找更快，因为B树的数据存储在叶子和非叶子节点上，而B+树的数据只存储在叶子节点上，且这些叶子节点通过指针依次按顺序进行连接，所以速度特别快。所以InnoDb选择了B+树*.



##### 参考链接

1. https://dev.mysql.com/doc/refman/5.7/en/innodb-index-types.html

2. https://medium.com/@mena.meseha/what-is-the-difference-between-mysql-innodb-b-tree-index-and-hash-index-ed8f2ce66d69

3. https://draveness.me/whys-the-design-mysql-b-plus-tree/

   








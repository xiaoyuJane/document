

#### sql约束

- NOT NULL: 用于控制字段的内容一定不能为空（NULL）。
- UNIQUE: 控制字段内容不能重复，一个表允许有多个 Unique 约束。
- PRIMARY KEY: 也是用于控制字段内容不能重复，但它在一个表只允许出现一个。
- FOREIGN KEY: 用于预防破坏表之间连接的动作，也能防止非法数据插入外键列，因为它必须是它指向
  的那个表中的值之一。



#### 关联查询

1. 内连接 inner join

   > 多表中同时符合某种条件的数据记录的集合
   >
   > - 等值连接： ON A.id=B.id
   > - 不等值连接： ON A.id > B.id
   > - 自连接： SELECT * FROM A T1 INNER JOIN A T2 ON T1.id=T2.pid

2. 外连接

   > - 左外连接：LEFT OUTER JOIN, 以左表为主，先查询出左表，按照ON后的关联条件匹配右表，没有匹配到的用NULL填充，可以简写成LEFT JOIN
   > - 右外连接：RIGHT OUTER JOIN, 以右表为主，先查询出右表，按照ON后的关联条件匹配左表，没有匹配到的用NULL填充，可以简写成RIGHT JOIN

3. 联合查询

   > 把多个结果集集中在一起，UNION前的结果为基准，需要注意的是联合查询的列数要相等，相同的记录行会合并
   >
   > 如果使用UNION ALL，不会合并重复的记录行

4. 全连接 full join

   > MySQL不支持全连接
   >
   > 可以使用LEFT JOIN 和UNION和RIGHT JOIN联合使用

5. 交叉连接 cross join

   > 没有任何关联条件，结果是笛卡尔积，结果集会很大，没有意义
   >
   > select * from r,s
   >
   > 输出个数为9行5列





#### varchar 和char的区别

- char表示定长字符串，长度是固定的；如果插入数据的长度小于char的固定长度时，则用空格填充；

  - 因为长度固定，所以存取速度要比varchar快很多，甚至能快50%，但正因为其长度固定，所以会占据多余的空间，是空间换时间的做法

  - 对于char来说， 多能存放的字符个数为255，和编码无关

    

- varchar表示可变长字符串，长度是可变的，插入的数据是多长，就按照多长来存储
  - 它存取慢，因为长度不固定，但正因如此，不占据多余的空间
  - 对于varchar来说， 多能存放的字符个数为65532



注意：varchar(50)中的50含义，存放50个字符，varchar(50)和(200)存储hello所占空间一样，但排序的时候会消耗更多内存，因为order by col采用fixed_length计算col长度
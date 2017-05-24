### MySql数据库常用的命令

### 一、关于用户的操作
|命令|说明|补充说明|
|:---|:---|:---|



### 二、关于数据库
|命令|说明|代码案例|
|:-------------|:--------|:---|
|databases|查看所有的数据库|show databases|
|use|使用哪个数据库|use 数据库名称|
|database|查看当前是哪个数据库|select database()|
||创建数据库|create database 数据库名称 charset utf8|
|drop|删除数据库|drop database 数据库名称|
|drop|删除数据库|drop database 数据库名称 if exists|
||查看当前使用的那个数据库|select database()|


### 三、关于表的基本操作

|命令|说明|代码案例|
|:-------------|:--------|:---|
|create|创建表|create table 表名(列名 类型)|
|drop|删除表|drop table 表名|
|comment|描述|create table 表名(列名 类型 comment "描述内容")|
|primary key|主键||
|auto_increment|自动增长|要先设置主键|
|desc 表名|查看表结构|desc 表名|
||查看表创建结构|show create table 表名|
||查看数据库下表|show tables|
|rename|修改表名|alter table 名字1 rename to 名字2|
|modify|修改列的属性|alter table 表名 modify 列名 新类型|
||修改列名与属性|alter table 表名 change 旧列名称 新列名称 列属性|
||新增列|alter tabel 表名 add 列名 列属性|
||删除列|alter table 表名 drop 列名|
|order by 列名 asc|升序查询|select * from 表名 order by id asc|
|order by 列名 desc|降序查询|select * from 表名 order by id desc|
|limit|分页查询|select * from 表名 limit 开始位置,取几条数据|
|insert|插入数据|insert into 表名(列名1，列名2,...) values(值1，值2，值3)|
|insert|一次插入多条数据|insert into 表名(列名1，列名2,...) values(值1，值2，值3),(值1，值2，值3),(值1，值2，值3)|
|delete|删除数据|delete from 表 where 列名= 值|
|update|修改数据|update 表名 set 列名=修改的值 where 条件|
||修改自动增长的游标|alter table 表名 auto_increment = 游标值|
|通过更改来删除|删除自动增长|alter table 表名 change 旧列名 新列名 数据类型|
|通过更改来添加|添加自动增长(要在主键上)|alter table 表名 change 旧列名 新列名 数据类型 auto_increment|
|count|计数|select count(*) as "数量" from 表名|
||删除主键|alter table 表名 drop primary key|
||添加主键|alter table 表名 change 旧列 新列 类型 primary key|
||添加主键|alter table 表名 add primary key(列名1，列名2)|
|unique|添加唯一约束|创建表的时候直接在字段中添加unique|
||手动添加唯一约束|alter table 表名 add 列名 类型 unique|
||手动删除唯一约束|alter table 表名 drop index 列名|
||删除外键约束|alter table 表名 drop foreign key 约束名字|
||非空约束|not null|


### 四、表约束
* 1、主键约束
    * primary key表示主键约束，一个表中只能有一个主键，但是一个主键可以是几个字段
    * 直接创建表的时候创建主键
    * 添加主键:`alter table 表名 add primary key(字段1，字段2)`
    * 删除主键:`alter table 表名 drop primary key`
    
* 2、唯一约束
    * `unique`表示唯一，一个表中可以有多个唯一的字段，仅仅是表示该字段不能重复
    * 直接创建表的时候在字段上加上`unique`
    * 添加唯一:`alter table 表名 change 字段名 新字段名 数据类型 unique`
    * 删除唯一:`alter table 表名 drop index 列名`

* 3、外键约束一般指的是物理外键:从表中的值只能是父表已经有的值
    * 创建方式一:`foreign key(id) references 父表(id)` 表示本表中的id列与父表的id列进行外键约束
    * 创建方式二:`constraint 约束的名字 foreign key(id) references 父表(id)` 表示定义了约束的名称
    * 删除外键约束:`alter table 表名 drop foreign key 外键名称`

* 4、非空约束
    * not null

* 5、检查约束
    * `enum`的使用:使用枚举类型,只能选择里面的一个值
    * `set`的使用:使用`set`可以选择里面多个值
 
### 五、常见的查询语句
* 1、普通的查询:`select 列名1,列名2,列名3... from 表名`
* 2、普通的查询:`select 列名1,列名2,列名3... from 表名\G`
* 3、根据条件查询:`select 列名1,列名2,列名3... from 表名 where 列名 条件`
    * 条件有:=,>,< 
* 4、计算`count`:`select count(*) as 别名 from 表名 where 条件`
* 5、分组查询`group`:`select count(*) from 表名 group by 列名`
* 6、`having`是对分组后继续过滤:`select count(*) from 表名 group by 列名 having count(*) 条件5;`
* 7、分组后排序:``select count(*) from 表名 group by 列名 order by count(*) desc`
* 8、查询非空的:`select * from 表名 where 列名 is not null`
* 9、`trim`的使用:`select * from 表名 where 列名= trim(值)`
* 10、`between`查询区域范围:`select * from 表名 where 字段 between 条件1 and 条件2`
* 11、`in`的使用:`select * from 表名 where 字段 in (值1,值2);`
* 12、
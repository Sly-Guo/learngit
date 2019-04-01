# Mysql 学习笔记 task1

  

﻿

#环境: win7 64位

#参考网址：

<https://www.yiibai.com/mysql/insert-statement.html易百教程>

http://www.runoob.com/mysql/mysql-group-by-statement.html菜鸟教程

#以下所有内容主要在DOS命令窗口下完成

#注意sql语句需要；结束

  

安装完毕；

  

 **登录mysql：**

    
    
    【】mysql -h 主机名 -u 用户名 -p
    【】mysql -hlocalhost -uroot -p﻿​

注意：若mysql没有安装在C盘下，需要先使用DOS命令进入mysql的bin目录中；

如：

    
    
    cd D:\Tools\MySQL5.5.25\bin进入到mysql的bin目录

  

  

 **可视化图形工具Navicat与数据库的连接：**

由于第一次连接时出现错误：

Client does not support authentication protocol requested by server; consider
upgrading MySQL client

解决方法：在mysql命令行中输入

USE mysql;

ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '密码';
FLUSH PRIVILEGES;

  

  

 **导入数据库：**

#使用source命令导入；

#也可选用 mysql -u用户名 -p密码 < 要导入的数据库数据(yiibaidb.sql)

  

    
    
    mysql> create database yiibaidb.sql; # 创建数据库 
    mysql> use abc; # 切换至已创建的数据库 
    mysql> set names utf8; # 设置编码，注意是names
    mysql> source D:yiibaidb/yiibaidb.sql; # 数据库目录​﻿​

  

  

 **Select语句： ﻿**

使用SELECT语句从表或[视图](http://www.yiibai.com/mysql/views.html)获取数，SELECT语句的结果称为结果集，它是行列表，每行由相同数量的列组成。

1、mysql>SELECT lastname, firstname, jobtitle FROM employees;

从employees中获取所需列；

2、mysql>SELECT * FROM employees;

从employees中获取所有列；

  

  

 **WHERE 语句和HAVING语句的对比：**

having字句可以让我们筛选成组后的各种数据，where字句在聚合前先筛选记录，

也就是说作用在group by和having字句前。而 having子句在聚合后对组记录进行筛选。

  

分组后的条件使用 HAVING 来限定，WHERE 是对原始数据进行条件限制。几个关键字的使用顺序为 where 、group by
、having、order by ，例如：

    
    
    SELECT name ,sum(*) 
    FROM employee_tbl 
    WHERE id<>1 GROUP BY name HAVING sum(*)>5 ORDER BY sum(*) DESC;

 **  
**

 **Mysql注释的三种格式：**

1、单行注释可以用"#"

    
    
    show databases; #this is a comment

2、单行注释的第二种写法用 "-- " 注意这个风格下"--【空格】" 也就是说“--" 与注释之间是有空格的。

    
    
    show databases; -- this is a comment

3、多行注释可以用/**/

  

    
    
    show database; /*this
    is a 
    comment*/

 **  
**

 **项目一：**

创建 email 表

    
    
    CREATE TABLE IF NOT EXISTS email
    (Id INT UNSIGNED AUTO_INCREMENT,
    Email VARCHAR(100) NOT NULL, PRIMARY KEY(ID))
    engine=InnoDB DEFAULT CHARSET=utf8;​​

插入数据

    
    
    INSERT INTO email(email)
    VALUES("a@b.com"),
    ("c@d.com"),
    ("a@b.com");  ﻿​ 

搜索重复项

    
    
    SELECT Email from email GROUP BY Email HAVING COUNT(Email)>1; 

 结果

    
    
    +---------+
    | Email   |
    +---------+
    | a@b.com |
    +---------+ 

  

 **目二：**  

查找大国

    
    
    SELECT name,population,area FROM WORLD 
    WHERE area>3000000 OR (population>25000000 AND gdp>20000000); 

结果

    
    
    +--------------+-------------+--------------+
    | name         | population  | area         |
    +--------------+-------------+--------------+
    | Afghanistan  | 25500100    | 652230       |
    | Algeria      | 37100000    | 2381741      |
    +--------------+-------------+--------------+ 

  

中间在插入数据时可以多行插入

    
    
    INSERT INTO WORLD(name,continent,area,population,gdp)
    VALUES('Afghanistan','Asia',652230,25500100,20343000),
    ('Albania','Europe',28748,2831741,12960000),
    ('Algeria','Africa',2381741,37100000,188681000),
    ('Andorra','Europe',468,78115,3712000),
    ('Angola','Africa',1246700,20609294,100990000); 

  

由于在创建数据表时，列属性area打成了are，可以使用如下语句更改

    
    
    ALTER TABLE WORLD CHANGE are area INT NOT NULL ;﻿​

  

  

  

  

  

  

  

  

  

  

  

  

  

  

  

  

  

  

  

  

  

  

  

  

  

  

  

  

  

  

  

  

    
    
      
    


---
title: mysql常用语句
tags: [mysql]
---

### MYSQL常用命令
1. 查看数据库：show databases;
2. 选择数据库：use 数据库名;
3. 查看表：show tables; 
4. 查看表结构：desc 表名;
5. 创建表：create table 表名(字段名 字段类型, 字段名 字段类型);
6. 插入数据：insert into 表名(字段名1, 字段名2) values(值1, 值2);
7. 删除数据：delete from 表名 where 条件;
8. 更新数据：update 表名 set 字段名=新值 where 条件;
9. 查询数据：select 字段名1, 字段名2 from 表名 where 条件;
10. 排序：order by 字段名1, 字段名2;
11. 分页：limit 起始位置, 显示条数;
12. 索引：create index 索引名 on 表名(字段名);
13. 备份数据库：mysqldump -u 用户名 -p 数据库名 > 备份文件名.sql;
14. 恢复数据库：mysql -u 用户名 -p 数据库名 < 备份文件名.sql;
15. 导出数据：mysqldump -u 用户名 -p 数据库名 表名1 表名2 > 导出文件名.sql;
16. 导入数据：mysql -u 用户名 -p 数据库名 < 导入文件名.sql;
17. 导出数据：mysqldump -u 用户名 -p 数据库名 表名1 表名2 > 导出文件名.sql;
18. 导入数据：mysql -u 用户名 -p 数据库名 < 导入文件名.sql;
19. 登录mysql：mysql -u 用户名 -p;
20. 退出mysql：exit;
21. 查看当前数据库: select database();
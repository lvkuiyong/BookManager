# 图书管理系统

### 框架使用

后端：Spring 5.3.14

数据库 ORM：Mybatis  3.5.7

数据库：MySQL 5.7

Web服务器：Tomcat 9.0.76

前端：Thymeleaf  3.0.12

UI 模板：Bootstrap  

### Tomcat配置

默认URL后缀：/bookmanager/page/auth/login

默认部署：war exploded

应用程序上下文：/bookmanager

### Mybatis配置文件

DataSource @Bean根据自己情况修改RootConfiguration配置文件

```java
HikariDataSource dataSource = new HikariDataSource();
dataSource.setJdbcUrl("jdbc:mysql://localhost:3306/book_manage");
dataSource.setDriverClassName("com.mysql.cj.jdbc.Driver");
dataSource.setUsername("root");
dataSource.setPassword("123456");
```

### 数据库建立

使用MySQL

建立名为book_manage的数据库

```sql
CREATE TABLE `book` (
  `bid` int(11) NOT NULL AUTO_INCREMENT,
  `title` varchar(255) DEFAULT NULL,
  `desc` varchar(255) DEFAULT NULL,
  `isbn` int(11) DEFAULT NULL,
  PRIMARY KEY (`bid`)
);
CREATE DEFINER=`root`@`localhost` TRIGGER `del_book` BEFORE DELETE ON `book` FOR EACH ROW DELETE FROM borrow WHERE bid =old.bid;

CREATE TABLE `borrow` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `bid` int(11) DEFAULT NULL,
  `sid` int(11) DEFAULT NULL,
  `time` datetime DEFAULT NULL,
  PRIMARY KEY (`id`)
);

CREATE TABLE `student` (
  `sid` int(11) NOT NULL AUTO_INCREMENT,
  `uid` int(11) DEFAULT NULL,
  `name` varchar(255) DEFAULT NULL,
  `sex` enum('男','女') DEFAULT '男',
  `grade` varchar(255) DEFAULT NULL,
  PRIMARY KEY (`sid`),
  KEY `f_uid` (`uid`),
  CONSTRAINT `f_uid` FOREIGN KEY (`uid`) REFERENCES `users` (`id`)
);

CREATE TABLE `users` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `name` varchar(255) DEFAULT NULL,
  `role` varchar(255) DEFAULT NULL,
  `password` varchar(255) DEFAULT NULL,
  PRIMARY KEY (`id`),
  UNIQUE KEY `unique_name` (`name`)
);
```

### 界面演示

用户登录

<img src=".\pics\1.jpg" style="zoom: 50%;" />

学生注册

<img src=".\pics\2.jpg" style="zoom: 50%;" />

管理员查看借阅信息

<img src=".\pics\3.jpg" style="zoom: 50%;" />

管理员查看图书信息

<img src=".\pics\4.jpg" style="zoom: 50%;" />

管理员添加书籍

<img src=".\pics\5.jpg" style="zoom: 50%;" />

学生查看可借阅列表

<img src=".\pics\6.jpg" style="zoom: 50%;" />

学生查看已借阅列表

<img src=".\pics\7.jpg" style="zoom: 50%;" />

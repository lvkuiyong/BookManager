# JavaWeb图书管理系统

### 框架使用

后端：Java EE Servlet  5.0.0

数据库 ORM：Mybatis  3.5.7

Web服务器：Tomcat 10.1.10

前端：Thymeleaf  3.0.12

UI 模板：Bootstrap  

### Tomcat配置

默认URL：http://localhost:8080/book_manager/login

默认部署：war exploded

应用程序上下文：/book_manager

### Mybatis配置文件

根据自己情况修改

```xml
<property name="url" value="jdbc:mysql://localhost:3306/book_manage"/>
<property name="username" value="root"/>
<property name="password" value="123456"/>
```

### 数据库建立

使用MySQL

建立名为book_manage的数据库

```sql
CREATE TABLE `admin` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `username` varchar(255) DEFAULT NULL,
  `nickname` varchar(255) DEFAULT NULL,
  `password` varchar(255) DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

CREATE TABLE `student` (
  `sid` int(11) NOT NULL,
  `name` varchar(255) NOT NULL,
  `sex` enum('男','女') NOT NULL,
  `grade` int(11) NOT NULL,
  PRIMARY KEY (`sid`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

CREATE DEFINER=`root`@`localhost` TRIGGER `del` BEFORE DELETE ON `student` FOR EACH ROW DELETE FROM borrow WHERE sid = old.sid;

CREATE TABLE `book` (
  `bid` int(11) NOT NULL,
  `title` varchar(255) DEFAULT NULL,
  `desc` varchar(255) DEFAULT NULL,
  `price` decimal(10,2) DEFAULT NULL,
  PRIMARY KEY (`bid`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

CREATE DEFINER=`root`@`localhost` TRIGGER `del_book` BEFORE DELETE ON `book` FOR EACH ROW DELETE FROM borrow WHERE bid =old.bid;

CREATE TABLE `borrow` (
  `id` int(11) NOT NULL,
  `sid` int(11) DEFAULT NULL,
  `bid` int(11) DEFAULT NULL,
  PRIMARY KEY (`id`),
  UNIQUE KEY `unique_sid_bid` (`sid`,`bid`),
  KEY `f_bid` (`bid`),
  CONSTRAINT `f_bid` FOREIGN KEY (`bid`) REFERENCES `book` (`bid`),
  CONSTRAINT `f_sid` FOREIGN KEY (`sid`) REFERENCES `student` (`sid`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```


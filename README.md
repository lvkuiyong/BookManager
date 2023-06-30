# JavaWeb图书管理系统

### 框架使用

| **后端**      | **Java EE Servelt** |
| ------------- | ------------------- |
| **数据库ORM** | **Mybatis**         |
| **前端**      | **Themeleaf**       |
| **UI模板**    | **Bootstrap**       |

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


# Showplex DB Query

### Create

```mysql
CREATE SCHEMA `showplex` ;

CREATE TABLE `showplex`.`user` (
  `usernum` INT NOT NULL AUTO_INCREMENT,
  `email` VARCHAR(45) NOT NULL,
  `password` VARCHAR(45) NOT NULL,
  `username` VARCHAR(45) NULL,
  `phone` VARCHAR(45) NULL,
  `verifyNumber` VARCHAR(45) NULL,
  `verify` VARCHAR(45) NOT NULL,
  PRIMARY KEY (`usernum`));

CREATE TABLE `showplex`.`log` (
  `seq` INT NOT NULL AUTO_INCREMENT,
  `usernum` VARCHAR(45) NOT NULL,
  `country` VARCHAR(45) NULL,
  `loginTime` VARCHAR(45) NULL,
  `ip` VARCHAR(45) NULL,
  `device` VARCHAR(45) NULL,
  PRIMARY KEY (`seq`));

CREATE TABLE `showplex`.`freeboard` (
  `id` INT NOT NULL AUTO_INCREMENT,
  `title` VARCHAR(45) NOT NULL,
  `contents` VARCHAR(45) NOT NULL,
  `author` VARCHAR(45) NULL,
  `time` VARCHAR(45) NULL,
  PRIMARY KEY (`id`));
```




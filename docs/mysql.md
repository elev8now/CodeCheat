# MySQL

## Queries

### Show

The **SHOW DATABASES** statement is used to show a list of available databases.

```bash
mysql> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| scotchbox          |
| sys                |
+--------------------+
5 rows in set (0.01 sec)
```

### Use

The **USE** statement is used to select the database.

```bash
USE `scotchbox`;
```

### Create

The **CREATE TABLE** statement is used to create a new table in a database.

```bash
CREATE TABLE IF NOT EXISTS `test` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `column1` varchar(255) NOT NULL,
  `column2` varchar(255) NOT NULL,
  `column3` int(11) NOT NULL,
  `created_at` TIMESTAMP DEFAULT NOW(),
  `updated_at` TIMESTAMP DEFAULT NOW() ON UPDATE NOW(),
  PRIMARY KEY (`id`)
) ENGINE=InnoDB  DEFAULT CHARSET=latin1 AUTO_INCREMENT=6 ;
```

```bash
CREATE TABLE `users` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `email` varchar(255) NOT NULL,
  `password` varchar(255) NOT NULL,
  `activation_code` varchar(64) NOT NULL,
  `activation_state` varchar(20) NOT NULL, // pending, active, banned, deleted
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=latin1 AUTO_INCREMENT=1 ;
```

### Insert

The **INSERT INTO** statement is used to insert new records in a table.

```bash
INSERT INTO `test` (`key1`, `key2`, `key3`, `key4`) VALUES ('value1', 'value2', 'value3', 'value4');
```

```bash
INSERT INTO `users` (`email`, `password`, `activation_code`, `activation_state`) VALUES ('$clean_email', '$hashed_password', '$activation_code', 'pending');
```

### Select

The **SELECT** statement is used to select data from a database.

```bash
SELECT * FROM `table name`;

SELECT SUM(`key1`) FROM `table name` WHERE `key2` LIKE 'value%'; # key1 must be numerical data type
```

### Update

The **UPDATE** statement is used to modify the existing records in a table.

```bash
UPDATE `users` SET `activation_state` = 'active' WHERE `activation_code` = '$clean_activation_code';
```

### Truncate

The **TRUNCATE TABLE** statement is used to delete the data inside a table, but not the table itself.

```bash
TRUNCATE TABLE `table name`;
```

### Drop

The **DROP TABLE** statement is used to drop an existing table in a database (irreversible)

```bash
DROP TABLE `table name`;
```

### Describe

The **DESCRIBE** statement is used to obtain information about table structure

```bash
DESCRIBE `users`;

+------------------+--------------+------+-----+---------+----------------+
| Field            | Type         | Null | Key | Default | Extra          |
+------------------+--------------+------+-----+---------+----------------+
| id               | int(11)      | NO   | PRI | NULL    | auto_increment |
| email            | varchar(255) | NO   |     | NULL    |                |
| password         | varchar(255) | NO   |     | NULL    |                |
| activation_code  | varchar(64)  | NO   |     | NULL    |                |
| activation_state | varchar(20)  | NO   |     | NULL    |                |
+------------------+--------------+------+-----+---------+----------------+
5 rows in set (0.00 sec)
```

### Alter

The **ALTER TABLE** statement is used to add, delete, or modify columns in an existing table.

```bash
# reset auto increment `id` after deleting rows
ALTER TABLE `users` AUTO_INCREMENT = 1;
```

### Delete

The **DELETE** statement is used to delete existing records in a table.

```bash
# delete rows with id greater than 4
DELETE FROM `users` WHERE `id` > 4;
```

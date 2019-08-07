## Databases

#### Queries

#### Show

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

#### Use

```bash
mysql> USE `scotchbox`;
```

#### Create

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

#### Insert

```bash
INSERT INTO `test` (`key1`, `key2`, `key3`, `key4`) VALUES ('value1', 'value2', 'value3', 'value4');
```

#### Select

```bash
SELECT * FROM `table name`;

SELECT SUM(`key1`) FROM `table name` WHERE `key2` LIKE 'value%'; # key1 must be numerical data type
```

#### Update

#### Truncate

[More info](https://dev.mysql.com/doc/refman/8.0/en/truncate-table.html)

```bash
mysql> TRUNCATE TABLE `table name`;
```

#### Drop

[More info](https://dev.mysql.com/doc/refman/8.0/en/drop-table.html)

```bash
mysql> DROP TABLE `table name`;
```

#### Describe

#### Alter

#### Delete

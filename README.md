# Linuxv3
## Linux. Конспект по курсу LPIC 105.3.
## Часть 1. Установка и создания MySQL
Чтобы начать пользоваться MySql, нужно его установить:
```bash
apt-get install mysql
///или просто 
apt install mysql
///если не установится, то нужно написать 
apt-get install mysql --fix-missing
///или
apt install mysql --fix-missing
```
Чтобы создать базу данных, нужно написать :
```sql
CREATE DATABASE database; ///создаем базу данных с именем database
```
Чтобы использовать Базу Данных, нужно написать:
```sql
USE database; ///database-имя нашей бд, которой хотим подключиться
```
Базы данных-это наборы таблиц, поэтому нужно научиться создавать таблицы.
Итак, чтобы создать таблицу, нужно написать:
```sql
CREATE TABLE new ( /// где new - Название нашей таблицы, а открытая скобка - место для полей таблицы, разных типов.
nick VARCHAR(10), /// где nick - имя переменной,а varchar - символьный тип данных с длиной указанной в скобках то есть 10 символов.
year YEAR, ///где year - имя переменной, а YEAR - Тип данных года в MYSQL
cost INT(7) ///где cost - имя переменной, а INT - целочисленный тип данных с длиной в скобках 7
); ///закрываем таблицу скобкой и обязательно Точкой с запятой
```
Все. Таблица создана.
Чтобы посмотреть все таблицы в базе данных, нужно написать 
```sql
SHOW TABLES;
+---------------------+
| Tables_in_database  |
+---------------------+
| new                 |
+---------------------+
1 rows in set (0.00 sec)
```
Мы можем посмотреть структуру этих таблиц. Для этого есть команда:
```sql
DESCRIBE new;
+-------+------------------+------+-----+---------+-------+
| Field | Type             | Null | Key | Default | Extra |
+-------+------------------+------+-----+---------+-------+
| nick  | varchar(10)      | Yes  |     | NULL    |       |
| year  | year(4)          | Yes  |     | NULL    |       |
| cost  | int(7)           | Yes  |     | NULL    |       |
+-------+------------------+------+-----+---------+-------+
3 rows in set(0.00 sec)
```
## Часть 2. Заполнение таблицы MYSQL данными.
Итак. Мы можем заполнить таблица из файла.
Через echo создадим файл с данными.
```bash
echo 'user  2020  35'>file.txt
echo 'kelv  2001  41'>>file.txt
echo 'some  2019  31'>>file.txt
```
Теперь нужно разрешить импорт из файла, поскольку по умолчанию, в MYSQL данная функция выключена.
Включаем функцию в консоли линукса вот так:
```bash
sudo mysql --local-infile=1 -u root ///root - пользователь с которого включается эта функция. 1 или 0 - значение вкл или вкл  
```
Дальше запуститься Mysql в режиме вставки данных из файла
Следовательно чтобы импортировать файл нужно написать:
```sql
USE new;
LOAD DATA LOCAL INFILE "file.txt" INTO TABLE new;
Query OK, 3 rows affected (0.01 sec) ///Выдаст вот этот результат.
Records: 3  Deleted: 0  Skipped: 0  Warnings: 0
```
Посмотреть все значения в таблице можно так:
```sql
SELECT * FROM new;
+--------+--------+-------+
| nick   | year   | cost  |
+--------+--------+-------+
| user   | 2020   | 35    |
| kelv   | 2001   | 41    |
| some   | 2019   | 31    |
+--------+--------+-------+
```
Теперь рассмотрим как можно добавить данные вручную.
Чтобы ввесть данные вручную, нужно написать:
```sql
INSERT INTO new (nick, year, cost) VALUES ('lolik', '2020', '67');
Query OK, 1 rows affected (0.01 sec)
```
Переменные (nick, year, cost) можно использовать в каком угодно порядке:
```
(nick, cost, year), но заполнять значения нужно в соотсветствии с порядком.
```
Рассмотрим удаление в MYSQL
Чтобы удалить какие-то значения, нужно написать:
```sql
DELETE FROM new WHERE nick='kelv' ///Удаляем все из таблицы New, где nick='kelv'
```
## Часть 3. Получение данных из MYSQL


#### ©Copyright Cloud App Storage
#### Информация, предоставленная на данной странице не разрешена к распространению без ведома создателя.

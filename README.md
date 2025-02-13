# Домашнее задание к занятию "`SQL`" - `Татаринйев Алексей`

По ссылке https://downloads.mysql.com/docs/sakila-db.zip скачайте дамп базы данных. 

---

### Задание 1


1. `Подключаюсь к уже развернутой с прошлого задания базе под пользователем sys_temp с паролем  password`

```
mysql -u sys_temp -p
```
![0](https://github.com/Foxbeerxxx/SQL1/blob/main/img/img0.png)`

2. `Указываю,что работаю с БД sakila`

```
 USE sakila; 
```
3. `Думаю....и формирую запрос по заданию 1`
```
SELECT DISTINCT district
FROM address
WHERE district LIKE 'K%a'
 AND district NOT LIKE '% %';
```   
`приходит ответ `
```
+-----------+
| district  |
+-----------+
| Kanagawa  |
| Kalmykia  |
| Kaduna    |
| Karnataka |
| Kütahya   |
| Kerala    |
| Kitaa     |
+-----------+
7 rows in set (0,00 sec)
```



---

### Задание 2



1. `Получите из таблицы платежей за прокат фильмов информацию по платежам, которые выполнялись в промежуток с 15 июня 2005 года по 18 июня 2005 года включительно и стоимость которых превышает 10.00.`

2. `Формирую запрос в базу данных`
```
SELECT *
FROM payment
WHERE payment_date BETWEEN '2005-06-15 00:00:00' AND '2005-06-18 23:59:59'
  AND amount > 10.00;

```
![2](https://github.com/Foxbeerxxx/SQL1/blob/main/img/img2.png)`

---

### Задание 3


1. `Получите последние пять аренд фильмов.`

2. `Формирую запрос к базе данных`
```
SELECT *
FROM rental
ORDER BY rental_date DESC, rental_id DESC
LIMIT 5;

```

```
+-----------+---------------------+--------------+-------------+-------------+----------+---------------------+
| rental_id | rental_date         | inventory_id | customer_id | return_date | staff_id | last_update         |
+-----------+---------------------+--------------+-------------+-------------+----------+---------------------+
|     15966 | 2006-02-14 15:16:03 |         4472 |         374 | NULL        |        1 | 2006-02-15 21:30:53 |
|     15894 | 2006-02-14 15:16:03 |         4416 |         168 | NULL        |        1 | 2006-02-15 21:30:53 |
|     15875 | 2006-02-14 15:16:03 |         3611 |          41 | NULL        |        1 | 2006-02-15 21:30:53 |
|     15867 | 2006-02-14 15:16:03 |          837 |         505 | NULL        |        2 | 2006-02-15 21:30:53 |
|     15862 | 2006-02-14 15:16:03 |          925 |         215 | NULL        |        1 | 2006-02-15 21:30:53 |
+-----------+---------------------+--------------+-------------+-------------+----------+---------------------+
5 rows in set (0,01 sec)

```
![3](https://github.com/Foxbeerxxx/SQL1/blob/main/img/img3.png)`



### Задание 4



1. `Одним запросом получите активных покупателей, имена которых Kelly или Willie.`

`Сформируйте вывод в результат таким образом:`
`- все буквы в фамилии и имени из верхнего регистра переведите в нижний регистр,`
`- замените буквы 'll' в именах на 'pp'.`

2. `Формирую запрос в базу данных`

```
SELECT
    LOWER(REPLACE(REPLACE(first_name, 'Kelly', 'Keppy'), 'Willie', 'Wippie')) AS first_name_modified,
    LOWER(last_name) AS last_name_lowercase,
    active
FROM
    customer
WHERE
    active = 1
    AND (first_name = 'Kelly' OR first_name = 'Willie');


```
![4](https://github.com/Foxbeerxxx/SQL1/blob/main/img/img4.png)`



3. `для замены буквы 'll' в именах на 'pp'`
```
SELECT
    LOWER(REPLACE(first_name, 'll', 'pp')) AS first_name_modified,
    LOWER(last_name) AS last_name_lowercase,
    active
FROM
    customer
WHERE
    active = 1
    AND (first_name = 'Kelly' OR first_name = 'Willie');
```

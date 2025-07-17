Домашнее задание к занятию «Работа с данными (DDL/DML)»

Задание 1
1.1. Поднимите чистый инстанс MySQL версии 8.0+. Можно использовать локальный сервер или контейнер Docker.

1.2. Создайте учётную запись sys_temp.

1.3. Выполните запрос на получение списка пользователей в базе данных. (скриншот)<img width="1718" height="1048" alt="1-3" src="https://github.com/user-attachments/assets/0595e71c-9955-4077-9994-8c7d5bfe7658" />


1.4. Дайте все права для пользователя sys_temp.

1.5. Выполните запрос на получение списка прав для пользователя sys_temp. (скриншот)<img width="1718" height="1048" alt="1-5" src="https://github.com/user-attachments/assets/2eefe183-f3f7-43c0-ba76-cd28c4f0d589" />


1.6. Переподключитесь к базе данных от имени sys_temp.

Для смены типа аутентификации с sha2 используйте запрос:

ALTER USER 'sys_test'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
1.6. По ссылке https://downloads.mysql.com/docs/sakila-db.zip скачайте дамп базы данных.

1.7. Восстановите дамп в базу данных.

1.8. При работе в IDE сформируйте ER-диаграмму получившейся базы данных. При работе в командной строке используйте команду для получения всех таблиц базы данных. (скриншот)<img width="1718" height="1048" alt="1-8" src="https://github.com/user-attachments/assets/acb0622c-475b-4163-81c7-2666d92f77cc" />


Результатом работы должны быть скриншоты обозначенных заданий, а также простыня со всеми запросами.

Команды:
docker run --name mysql8-test -e MYSQL_ROOT_PASSWORD=root -p 3306:3306 -d mysql:8
docker exec -it mysql8-test mysql -uroot -proot

CREATE USER 'sys_temp'@'localhost' IDENTIFIED BY 'P@ssw0rd';
SELECT User, Host FROM mysql.user;
GRANT ALL PRIVILEGES ON *.* TO 'sys_temp'@'localhost' WITH GRANT OPTION;
SHOW GRANTS FOR 'sys_temp'@'localhost';

docker exec -it mysql8-test mysql -usys_temp -pP@ssw0rd
ALTER USER 'sys_temp'@'localhost'
  IDENTIFIED WITH mysql_native_password BY 'P@ssw0rd';
docker exec -it mysql8-test mysql -usys_temp -pP@ssw0rd
docker cp sakila-schema.sql mysql8-test:/sakila-schema.sql
docker cp sakila-data.sql mysql8-test:/sakila-data.sql
docker exec -it mysql8-test bash
mysql -uroot -proot -e "CREATE DATABASE sakila;"
mysql -uroot -proot sakila < /sakila-schema.sql
mysql -uroot -proot sakila < /sakila-data.sql
mysql -usys_temp -pP@ssw0rd sakila
SHOW TABLES;


Задание 2
Составьте таблицу, используя любой текстовый редактор или Excel, в которой должно быть два столбца: в первом должны быть названия таблиц восстановленной базы, во втором названия первичных ключей этих таблиц. Пример: (скриншот/текст)

Название таблицы | Название первичного ключа
customer         | customer_id

Решение:
+---------------+--------------+
| TABLE_NAME    | COLUMN_NAME  |
+---------------+--------------+
| actor         | actor_id     |
| address       | address_id   |
| category      | category_id  |
| city          | city_id      |
| country       | country_id   |
| customer      | customer_id  |
| film          | film_id      |
| film_actor    | actor_id     |
| film_actor    | film_id      |
| film_category | film_id      |
| film_category | category_id  |
| film_text     | film_id      |
| inventory     | inventory_id |
| language      | language_id  |
| payment       | payment_id   |
| rental        | rental_id    |
| staff         | staff_id     |
| store         | store_id     |
+---------------+--------------+

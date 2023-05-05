# SQL-Academy-Solved-Exercises

Решенные мной задачи с сайта https://sql-academy.org/ru

### [Задание 1](https://sql-academy.org/ru/trainer/tasks/1)
Вывести имена всех людей, которые есть в базе данных авиакомпаний. Поля в результирующей таблице: name

```sql
SELECT name
FROM Passenger
```

### [Задание 2](https://sql-academy.org/ru/trainer/tasks/2)
Вывести названия всеx авиакомпаний. Поля в результирующей таблице: name

```sql
SELECT name
FROM Company
```

### [Задание 3](https://sql-academy.org/ru/trainer/tasks/3)
Вывести все рейсы, совершенные из Москвы. Поля в результирующей таблице: *

```sql
SELECT *
FROM Trip
WHERE town_from = 'Moscow'
```

### [Задание 4](https://sql-academy.org/ru/trainer/tasks/4)
Вывести имена людей, которые заканчиваются на "man". Поля в результирующей таблице: name

```sql
SELECT name
FROM Passenger
WHERE name LIKE '%man'
```

### [Задание 5](https://sql-academy.org/ru/trainer/tasks/5)
Вывести количество рейсов, совершенных на TU-134. Поля в результирующей таблице: count.

Используйте конструкцию "as count" для агрегатной функции подсчета количества рейсов. Это необходимо для корректной проверки.

```sql
SELECT COUNT(*) as count
FROM Trip
WHERE plane = 'TU-134'
```

### [Задание 6](https://sql-academy.org/ru/trainer/tasks/6)
Какие компании совершали перелеты на Boeing. Поля в результирующей таблице: name

```sql
SELECT DISTINCT Company.name
FROM Trip JOIN Company
ON Trip.company = Company.id
WHERE Trip.plane = 'Boeing'
```

### [Задание 7](https://sql-academy.org/ru/trainer/tasks/7)
Вывести все названия самолётов, на которых можно улететь в Москву (Moscow). Поля в результирующей таблице: plane

```sql
SELECT DISTINCT plane
FROM Trip
WHERE town_to = 'Moscow'
```

### [Задание 8](https://sql-academy.org/ru/trainer/tasks/8)
В какие города можно улететь из Парижа (Paris) и сколько времени это займёт? Поля в результирующей таблице: town_to, flight_time

Используйте конструкцию "as flight_time" для вывода необходимого времени. Это необходимо для корректной проверки. Формат для вывода времени: HH:MM:SS

```sql
SELECT town_to, TIMEDIFF(time_in, time_out) as flight_time
FROM Trip
WHERE town_from = 'Paris'
```

### [Задание 9](https://sql-academy.org/ru/trainer/tasks/9)
Какие компании организуют перелеты из Владивостока (Vladivostok)? Поля в результирующей таблице: name

```sql
SELECT DISTINCT Company.name
FROM Trip JOIN Company
ON Trip.company = Company.id
WHERE town_from = 'Vladivostok'
```

### [Задание 10](https://sql-academy.org/ru/trainer/tasks/10)
Вывести вылеты, совершенные с 10 ч. по 14 ч. 1 января 1900 г. Поля в результирующей таблице: *

```sql
SELECT *
FROM Trip
WHERE time_out BETWEEN '1900-01-01T10:00:00'
AND '1900-01-01T14:00:00'
```

### [Задание 11](https://sql-academy.org/ru/trainer/tasks/11)
Вывести пассажиров с самым длинным именем. Поля в результирующей таблице: name

```sql
SELECT name
FROM Passenger
WHERE LENGTH(name) = (
		SELECT max(LENGTH(name))
		FROM Passenger
	)
```

### [Задание 12](https://sql-academy.org/ru/trainer/tasks/12)
Вывести id и количество пассажиров для всех прошедших полётов. Поля в результирующей таблице: trip, count

```sql
SELECT Trip.id as trip, count(*) as count
FROM Trip JOIN Pass_in_trip
ON Trip.id = Pass_in_trip.trip
GROUP BY Trip.id
```

### [Задание 13](https://sql-academy.org/ru/trainer/tasks/13)
Вывести имена людей, у которых есть полный тёзка среди пассажиров. Поля в результирующей таблице: name

```sql
SELECT name
FROM Passenger
GROUP BY name
HAVING count(*) >= 2
```

### [Задание 14](https://sql-academy.org/ru/trainer/tasks/14)
В какие города летал Bruce Willis. Поля в результирующей таблице: town_to

```sql
SELECT DISTINCT Trip.town_to
FROM Trip
	JOIN Pass_in_trip ON Trip.id = Pass_in_trip.trip)
	JOIN Passenger ON Pass_in_trip.passenger = Passenger.id
WHERE Passenger.name = 'Bruce Willis'
```

### [Задание 15](https://sql-academy.org/ru/trainer/tasks/15)
Выведите дату и время прилёта пассажира Стив Мартин (Steve Martin) в Лондон (London). Поля в результирующей таблице: time_in

```sql
SELECT Trip.time_in
FROM Trip
	JOIN Pass_in_trip ON Trip.id = Pass_in_trip.trip)
	JOIN Passenger ON Pass_in_trip.passenger = Passenger.id
WHERE Passenger.name = 'Steve Martin'
AND Trip.town_to = 'London'
```

### [Задание 16](https://sql-academy.org/ru/trainer/tasks/16)
Вывести отсортированный по количеству перелетов (по убыванию) и имени (по возрастанию) список пассажиров, совершивших хотя бы 1 полет. Поля в результирующей таблице: name, count

```sql
SELECT Passenger.name, count(Pass_in_trip.id) as count
FROM Trip
	JOIN Pass_in_trip ON Trip.id = Pass_in_trip.trip)
	JOIN Passenger ON Pass_in_trip.passenger = Passenger.id
GROUP BY Passenger.name
HAVING count(Pass_in_trip.id) >= 1
ORDER BY count(Pass_in_trip.id) DESC, name
```

### [Задание 17](https://sql-academy.org/ru/trainer/tasks/17)
Определить, сколько потратил в 2005 году каждый из членов семьи. В результирующей выборке не выводите тех членов семьи, которые ничего не потратили. Поля в результирующей таблице: member_name, status, costs

```sql
SELECT FamilyMembers.member_name,
	FamilyMembers.status,
	SUM(Payments.amount * Payments.unit_price) as costs
FROM FamilyMembers JOIN Payments
ON member_id = family_member
WHERE YEAR(Payments.date) = 2005
GROUP BY FamilyMembers.member_name, FamilyMembers.status
```

### [Задание 18](https://sql-academy.org/ru/trainer/tasks/18)
Узнать, кто старше всех в семьe. Поля в результирующей таблице: member_name

```sql
SELECT member_name
FROM FamilyMembers
ORDER BY birthday
LIMIT 1
```

### [Задание 19](https://sql-academy.org/ru/trainer/tasks/19)
Определить, кто из членов семьи покупал картошку (potato). Поля в результирующей таблице: status

```sql
SELECT DISTINCT status
FROM FamilyMembers
	JOIN Payments ON member_id = family_member
	JOIN Goods ON good = good_id
WHERE good_name = 'potato'
```

### [Задание 20](https://sql-academy.org/ru/trainer/tasks/20)
Сколько и кто из семьи потратил на развлечения (entertainment). Вывести статус в семье, имя, сумму. Поля в результирующей таблице: status, member_name, costs

```sql
SELECT status, member_name,
	SUM(amount * unit_price) as costs
FROM FamilyMembers
	JOIN Payments ON member_id = family_member
	JOIN Goods ON good = good_id
	JOIN GoodTypes ON type = good_type_id
WHERE good_type_name = 'entertainment'
GROUP BY status, member_name
```

### [Задание 21](https://sql-academy.org/ru/trainer/tasks/21)
Определить товары, которые покупали более 1 раза. Поля в результирующей таблице: good_name

```sql
SELECT good_name
FROM Payments JOIN Goods ON good = good_id
GROUP BY good_name
HAVING count(*) > 1
```

### [Задание 22](https://sql-academy.org/ru/trainer/tasks/22)
Найти имена всех матерей (mother). Поля в результирующей таблице: member_name

```sql
SELECT member_name
FROM FamilyMembers
WHERE status = 'mother'
```

### [Задание 23](https://sql-academy.org/ru/trainer/tasks/23)
Найдите самый дорогой деликатес (delicacies) и выведите его цену. Поля в результирующей таблице: good_name, unit_price

```sql
SELECT good_name, unit_price
FROM Payments JOIN Goods ON good = good_id
WHERE unit_price = (
		SELECT MAX(unit_price)
		FROM Payments
			JOIN Goods ON good = good_id
			JOIN GoodTypes ON type = good_type_id
		WHERE good_type_name = 'delicacies'
	)
```

### [Задание 24](https://sql-academy.org/ru/trainer/tasks/24)
Определить кто и сколько потратил в июне 2005. Поля в результирующей таблице: member_name, costs

```sql
SELECT member_name, SUM(amount * unit_price) as costs
FROM FamilyMembers JOIN Payments
ON member_id = family_member
WHERE date LIKE '2005-06%'
GROUP BY member_name
```

### [Задание 25](https://sql-academy.org/ru/trainer/tasks/25)
Определить, какие товары не покупались в 2005 году. Поля в результирующей таблице: good_name

```sql
SELECT DISTINCT good_name
FROM Goods
WHERE good_name NOT IN (
		SELECT good_name
		FROM Payments
			JOIN Goods ON good = good_id
		WHERE date LIKE '2005%'
	)
```

### [Задание 26](https://sql-academy.org/ru/trainer/tasks/26)
Определить группы товаров, которые не приобретались в 2005 году. Поля в результирующей таблице: good_type_name

```sql
SELECT DISTINCT good_type_name
FROM GoodTypes
WHERE good_type_name NOT IN (
		SELECT DISTINCT good_type_name
		FROM Payments
			JOIN Goods ON good = good_id
			JOIN GoodTypes ON good_type_id = type
		WHERE date LIKE '2005%'
	)
```

### [Задание 27](https://sql-academy.org/ru/trainer/tasks/27)
Определить кто и сколько потратил в июне 2005. Поля в результирующей таблице: member_name, costs

```sql
SELECT good_type_name, SUM(amount * unit_price) AS costs
FROM Payments, Goods, GoodTypes
WHERE good = good_id
	AND type = good_type_id
	AND date LIKE '2005%'
GROUP BY good_type_name
```

### [Задание 28](https://sql-academy.org/ru/trainer/tasks/28)
Сколько рейсов совершили авиакомпании из Ростова (Rostov) в Москву (Moscow)? Поля в результирующей таблице: count

```sql
SELECT COUNT(*) AS count
FROM Trip
WHERE town_from = 'Rostov'
	AND town_to = 'Moscow'
```

### [Задание 29](https://sql-academy.org/ru/trainer/tasks/29)
Выведите имена пассажиров улетевших в Москву (Moscow) на самолете TU-134. Поля в результирующей таблице: name

```sql
SELECT DISTINCT name
FROM Trip, Pass_in_trip, Passenger
WHERE Trip.id = trip
	AND passenger = Passenger.id
	AND town_to = 'Moscow'
	AND plane = 'TU-134'
```

### [Задание 30](https://sql-academy.org/ru/trainer/tasks/30)
Выведите нагруженность (число пассажиров) каждого рейса (trip). Результат вывести в отсортированном виде по убыванию нагруженности. Поля в результирующей таблице: trip, count

```sql
SELECT Trip.id AS trip, COUNT(*) AS count
FROM Trip, Pass_in_trip
WHERE Trip.id = Pass_in_trip.trip
GROUP BY Trip.id
ORDER BY count DESC
```

### [Задание 31](https://sql-academy.org/ru/trainer/tasks/31)
Вывести всех членов семьи с фамилией Quincey. Поля в результирующей таблице: *

```sql
SELECT *
FROM FamilyMembers
WHERE member_name LIKE '%Quincey'
```

### [Задание 32](https://sql-academy.org/ru/trainer/tasks/32)
Вывести средний возраст людей (в годах), хранящихся в базе данных. Результат округлите до целого в меньшую сторону. Поля в результирующей таблице: age

```sql
SELECT ROUND(AVG(TIMESTAMPDIFF(YEAR, birthday, NOW()))) AS age
FROM FamilyMembers
```

### [Задание 33](https://sql-academy.org/ru/trainer/tasks/33)
Найдите среднюю стоимость икры. В базе данных хранятся данные о покупках красной (red caviar) и черной икры (black caviar). Поля в результирующей таблице: cost

```sql
SELECT AVG(unit_price) AS cost
FROM Payments, Goods
WHERE good = good_id
	AND good_name IN ('red caviar', 'black caviar')
```

### [Задание 34](https://sql-academy.org/ru/trainer/tasks/34)
Сколько всего 10-ых классов. Поля в результирующей таблице: count

```sql
SELECT COUNT(*) AS count
FROM Class
WHERE name LIKE "10%"
```

### [Задание 35](https://sql-academy.org/ru/trainer/tasks/35)
Сколько различных кабинетов школы использовались 2.09.2019 в образовательных целях? Поля в результирующей таблице: count

```sql
SELECT COUNT(DISTINCT classroom) AS count
FROM Schedule
WHERE date LIKE "2019-09-02%"
```

### [Задание 36](https://sql-academy.org/ru/trainer/tasks/36)
Выведите информацию об обучающихся живущих на улице Пушкина (ul. Pushkina)? Поля в результирующей таблице: *

```sql
SELECT *
FROM Student
WHERE address LIKE 'ul. Pushkina%'
```

### [Задание 37](https://sql-academy.org/ru/trainer/tasks/37)
Сколько лет самому молодому обучающемуся? Поля в результирующей таблице: year

```sql
SELECT TIMESTAMPDIFF(YEAR, MAX(birthday), NOW()) AS year
FROM Student
```

### [Задание 38](https://sql-academy.org/ru/trainer/tasks/38)
Сколько Анн (Anna) учится в школе? Поля в результирующей таблице: count

```sql
SELECT COUNT(*) AS count
FROM Student
WHERE first_name = 'Anna'
```

### [Задание 39](https://sql-academy.org/ru/trainer/tasks/39)
Сколько обучающихся в 10 B классе? Поля в результирующей таблице: count

```sql
SELECT COUNT(*) AS count
FROM Class, Student_in_class
WHERE Class.id = Student_in_class.class
	AND Class.name = '10 B'
```

### [Задание 40](https://sql-academy.org/ru/trainer/tasks/40)
Выведите название предметов, которые преподает Ромашкин П.П. (Romashkin P.P.)? Поля в результирующей таблице: subjects

```sql
SELECT DISTINCT Subject.name AS subjects
FROM Teacher, Schedule, Subject
WHERE Teacher.id = Schedule.teacher
	AND Schedule.subject = Subject.id
	AND Teacher.last_name = 'Romashkin'
```

### [Задание 41](https://sql-academy.org/ru/trainer/tasks/41)
Во сколько начинается 4-ый учебный предмет по расписанию? Поля в результирующей таблице: start_pair

```sql
SELECT start_pair
FROM Timepair
WHERE id = 4
```

### [Задание 42](https://sql-academy.org/ru/trainer/tasks/42)
Сколько времени обучающийся будет находиться в школе, учась со 2-го по 4-ый уч. предмет? Поля в результирующей таблице: time

```sql
SELECT TIMEDIFF(
		(
			SELECT end_pair
			FROM Timepair
			WHERE id = 4
		),
		(
			SELECT start_pair
			FROM Timepair
			WHERE id = 2
		)
	) AS time
```

### [Задание 43](https://sql-academy.org/ru/trainer/tasks/43)
Выведите фамилии преподавателей, которые ведут физическую культуру (Physical Culture). Отcортируйте преподавателей по фамилии. Поля в результирующей таблице: last_name

```sql
SELECT DISTINCT Teacher.last_name
FROM Teacher, Schedule, Subject
WHERE Teacher.id = Schedule.teacher
	AND Schedule.subject = Subject.id
	AND Subject.name = 'Physical Culture'
ORDER BY Teacher.last_name
```

### [Задание 44](https://sql-academy.org/ru/trainer/tasks/44)
Найдите максимальный возраст (колич. лет) среди обучающихся 10 классов? Поля в результирующей таблице: max_year

```sql
SELECT MAX(2022 - YEAR(Student.birthday)) AS max_year
FROM Class, Student_in_class, Student
WHERE Class.id = Student_in_class.class
	AND Student_in_class.student = Student.id
	AND Class.name LIKE '10%'
```

### [Задание 45](https://sql-academy.org/ru/trainer/tasks/45)
Какие кабинеты чаще всего использовались для проведения занятий? Выведите те, которые использовались максимальное количество раз. Поля в результирующей таблице: classroom

```sql
WITH t AS (
	SELECT classroom,
		count(*) AS counts,
		max(count(*)) OVER() AS max_counts
	FROM Schedule
	GROUP BY classroom
	ORDER BY counts DESC
)
SELECT classroom
FROM t
WHERE counts = max_counts
```

### [Задание 46](https://sql-academy.org/ru/trainer/tasks/46)
В каких классах введет занятия преподаватель "Krauze"? Поля в результирующей таблице: name

```sql
SELECT DISTINCT name
FROM Class, Schedule, Teacher
WHERE Class.id = Schedule.class
	AND Schedule.teacher = Teacher.id
	AND last_name = 'Krauze'
```

### [Задание 47](https://sql-academy.org/ru/trainer/tasks/47)
Сколько занятий провел Krauze 30 августа 2019 г.? Поля в результирующей таблице: count

```sql
SELECT COUNT(*) AS count
FROM Teacher, Schedule
WHERE Teacher.id = Schedule.teacher
	AND Teacher.last_name = 'Krauze'
	AND Schedule.date LIKE '2019-08-30%'
```

### [Задание 48](https://sql-academy.org/ru/trainer/tasks/48)
Выведите заполненность классов в порядке убывания. Поля в результирующей таблице: name, count

```sql
SELECT Class.name, COUNT(Student_in_class.student) as count
FROM Class JOIN Student_in_class
ON Class.id = Student_in_class.class
GROUP BY Class.name
ORDER BY count DESC
```

### [Задание 49](https://sql-academy.org/ru/trainer/tasks/49)
Какой процент обучающихся учится в 10 A классе? Поля в результирующей таблице: percent

```sql
SELECT (
		SELECT COUNT(*)
		FROM Class,
			Student_in_class,
			Student
		WHERE Class.id = Student_in_class.class
			AND Student_in_class.student = Student.id
			AND Class.name = '10 A'
	) /(
		SELECT COUNT(*)
		FROM Student
	) * 100 as percent
```

### [Задание 50](https://sql-academy.org/ru/trainer/tasks/50)
Какой процент обучающихся родился в 2000 году? Результат округлить до целого в меньшую сторону. Поля в результирующей таблице: percent

```sql
SELECT ROUND(
		(
			SELECT COUNT(*)
			FROM Student
			WHERE YEAR(birthday) = 2000
		) /(
			SELECT COUNT(*)
			FROM Student
		) * 100,
		0
	) as percent
```

### [Задание 51](https://sql-academy.org/ru/trainer/tasks/51)
Добавьте товар с именем "Cheese" и типом "food" в список товаров (Goods).

```sql
INSERT INTO Goods (good_id, good_name, type)
SELECT MAX(good_id) + 1,
	"Cheese",
	(
		SELECT DISTINCT type
		FROM Goods,
			GoodTypes
		WHERE good_type_id = type
			AND good_type_name = "food"
	)
FROM Goods
```

### [Задание 52](https://sql-academy.org/ru/trainer/tasks/52)
Добавьте в список типов товаров (GoodTypes) новый тип "auto".

```sql
INSERT into GoodTypes (good_type_id, good_type_name)
SELECT MAX(good_type_id) + 1,
	'auto'
FROM GoodTypes
```

### [Задание 53](https://sql-academy.org/ru/trainer/tasks/53)
Измените имя "Andie Quincey" на новое "Andie Anthony".

```sql
UPDATE FamilyMembers
SET member_name = 'Andie Anthony'
WHERE member_name = 'Andie Quincey'
```

### [Задание 54](https://sql-academy.org/ru/trainer/tasks/54)
Удалить всех членов семьи с фамилией "Quincey".

```sql
DELETE FROM FamilyMembers
WHERE member_name LIKE '% Quincey'
```

### [Задание 55](https://sql-academy.org/ru/trainer/tasks/55)
Удалить компании, совершившие наименьшее количество рейсов.

```sql

MySQL

DELETE FROM Company
WHERE id IN (
		SELECT company
		FROM Trip
		GROUP BY company
		HAVING COUNT(1) = (
				SELECT COUNT(1) as count
				FROM Trip as t
				GROUP BY company
				ORDER BY count
				LIMIT 1
			)
	)
```

### [Задание 56](https://sql-academy.org/ru/trainer/tasks/56)
Удалить все перелеты, совершенные из Москвы (Moscow).

```sql
DELETE FROM Trip
WHERE town_from = 'Moscow'
```

### [Задание 57](https://sql-academy.org/ru/trainer/tasks/57)
Перенести расписание всех занятий на 30 мин. вперед.

```sql
UPDATE Timepair
SET start_pair = TIMESTAMPADD(MINUTE, 30, start_pair),
	end_pair = TIMESTAMPADD(MINUTE, 30, end_pair)
```

### [Задание 58](https://sql-academy.org/ru/trainer/tasks/58)
Добавить отзыв с рейтингом 5 на жилье, находящиеся по адресу "11218, Friel Place, New York", от имени "George Clooney"

```sql
INSERT INTO Reviews (id, reservation_id, rating)
VALUES (
		(
			SELECT MAX(id) + 1
			FROM Reviews as r
		),
		(
			SELECT Reservations.id
			FROM Users
				JOIN Reservations ON Users.id = Reservations.user_id
				JOIN Rooms ON Reservations.room_id = Rooms.id
			WHERE Rooms.address = "11218, Friel Place, New York"
				AND Users.name = "George Clooney"
		),
		5
	)
```

### [Задание 59](https://sql-academy.org/ru/trainer/tasks/59)
Вывести пользователей,указавших Белорусский номер телефона ? Телефонный код Белоруссии +375. Поля в результирующей таблице: *

```sql
SELECT *
FROM Users
WHERE phone_number LIKE '+375%'
```

### [Задание 60](https://sql-academy.org/ru/trainer/tasks/60)
Выведите идентификаторы преподавателей, которые хотя бы один раз за всё время преподавали в каждом из одиннадцатых классов. Поля в результирующей таблице: teacher

```sql
SELECT Teacher.id as teacher
FROM Teacher
	JOIN Schedule ON Teacher.id = Schedule.teacher
	JOIN Class ON Schedule.class = Class.id
WHERE Class.name IN (
		SELECT name
		FROM Class
		WHERE name LIKE "11%"
	)
GROUP BY Teacher.id
HAVING COUNT(DISTINCT Class.name) = (
		SELECT COUNT(name)
		FROM Class
		WHERE name LIKE "11%"
	)
```










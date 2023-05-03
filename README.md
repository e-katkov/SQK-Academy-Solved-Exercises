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



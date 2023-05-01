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



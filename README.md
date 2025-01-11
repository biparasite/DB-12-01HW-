# Домашнее задание к занятию " `Базы данных` " - `Сулименков Алексей`

---

## Задание 1

Опишите не менее семи таблиц, из которых состоит база данных:

какие данные хранятся в этих таблицах;
какой тип данных у столбцов в этих таблицах, если данные хранятся в PostgreSQL.
Приведите решение к следующему виду:

Сотрудники (

- идентификатор, первичный ключ, serial,
- фамилия varchar(50),
  ...
- идентификатор структурного подразделения, внешний ключ, integer).

### Ответ

```PostgreSQL
-- Офисы
create table branches(
    id int primary key,
    address_branche  varchar(255) not null unique
);
```

```PostgreSQL
-- Структурное подразделение
create table structural_unit (
    id int primary key,
    name_structural_unit varchar(128) not null,
    branche int,
    foreign key(branche) references branches (id)
);
```

```PostgreSQL
-- Тип подразделения
create table units_type(
    id int primary key,
    name_units_type varchar(128) not null,
    structural int,
    foreign key(structural) references structural_unit (id)
);
```

```PostgreSQL
-- Должность
create table job_title(
    id int primary key,
    name_job_title varchar(128) not null,
    name_title int,
    foreign key(name_title) references units_type (id)
);
```

```PostgreSQL
-- Оклад
create table salary(
    id int primary key,
    salary_person money not null
);
```

```PostgreSQL
-- Дата найма
create table start_job(
    id int primary key,
    date_start_job date not null
);
```

```PostgreSQL
-- Проект на который назначен
create table projects(
    id int primary key,
    name_projects varchar(128) not null
);
```

```PostgreSQL
-- ФИО
create table person (
    id int primary key,
    name_person varchar(255),
    start_job_date int,
    foreign key(start_job_date) references start_job (id),
    salary_unique int,
    foreign key(salary_unique) references salary (id),
    job int,
    foreign key(job) references job_title (id),
    project_name int,
    foreign key(project_name) references projects (id)
);
```

![diagram](https://github.com/biparasite/DB-12-01HW-/blob/main/diagram.png)

---

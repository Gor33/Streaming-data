**Задание**

#1.Загрузка данных в КХ

#2.Создайте базу homework
```
CREATE DATABASE homework
```
#3.Создаём таблицу metrika
```
CREATE TABLE homework.metrika
(
    `EventDate` Date,
    `CounterID` UInt32,
    `UserID` UInt64,
    `RegionID` UInt32
)
ENGINE = MergeTree()
PARTITION BY toYYYYMM(EventDate)
ORDER BY (CounterID, EventDate, intHash32(UserID))
```
#4.Заливаем данные в таблицу
```
cat metrika_sample.tsv | clickhouse-client --database homework --query "INSERT INTO metrika FORMAT TSV"
```
#5.Посчитайте какой пользователь UserID сделал больше всего просмотров страниц?

---
description: Commands Cheat Sheet
---

# Mongo

#### **Работа с базами данных**

**Посмотреть список баз данных**:

```mongodb
show dbs
```

**Переключиться на базу данных** (или создать новую, если она ещё не существует):

```mongodb
use <database_name>
```

**Посмотреть список коллекций**:

```mongodb
show collections
```

**Показать все документы в коллекции**:

```mongodb
db.<collection_name>.find()

//for pretty output
db.<collection_name>.find().pretty()
```

**Вывести документы с определённым условием**:

```mongodb
db.<collection_name>.find({ field_name: "value" })
```

**Вывод с ограничением полей**: Чтобы показать только определённые поля в выводе, укажите их значения как `1` (включить) или `0` (исключить):

```mongodb
db.<collection_name>.find({}, { field1: 1, field2: 1, _id: 0 })
```

Чтобы узнать, сколько документов содержится в коллекции:

```mongodb
db.<collection_name>.countDocuments()
```

**Получить первые 10 документов**:

```mongodb
db.<collection_name>.find().limit(10)
```

**Пропустить первые 5 документов и вывести следующие 10**:

```mongodb
db.<collection_name>.find().skip(5).limit(10)
```

---
layout: default
title: Метод Groups.Get
permalink: groups/get/
comments: true
---
# Метод Groups.Get
Возвращает список групп указанного пользователя.

# Синтаксис
```csharp
public ReadOnlyCollection<Group> Get(
	long uid, 
	bool extended = false, 
	GroupsFilters filters = null, 
	GroupsFields fields = null
)
```

## Параметры
+ **uid** - ID пользователя, группы которого необходимо получить.
+ **extended** - Если указать в качестве этого параметра true, то будет возвращена полная информация о группах пользователя. По умолчанию false.
+ **filters** - Список фильтров сообществ, которые необходимо вернуть.
+ **fields** - Список полей из информации о группах, которые необходимо получить.

## Результат
Возвращает список идентификаторов групп gid, в которых состоит пользователь uid. В случае передачи параметра extended равным true, будут также возвращены счётчик количества групп и основные поля.

## Исключения
+ **AccessTokenInvalidException** - не задан или используется неверный AccessToken.

## Пример
```csharp
// Получить список групп, в которых состоит Павел Дуров.
var groups = vk.Groups.Get(1);
foreach (var g in groups)
{
   int id = g.Id; // 214211
}

// Получить всю информацию о событиях в которых участвует Павел Дуров.
var groups = vk.Groups.Get(1, true, GroupsFilters.Events, GroupsFields.All);
foreach (var g in groups)
{
    int id = g.Id; // 214211
    string name = g.Name; // "Какое либо название группы"
    ....
}
```
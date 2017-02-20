# Списки видимости резюме



* [Получение списков видимости](#get)
* [Добавление компаний в список видимости](#add)
* [Удаление компаний из списка видимости](#remove)
* [Очистка списка видимости](#clear)


<a name="get"></a>
## Получение списков видимости

``` 
GET /resumes/{resume_id}/{list_type}
```

где:
* `resume_id` — идентификатор резюме
* `list_type` — тип списка (можно узнать в [справочнике resume_visibility_list_type](/docs/dictionaries.md#etc))

Поддерживаются [стандартные параметры пагинации](/docs/general.md#pagination) `page` и `per_page`
(`per_page` <= 100). 


### Успешный ответ

Успешный ответ приходит с кодом `200 OK` и содержит тело:

```json
{
    "found": 11,
    "page": 0,
    "pages": 1,
    "per_page": 20,
    "limit": 2000,
    "can_add": 1989,
    "items": [
        {
            "id": "1455",
            "name": "HeadHunter",
            "url": "https://api.hh.ru/employers/1455",
            "alternate_url": "https://hh.ru/employer/1455"
        }
    ]
}
```

Ответ включает [стандартные поля пагинации](/docs/general.md#pagination), а также:

Имя | Тип | Описание
----|-----|---------
limit | number | Максимальное количество элементов в списке.
can_add | number | Количество элементов, которые можно добавить в список.
items | array | Список компаний.
items.id | string | Идентификатор работодателя.
items.name | string | Название работодателя.
items.url | string | Ссылка на детальное описание работодателя.
items.alternate_url | string | Ссылка на описание работодателя на сайте.


### Ошибки

* `404 Not Found` – резюме с указанным идентификатором не найдено. 

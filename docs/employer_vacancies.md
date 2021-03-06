# Вакансии для работодателя

* [Публикация вакансий](#creation)
* [Условия заполнения полей при добавлении и редактировании вакансий](#conditions)
* [Редактирование вакансий](#edit)
* [Продление вакансий](#prolongate)
* [Информация о возможности продления вакансии](#prolongate-info)
* [Список опубликованных вакансий](#active)
* [Архивация вакансий](#archive)
* [Список архивных вакансий](#archived)
* [Удаление вакансий](#hide)
* [Список удаленных вакансий](#hidden)
* [Восстановление из удаленных](#restore)
* [Статистика по вакансии](#stats)

Смотрите также:

* [Дополнительные поля для автора вакансии при получении вакансии](vacancies.md#author)


<a name="creation"></a>
## Публикация вакансий

`POST /vacancies`


### Общая информация

В качестве тела запроса необходимо передавать
[JSON](general.md#request-body) с данными размещаемой вакансии,
формат данных аналогичен [просмотру вакансии](vacancies.md#item), но также содержит
некоторые дополнительные поля.

> В соответствии с
[законом РФ № 1032-1 от 19.04.1991 в ред. от 02.07.2013 г.](https://hh.ru/article/13967)
запрещено размещать информацию, ограничивающую права или устанавливающую
преимущества для соискателей по полу, возрасту, семейному положению и другим
обстоятельствам, не связанным с деловыми качествами работников.

* при успешной публикации будут списаны соответствующие услуги.
* все вакансии проходят ручную модерацию.
* в течение нескольких минут после публикации вакансия станет доступна в поиске.


### Полезные ссылки

* [правила размещения вакансий](https://hh.ru/article/341)
* [как составить хорошее описание вакансии](https://hh.ru/article/16239)


<a name="creation-example"></a>
### Пример тела запроса

```json
{
  "description": "<p>— Eh bien, mon prince. Gênes et Lucques ne sont plus que des apanages, des поместья, de la famille Buonaparte. Non, je vous préviens que si vous ne me dites pas que nous avons la guerre, si vous vous permettez encore de pallier toutes les infamies, toutes les atrocités de cet Antichrist (ma parole, j'y crois) — je ne vous connais plus, vous n'êtes plus mon ami, vous n'êtes plus мой верный раб, comme vous dites. Ну, здравствуйте, здравствуйте.</p><p><em>Je vois que je vous fais peur</em>, садитесь и рассказывайте.</p>",
  "key_skills": [
    {"name": "Холодные продажи"},
    {"name": "Проведение промо акций"}
  ],
  "schedule": {
    "id": "flyInFlyOut"
  },
  "experience": {
    "id": "moreThan6"
  },
  "employment": {
    "id": "full"
  },
  "name": "Менеджер по продажам",
  "area": {
    "id": "1"
  },
  "type": {
    "id": "open"
  },
  "employer": {
    "id": "1455"
  },
  "specializations": [
    {
      "id": "17.324"
    },
    {
      "id": "3.148"
    }
  ],
  "response_letter_required": true,
  "salary": {
    "from": 100,
    "to": 500,
    "currency": "USD"
  },
  "contacts": {
    "name": "Иванов Иван",
    "email": "i.ivanov@example.com",
    "phones": [
      {
        "country": "7",
        "city": "495",
        "number": "1234567",
        "comment": "с 10 до 20"
      }
    ]
  },
  "accept_handicapped": true,
  "code": "код-1234",
  "response_notifications": true,
  "allow_messages": true,
  "billing_type": {
    "id": "standard"
  },
  "site": {
    "id": "hh"
  },
  "address": {
    "id": "123",
    "show_metro_only": true
  },
  "manager": {
    "id": "321"
  },
  "test": {
    "id": "42",
    "required": true
  },
  "branded_template": {
    "id": "marketing"
  }
}
```


<a name="creation_fields"></a>
### Поля запроса

* `[]` (например, в полях специализации и контактах) обозначает, что значение данного ключа является массивом объектов.  
* `a.b` обозначает объект `a` с ключом `b` описанного типа.

Путь | JSON тип | Описание
---- | -------- | --------
name | string | название
description | string | описание в html, не менее 200 символов
key_skills | array | список ключевых навыков, не более 30
key_skills[].name | string | название ключевого навыка
specializations | array | список специализаций
specializations[].id | string | специализация [из справочника](specializations.md)
area.id | string | регион публикации [из справочника](areas.md)
type.id | string | тип из [справочника vacancy_type](dictionaries.md)
billing_type.id | string | биллинговый тип [из справочника vacancy_billing_type](dictionaries.md)
site.id | string | сайт для публикации [из справочника vacancy_site](dictionaries.md)
code | string | внутренний код вакансии
department.id | string | департамент [из справочника](employer_departments.md), от имени которого размещается вакансия (если данная возможность доступна для компании)
salary | object или null | зарплата
salary.from | numeric или null | нижняя граница зарплаты
salary.to | numeric или null | верхняя граница зарплаты
salary.currency | string | код валюты из [справочника currency](dictionaries.md)
address | object или null | адрес
address.id | string | адрес из [списка доступных адресов работодателя](employer_addresses.md)
address.show_metro_only | boolean | показывать только метро для указанного адреса
experience.id | string | требуемый опыт работы из [справочника experience](dictionaries.md)
schedule.id | string | график работы из [справочника schedule](dictionaries.md)
employment.id | string | тип занятости из [справочника employment](dictionaries.md)
contacts | object | контактная информация (для вакансий рабочих специальностей). Определить является ли специальность рабочей можно по полю laboring из [справочника специализаций](specializations.md) 
contacts.name | string | контактное лицо
contacts.email | string | email
contacts.phones | array | список телефонов для связи
contacts.phones[].country | string | код страны
contacts.phones[].city | string | код города
contacts.phones[].number | string | телефон
contacts.phones[].comment | string или null | комментарий (удобное время для звонка по этому номеру)
test | object | тест для вакансии
test.id | string | тест, который будет добавлен в вакансию
test.required | boolean | требовать прохождение теста для отклика на вакансию
response_url | string | URL отклика для прямых вакансий (`type.id=direct`)
custom_employer_name | string | название компании для анонимных вакансий (`type.id=anonymous`), например "крупный российский банк"
employer.id | string | работодатель, для которого размещается вакансия
manager.id | string | контактное лицо (менеджер) по размещаемой вакансии, по-умолчанию текущий пользователь
response_notifications | boolean | уведомлять о новых откликах
<a name="allow_messages"></a> allow_messages | boolean | возможность [переписки с кандидатами](https://inboxemp.hh.ru/) по данной вакансии
response_letter_required | boolean | требовать сопроводительное письмо
accept_handicapped | boolean | указание, что вакансия доступна для соискателей с инвалидностью
branded_template.id | string | <a name="branded-template-field"></a> брендированное оформление вакансии из [справочника](employer_vacancy_branded_templates.md#list)


<a name="creation-results"></a>
### Результат запроса

* `201 Created` - успешное добавление. В заголовке `Location` будет
  содержаться ссылка на добавленную вакансию:
  
```
   HTTP/1.1 201 Created
   
   Location: /vacancies/78789890
```
  
  Также в теле ответа будет возвращаться json с идентификатором:
```
    {"id": "78789890"}
```
* `403 Forbidden` - добавление вакансий недоступно данному пользователю или
  добавление вакансии недоступно, так как вакансия с похожими
  данными уже опубликована у данного работодателя. Если вы уверены, что
  добавление дубликата необходимо, вы можете добавить к запросу параметр
  `POST /vacancies?ignore_duplicates=true`.
* `400 Bad Request` - ошибки в полях при добавлении вакансии.

Дополнительно к HTTP коду сервер может вернуть описание
[причины ошибки](errors.md#vacancies-create-n-edit).


<a name="conditions"></a>
## Условия заполнения полей при добавлении и редактировании вакансий

`GET /vacancy_conditions`

Каждое конечное поле описано объектом правил. Если поле состоит из
объекта с несколькими полями, эти поля описаны в `fields`.

Условия полей вакансии доступны только работодателям, в противном случае
вернётся код ответа `403 Forbidden`.

Для всех полей и их частей указано, являются ли они необходимыми (`required`).


### Пример ответа

Успешный ответ содержит код ответа `200 OK` и тело.

```json
{
    "accept_handicapped": {
        "required": false
    },
    "address": {
        "fields": {
            "show_metro_only": {
                "required": false
            }
        },
        "required": false
    },
    "allow_messages": {
        "required": false
    },
    "area": {
        "required": true
    },
    "billing_type": {
        "required": true
    },
    "code": {
        "max_length": 50,
        "min_length": 0,
        "required": false
    },
    "contacts": {
        "fields": {
            "email": {
                "max_length": 255,
                "min_length": 0,
                "required": false
            },
            "name": {
                "max_length": 255,
                "min_length": 0,
                "required": true
            },
            "phones": {
                "fields": {
                    "city": {
                        "max_length": 6,
                        "min_length": 1,
                        "regexp": "^\\d{0,6}$",
                        "required": true
                    },
                    "comment": {
                        "max_length": 255,
                        "min_length": 0,
                        "required": false
                    },
                    "country": {
                        "max_length": 6,
                        "min_length": 1,
                        "regexp": "^\\+?\\d{0,5}$",
                        "required": true
                    },
                    "number": {
                        "max_length": 32,
                        "min_length": 4,
                        "regexp": "^[\\d -]{4,32}$",
                        "required": true
                    }
                },
                "max_count": 2,
                "min_count": 0,
                "required": true
            }
        },
        "required": false
    },
    "custom_employer_name": {
        "max_length": 150,
        "min_length": 0,
        "required": false
    },
    "department": {
        "max_length": 32,
        "min_length": 0,
        "required": false
    },
    "description": {
        "max_length": 10000,
        "min_length": 200,
        "required": true
    },
    "employment": {
        "required": false
    },
    "experience": {
        "required": false
    },
    "key_skills": {
        "max_count": 30,
        "min_count": 0,
        "required": false
    },
    "manager": {
        "required": false
    },
    "name": {
        "max_length": 220,
        "min_length": 0,
        "required": true
    },
    "response_letter_required": {
        "required": false
    },
    "response_notifications": {
        "required": false
    },
    "response_url": {
        "max_length": 511,
        "min_length": 0,
        "regexp": "^(http|https)://.+$",
        "required": false
    },
    "salary": {
        "fields": {
            "currency": {
                "required": false
            },
            "from": {
                "required": false
            },
            "to": {
                "required": false
            }
        },
        "required": false
    },
    "schedule": {
        "required": false
    },
    "site": {
        "required": true
    },
    "specializations": {
        "max_count": null,
        "min_count": 1,
        "required": true
    },
    "test": {
        "fields": {
            "required": {
                "required": false
            }
        },
        "required": false
    },
    "type": {
        "required": true
    }
}

```

### Правила

Имя | Тип | Описание
--- | --- | --------
required | логический | Является ли поле вакансии или поле объекта необходимым?
min_length | целое | Минимальная длина для текстовых полей.
max_length | целое | Максимальная длина для текстовых полей.
min_count | целое | Минимальное количество объектов для полей, где необходимо передавать список.
max_count | целое или `null` | Максимально количество объектов для полей, где необходимо передавать список. `null` – если количество не ограничено.


<a name="edit"></a>
## Редактирование вакансий

`PUT /vacancies/{vacancy_id}`

Редактирование происходит по аналогии с созданием вакансии, но есть возможность
передачи отдельных полей в объекте для частичного редактирования вакансии.
Cоставные поля (например, `salary`, `contacts`, `specializations`) можно
редактировать только целиком, передавая полный объект. Например, для изменения
валюты в зарплате, необходимо передавать также и значения зарплаты, а
для изменения специализации необходимо передать полный список.


### Поля доступные для редактирования

поле | описание
-----|----------
name | название
description | описание
key_skills | ключевые навыки
schedule | график работы
experience | требуемый опыт работы
employment | тип занятости
specializations | список специализаций
salary | зарплата
address | адрес
test | тестовое задание
department | департамент
code | внутренний код вакансии
response_letter_required | необходимость сопроводительного письма при отклике
accept_handicapped | указание, что вакансия доступна для соискателей с инвалидностью
response_notifications | настройка уведомления о новых откликах
allow_messages | возможность переписки с кандидатами по данной вакансии
contacts | контактная информация (для вакансий рабочих специальностей)
custom_employer_name | название компании для анонимных вакансий
response_url | URL отклика для прямых вакансий

Остальные поля доступны только для чтения, либо их можно задать только при создании вакансии.

<a name="edit-results"></a>
### Результат запроса

* `204 No Content` - успешное обновление.
* `404 Not Found` - редактируемая вакансия не найдена.
* `403 Forbidden` - редактирование вакансий недоступно данному пользователю.
* `400 Bad Request` - ошибки в полях при редактировании вакансии.

Дополнительно к HTTP коду сервер может вернуть описание
[причины ошибки](errors.md#vacancies-create-n-edit).

<a name="edit_more"></a>
### Смена биллинг-типа, менеджера вакансии

Изменение биллингового типа вакансии, а также передача вакансии другому
менеджеру компании происходит по аналогии с редактированием
`POST /vacancies/{vacancy_id}`. Единственная особенность — эти поля
(`billing_type` и `manager`) необходимо отправлять отдельно от остальных полей
вакансии.

```
PUT /vacancies/{vacancy_id}
{"billing_type":{"id":"premium"}
```

```
PUT /vacancies/{vacancy_id}
{"manager":{"id":"1337"}
```

При передаче этих полей вместе с любыми другими вернется ошибка.


<a name="other-actions"></a>
### Прочие действия

* [архивация](#archive)
* [удаление](#hide)
* [восстановление из удаленных](#restore)


<a name="prolongate"></a>
## Продление вакансий

**Продление вакансии по стоимости приравнивается к новой публикации**

Существуют ограничения по продлению вакансии, они могут меняться, на данный
момент работают следующие правила:

* стандартные вакансии можно продлевать, если с предыдущего продления прошло не менее 3 дней.
* вакансии "стандарт-плюс" возможно продлевать не ранее 5 дней до окончания публикации.


### Запрос

`POST /vacancies/{vacancy_id}/prolongate`

где `vacancy_id` - идентификатор вакансии.


### Ответ

* `204 No Content` – вакансия продлена успешно
* `403 Forbidden` – текущий пользователь не является работодателем или
  продление невозможно.
* `404 Not Found` – вакансия не существует или текущему пользователю
  недоступно её продление.

Дополнительно к HTTP коду сервер может вернуть
описание [причины ошибки](errors.md#vacancies-prolongate).


<a name="prolongate-info"></a>
## Информация о возможности продления вакансии


### Запрос

`GET /vacancies/{vacancy_id}/prolongate`

где `vacancy_id` - идентификатор вакансии.


### Ответ

Успешный ответ приходит с кодом `200 OK`.

Пример ответа, когда продление невозможно:

```json
{
  "id": "123456789",
  "expires_at": "2015-11-19T17:10:48+0300",
  "actions": [
    {
      "id": "prolongate",
      "enabled": false,
      "disable_reason": {
        "id": "standard_plus_publication_is_updated_automatically",
        "name": "Вакансия \"Стандарт Плюс\" не может быть обновлена, это происходит автоматически раз в три дня."
      }
    }
  ]
}
```

Пример ответа, когда продление возможно:

```json
{
  "id": "123456789",
  "expires_at": "2015-11-19T17:10:48+0300",
  "actions": [
    {
      "id": "prolongate",
      "enabled": true,
      "url": "https://api.hh.ru/vacancies/123456789/prolongate",
      "method": "POST"
    }
  ]
}
```

Где:

* `actions` – список действий, которые можно предпринять для продления
  вакансии. В данный момент поддерживается только обычное продление.
* `id` – идентификатор вакансии.
* `expires_at` – дата и время окончания публикации вакансии.

По действию доступны данные:

* `id` - идентификатор действия,
* `enabled` - возможно ли действие,
* `disable_reason` - причина, по которой совершить действие невозможно.
  Возможные причины перечислены [в справочнике](dictionaries.md)
  `vacancy_not_prolonged_reason`.
* `url` и `method` – url и HTTP метод, с которыми нужно сделать запрос,
  чтобы совершить действие.

### Ошибки

* `403 Forbidden` – текущий пользователь не является работодателем.
* `404 Not Found` – вакансия несуществует или текущему пользователю
  недоступно получение информации о вакансии.


<a name="active"></a>
## Список опубликованных вакансий

`GET /employers/{employer_id}/vacancies/active?manager_id={manager_id}`

Для просмотра списка опубликованных вакансий необходимо указать id менеджера,
даже если необходимо сделать запрос для текущего менеджера (значение можно
взять из `/me`).


### Ответ

Успешный ответ приходит с кодом `200 OK` и содержит:

```json
{
    "found": 1,
    "page": 0,
    "pages": 1,
    "per_page": 20,
    "items": [
    {
      "salary": {
        "to": null,
        "from": 30000,
        "currency": "RUR"
      },
      "name": "Секретарь",
      "area": {
        "url": "https://api.hh.ru/areas/1",
        "id": "1",
        "name": "Москва"
      },
      "url": "https://api.hh.ru/vacancies/8331228",
      "published_at": "2013-07-08T16:17:21+0400",
      "relations": [],
      "employer": {
        "logo_urls": {
          "90": "https://hh.ru/employer-logo/289027.png",
          "240": "https://hh.ru/employer-logo/289169.png",
          "original": "https://hh.ru/file/2352807.png"
        },
        "name": "HeadHunter",
        "url": "https://api.hh.ru/employers/1455",
        "alternate_url": "https://hh.ru/employer/1455",
        "id": "1455",
        "trusted": true
      },
      "response_letter_required": true,
      "address": null,
      "alternate_url": "https://hh.ru/vacancy/8331228",
      "apply_alternate_url": "https://hh.ru/applicant/vacancy_response?vacancyId=8331228",
      "department": {
        "id": "HH-1455-TECH",
        "name": "HeadHunter::Технический департамент"
      },
      "premium": false,
      "type": {
        "id": "open",
        "name": "Открытая"
      },
      "id": "8331228",
      "archived": false,

      "counters": {
        "views": 100500,
        "responses": 5,
        "unread_responses": 3,
        "resumes_in_progress": 5,
        "invitations": 10
      },
      "expires_at": "2013-07-08T16:17:21+0400",
      "has_updates": false
    }
  ]
}
```

Где помимо [стандартных полей вакансии](vacancies.md#nano) вернутся
дополнительные поля:

ключ | тип | описание
-----|-----|---------
counters.views | number | количество просмотров вакансии
counters.responses | number | количество откликов на вакансию
counters.unread_responses | number | количество непросмотренных откликов на вакансию
counters.resumes_in_progress | number | количество резюме в работе на вакансию
counters.invitations | number | количество приглашений на вакансию
expires_at | string | дата окончания публикации вакансии
has_updates | boolean | Есть ли в откликах/приглашениях по данной вакансии обновления, требующие внимания

Также доступен
[список опубликованных вакансий, подходящих для приглашения соискателя](employer_vacancies_for_invitation.md).


### Поддерживаемые параметры

Помимо стандартных параметров для пагинации `per_page` и `page`, коллекция поддерживает:

* `text` — строка для поиска по названию вакансии
* `area` — id региона (см.
  [список регионов, в которых есть активные вакансии](employer_vacancy_areas_active.md))
* `order_by` — сортировка вакансий, возможные варианты доступны в справочнике
  `employer_active_vacancies_order`


<a name="archive"></a>
## Архивация вакансий

Для переноса вакансии в архив необходимо отправить запрос PUT:

`PUT /employers/{employer_id}/vacancies/archived/{vacancy_id}`

При успешной архивации вернётся `204 No Content`.


<a name="archived"></a>
## Список архивных вакансий

`GET /employers/{employer_id}/vacancies/archived?manager_id={manager_id}`

Для просмотра списка архивных вакансий также необходимо указать id менеджера,
даже если необходимо сделать запрос для текущего менеджера (значение можно
взять из `/me`). Поддерживается пагинация (`per_page` и `page`) и сортировка
(`order_by`). Возможные значения сортировки доступны в справочнике
`employer_archived_vacancies_order` (`/dictionaries`). В отличие от списка
опубликованных вакансий, данная коллекция не поддерживает поиск (параметры
`text` и `area`).


### Ответ

Успешный ответ приходит с кодом `200 OK` и содержит:

```json
{
    "found": 1,
    "page": 0,
    "pages": 1,
    "per_page": 20,
    "items": [
    {
      "salary": {
        "to": null,
        "from": 30000,
        "currency": "RUR"
      },
      "name": "Секретарь",
      "area": {
        "url": "https://api.hh.ru/areas/1",
        "id": "1",
        "name": "Москва"
      },
      "url": "https://api.hh.ru/vacancies/8331228",
      "published_at": "2013-07-08T16:17:21+0400",
      "relations": [],
      "employer": {
        "logo_urls": {
          "90": "https://hh.ru/employer-logo/289027.png",
          "240": "https://hh.ru/employer-logo/289169.png",
          "original": "https://hh.ru/file/2352807.png"
        },
        "name": "HeadHunter",
        "url": "https://api.hh.ru/employers/1455",
        "alternate_url": "https://hh.ru/employer/1455",
        "id": "1455",
        "trusted": true
      },
      "response_letter_required": true,
      "address": null,
      "alternate_url": "https://hh.ru/vacancy/8331228",
      "apply_alternate_url": "https://hh.ru/applicant/vacancy_response?vacancyId=8331228",
      "department": {
        "id": "HH-1455-TECH",
        "name": "HeadHunter::Технический департамент"
      },
      "premium": false,
      "type": {
        "id": "open",
        "name": "Открытая"
      },
      "id": "8331228",
      "archived": true,

      "counters": {
        "responses": 3,
        "invitations_and_responses": 5
      },
      "archived_at": "2013-08-08T16:17:21+0400"
    }
  ]
}
```

Где помимо [стандартных полей вакансии](vacancies.md#nano) вернутся
дополнительные поля:

ключ | тип | описание
---- |---- |---------
counters.responses | числовой | количество откликов на вакансию
counters.invitations_and_responses | числовой | количество откликов и приглашений на вакансию
archived_at | строка | дата архивации вакансии


<a name="hide"></a>
## Удаление вакансий

`PUT /employers/{employer_id}/vacancies/hidden/{vacancy_id}`

Удалить можно только вакансию из архива.
При успешной операции вернётся `204 No Content`.


<a name="hidden"></a>
## Список удаленных вакансий

`GET /employers/{employer_id}/vacancies/hidden?manager_id={manager_id}`

Поддерживается пагинация (`per_page` и `page`) и сортировка (`order_by`).
Возможные значения сортировки доступны в справочнике
`employer_hidden_vacancies_order` (`/dictionaries`). В отличие от списка
опубликованных вакансий, данная коллекция не поддерживает поиск (параметры
`text` и `area`).


### Ответ

Успешный ответ приходит с кодом `200 OK` и содержит:

```json
{
    "found": 1,
    "page": 0,
    "pages": 1,
    "per_page": 20,
    "items": [
    {
      "salary": {
        "to": null,
        "from": 30000,
        "currency": "RUR"
      },
      "name": "Секретарь",
      "area": {
        "url": "https://api.hh.ru/areas/1",
        "id": "1",
        "name": "Москва"
      },
      "url": "https://api.hh.ru/vacancies/8331228",
      "published_at": "2013-07-08T16:17:21+0400",
      "relations": [],
      "employer": {
        "logo_urls": {
          "90": "https://hh.ru/employer-logo/289027.png",
          "240": "https://hh.ru/employer-logo/289169.png",
          "original": "https://hh.ru/file/2352807.png"
        },
        "name": "HeadHunter",
        "url": "https://api.hh.ru/employers/1455",
        "alternate_url": "https://hh.ru/employer/1455",
        "id": "1455",
        "trusted": true
      },
      "response_letter_required": true,
      "address": null,
      "alternate_url": "https://hh.ru/vacancy/8331228",
      "apply_alternate_url": "https://hh.ru/applicant/vacancy_response?vacancyId=8331228",
      "department": {
        "id": "HH-1455-TECH",
        "name": "HeadHunter::Технический департамент"
      },
      "premium": false,
      "type": {
        "id": "open",
        "name": "Открытая"
      },
      "id": "8331228",
      "archived": true
    }
  ]
}
```

Ответ состоит из [стандартных полей вакансии](vacancies.md#nano).


<a name="restore"></a>
## Восстановление из удаленных

`DELETE /employers/{employer_id}/vacancies/hidden/{vacancy_id}`

Восстановить можно только удаленную из архива вакансию.
При успешной операции вернётся `204 No Content`.
Вакансия вернется в архив.


<a name="stats"></a>
## Статистика по вакансии

`GET /vacancies/{vacancy_id}/stats`

где `vacancy_id` - идентификатор вакансии.

```json
{
    "items": [
        {
            "date": "2017-01-10",
            "responses": 1,
            "views": 36
        },
        {
            "date": "2017-01-11",
            "responses": 4,
            "views": 35
        },
        {
            "date": "2017-01-12",
            "responses": 1,
            "views": 32
        },
        {
            "date": "2017-01-13",
            "responses": null,
            "views": null
        },
        {
            "date": "2017-01-14",
            "responses": null,
            "views": null
        }
    ]
}
```
Здесь:

Имя | Тип | Описание
--- | --- | ---
date | Строка | Дата в формате `YYYY-MM-DD`
responses | Число или null | Количество откликов, `null` если дата в будущем или данных на эту дату нет
views | Число или null | Количество просмотров, `null` если дата в будущем или данных на эту дату нет

Возвращается окно в 5 последних дней существования вакансии:

* если вакансия создана поздее начала окна, то первой датой будет дата создания вакансии;
* если вакансия находится в архиве или удалена, то последней датой будет дата архивации.

Если вакансия с идентификатором `vacancy_id` не существует или у текущего менеджера нет прав на редактирование данной вакансии, то в
ответ вернется `404 Not Found`.

# Описание использованных параметров поиска вакансий

Для получения выставленных параметров в
[поиске вакансий](vacancies.md#search) необходимо в поисковом запросе на
`/vacancies` добавить параметр `describe_arguments=true`.

Пример выдачи параметров (приведён пример всех возможных параметров, в
реальных запросах данных будет меньше):

```json
{
    "arguments": [
        {
            "argument": "area",
            "value": "1",
            "name": "Москва",
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&...",
            "cluster_group": {
                "id": "area",
                "name": "Регион"
            }
        },
        {
            "argument": "area",
            "value": "2",
            "name": "Санкт-Петербург",
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=1&...",
            "cluster_group": {
                "id": "area",
                "name": "Регион"
            }
        },
        {
            "argument": "text",
            "value": "менеджер по продажам",
            "name": null,
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&...",
            "cluster_group": null
        },
        {
            "argument": "search_field",
            "value": "name",
            "name": "в названии вакансии",
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&...",
            "cluster_group": null
        },
        {
            "argument": "experience",
            "value": "between3And6",
            "name": "От 3 до 6 лет",
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&...",
            "cluster_group": {
                "id": "experience",
                "name": "Опыт работы"
            }
        },
        {
            "argument": "employment",
            "value": "full",
            "name": "Полная занятость",
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&...",
            "cluster_group": {
                "id": "employment",
                "name": "Тип занятости"
            }
        },
        {
            "argument": "schedule",
            "value": "fullDay",
            "name": "Полный день",
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&...",
            "cluster_group": {
                "id": "schedule",
                "name": "График работы"
            }
        },
        {
            "argument": "metro",
            "value": "2.133",
            "name": "Сокол",
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&metro=2&...",
            "cluster_group": {
                "id": "metro",
                "name": "Метро"
            }
        },
        {
            "argument": "specialization",
            "value": "24",
            "name": "Спорт, фитнес",
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&...",
            "cluster_group": {
                "id": "professional_area",
                "name": "Профобласть"
            }
        },
        {
            "argument": "specialization",
            "value": "24.624",
            "name": "Ногтевой сервис",
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&specialization=24&...",
            "cluster_group": {
                "id": "specialization",
                "name": "Специализация"
            }
        },
        {
            "argument": "industry",
            "value": "51",
            "name": "ЖКХ",
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&...",
            "cluster_group": {
                "id": "industry",
                "name": "Отрасль компании"
            }
        },
        {
            "argument": "industry",
            "value": "51.675",
            "name": "Энергосбережение",
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&...",
            "cluster_group": null
        },
        {
            "argument": "label",
            "value": "not_from_agency",
            "name": "Без вакансий агентств",
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&...",
            "cluster_group": {
                "id": "label",
                "name": "Исключение"
            }
        },
        {
            "argument": "currency",
            "value": "USD",
            "name": null,
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&...",
            "cluster_group": null
        },
        {
            "argument": "only_with_salary",
            "value": "true",
            "name": "Указана зарплата",
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&...",
            "cluster_group": {
                "id": "salary",
                "name": "Зарплата"
            }
        },
        {
            "argument": "salary",
            "value": "1500",
            "name": "от 1500 USD",
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&...",
            "cluster_group": {
                "id": "salary",
                "name": "Зарплата"
            }
        },
        {
            "argument": "bottom_lat",
            "value": "55.58",
            "name": null,
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&...",
            "cluster_group": null
        },
        {
            "argument": "left_lng",
            "value": "37.52",
            "name": null,
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&...",
            "cluster_group": null
        },
        {
            "argument": "top_lat",
            "value": "55.74",
            "name": null,
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&...",
            "cluster_group": null
        },
        {
            "argument": "right_lng",
            "value": "37.86",
            "name": null,
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&...",
            "cluster_group": null
        },
        {
            "argument": "date_from",
            "value": "2017-02-01",
            "name": null,
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&...",
            "cluster_group": null
        },
        {
            "argument": "date_to",
            "value": "2017-02-10",
            "name": null,
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&...",
            "cluster_group": null
        },
        {
            "argument": "order_by",
            "value": "salary_desc",
            "name": null,
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&...",
            "cluster_group": null
        },
        {
            "argument": "sort_point_lat",
            "value": "55.74",
            "name": null,
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&...",
            "cluster_group": null
        },
        {
            "argument": "sort_point_lng",
            "value": "37.86",
            "name": null,
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&page=0&area=2&...",
            "cluster_group": null
        },
        {
            "id": "per_page",
            "name": null,
            "value": "10",
            "disable_url": "https://api.hh.ru/vacancies?page=0&area=1&area=2...",
            "cluster": null
        },
        {
            "id": "page",
            "name": null,
            "value": "0",
            "disable_url": "https://api.hh.ru/vacancies?per_page=10&area=1&area=2&...",
            "cluster": null
        },
        {
            "id": "clusters",
            "name": null,
            "value": "true",
            "disable_url": "https://api.hh.ru/vacancies?page=0&area=1&area=2...",
            "cluster": null
        },
        {
            "id": "describe_arguments",
            "name": null,
            "value": "true",
            "disable_url": "https://api.hh.ru/vacancies?page=0&area=1&area=2...",
            "cluster": null
        }
    ]
}
```

В списке выдаются только те параметры, которые
[влияют на поиск вакансий](vacancies.md#search-params),
неизвестные параметры игнорируются. Параметр с одним значением `argument` может
повторяться несколько раз, если параметр имеет множественное значение.

Для каждого элемента в списке `arguments` будет доступно:

Поле | Тип | Описание
---- | ----| --------
argument | string | параметр поиска вакансии
value | string | значение параметра
name | string или null | название значения, если оно есть, либо `null`
disable_url | string | url поиска вакансий, который получится, если перестать учитывать в поиске данный параметр
cluster_group | object или null | [группа кластеров](clusters.md), которая связана с данным параметром, если она есть, либо `null`
cluster_group.id | string | идентификатор группы кластеров
cluster_group.name | string | название группы кластеров


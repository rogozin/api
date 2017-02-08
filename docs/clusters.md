# Кластеры в поиске вакансий

Часто в [поиске вакансий](vacancies.md#search) удобно получать расширенную
информацию о том, как разделены вакансии в поиске по различным критериям.
Например, при поиске по выбранным критериям, удобно знать каким образом
распределены зарплаты в искомых вакансиях - в скольких вакансиях зарплата
указана, в скольких она больше определенной суммы. Эти данные возможно получить
пользуясь поиском вакансий, формируя отдельный запрос на каждый интересующий
критерий. Однако значительно проще воспользоваться специальной возможностью
поисковой выдачи - разбиения данных на кластера.

Пример использования этих данных на основном сайте hh.ru можно увидеть в левой
колонке на [странице результатов поиска вакансий](https://hh.ru/search/vacancy).

Для того, чтобы получить данные по кластерам, необходимо в поисковом запросе на
`/vacancies` добавить параметр `clusters=true`. При этом в поисковом ответе
помимо поисковой выдачи будет возвращаться дополнительная разбивка вакансий по
кластерам. Если необходимо получить только кластера, а не сам список найденных
вакансий, можно указать в запросе `?per_page=0`.

Кластера разбиваются на группы кластеров, в группу попадают кластера схожего
значения. Например, группа кластеров "Зарплата" содержит кластер
"от 45000 руб.".

Пример выдачи кластеров в поиске, ключ `clusters` добавляется к
[стандартной выдаче поиска вакансий](vacancies.md#search-results)
(приведены все возможные группы кластеров, в реальных запросах не все группы
будут присутствовать):

```json
{
    "clusters": [
        {
            "id": "professional_area",
            "name": "Профобласть",
            "items": [
                {
                    "name": "Спортивные клубы, фитнес, салоны красоты",
                    "url": "https://api.hh.ru/vacancies?clusters=true&specialization=24",
                    "count": 2852
                },
                {
                    "name": "Инсталляция и сервис",
                    "url": "https://api.hh.ru/vacancies?clusters=true&specialization=25",
                    "count": 2469
                }
            ]
        },
        {
            "id": "specialization",
            "name": "Специализация",
            "items": [
                {
                    "name": "Продажи",
                    "url": "https://api.hh.ru/vacancies?clusters=true&specialization=15.389",
                    "count": 3098
                },
                {
                    "name": "Административный персонал",
                    "url": "https://api.hh.ru/vacancies?clusters=true&specialization=15.388",
                    "count": 1035
                }
            ]
        },
        {
            "id": "area",
            "name": "Регион",
            "items": [
                {
                    "name": "Москва",
                    "url": "https://api.hh.ru/vacancies?clusters=true&area=1",
                    "count": 83285
                },
                {
                    "name": "Московская область",
                    "url": "https://api.hh.ru/vacancies?clusters=true&area=2019",
                    "count": 16413
                }
            ]
        },
        {
            "id": "metro",
            "name": "Метро",
            "items": [
                {
                    "name": "Замоскворецкая",
                    "url": "https://api.hh.ru/vacancies?clusters=true&metro=2&area=1",
                    "count": 11639
                },
                {
                    "name": "Люблинско-Дмитровская",
                    "url": "https://api.hh.ru/vacancies?clusters=true&metro=10&area=1",
                    "count": 4197
                }
            ]
        },
        {
            "id": "schedule",
            "name": "График работы",
            "items": [
                {
                    "name": "Полный день",
                    "url": "https://api.hh.ru/vacancies?clusters=true&schedule=fullDay",
                    "count": 67101
                },
                {
                    "name": "Сменный график",
                    "url": "https://api.hh.ru/vacancies?clusters=true&schedule=shift",
                    "count": 10736
                }
            ]
        },
        {
            "id": "experience",
            "name": "Опыт работы",
            "items": [
                {
                    "name": "От 1 года до 3 лет",
                    "url": "https://api.hh.ru/vacancies?clusters=true&experience=between1And3",
                    "count": 39873
                },
                {
                    "name": "От 3 до 6 лет",
                    "url": "https://api.hh.ru/vacancies?clusters=true&experience=between3And6",
                    "count": 22922
                }
            ]
        },
        {
            "id": "label",
            "name": "Исключение",
            "items": [
                {
                    "name": "Без вакансий агентств",
                    "url": "https://api.hh.ru/vacancies?clusters=true&label=not_from_agency",
                    "count": 77116
                },
                {
                    "name": "Только с адресом",
                    "url": "https://api.hh.ru/vacancies?clusters=true&label=with_address",
                    "count": 47774
                },
                {
                    "name": "Только доступные для людей с инвалидностью",
                    "url": "https://api.hh.ru/vacancies?clusters=true&label=accept_handicapped",
                    "count": 1407
                }
            ]
        },
        {
            "id": "salary",
            "name": "Зарплата",
            "items": [
                {
                    "name": "Указана",
                    "url": "https://api.hh.ru/vacancies?clusters=true&only_with_salary=true",
                    "count": 51300
                },
                {
                    "name": "от 45000 руб.",
                    "url": "https://api.hh.ru/vacancies?salary=45000&clusters=true&only_with_salary=true",
                    "count": 40026
                },
                {
                    "name": "от 75000 руб.",
                    "url": "https://api.hh.ru/vacancies?salary=75000&clusters=true&only_with_salary=true",
                    "count": 19903
                }
            ]
        },
        {
            "id": "employment",
            "name": "Тип занятости",
            "items": [
                {
                    "name": "Полная занятость",
                    "url": "https://api.hh.ru/vacancies?clusters=true&employment=full",
                    "count": 79713
                },
                {
                    "name": "Частичная занятость",
                    "url": "https://api.hh.ru/vacancies?clusters=true&employment=part",
                    "count": 2699
                }
            ]
        },
        {
            "id": "industry",
            "name": "Отрасль компании",
            "items": [
                {
                    "name": "Информационные технологии, системная интеграция, интернет",
                    "url": "https://api.hh.ru/vacancies?clusters=true&industry=7",
                    "count": 10316
                },
                {
                    "name": "Сельское хозяйство",
                    "url": "https://api.hh.ru/vacancies?clusters=true&industry=29",
                    "count": 512
                }
            ]
        }
    ]
}
```

Набор групп кластеров (элементы массива `clusters`) может отличаться от
запроса к запросу и зависит от параметров поискового запроса. Список всех
возможных групп кластеров можно узнать в [справочнике](dictionaries.md) в
элементе с ключем `vacancy_cluster`.

При этом, если в поисковом запросе было указано `clusters=false` или параметр
`clusters` вообще не был указан, то поле `clusters` в ответе будет `null`.

Каждая группа кластеров имеет следующие поля:

Имя | Тип | Значение
--- | --- | ---
id | string | Тип кластера
name | string | Название типа кластера
items | array | Массив поисковых запросов в данном кластере с указанием дополнительных параметров

Каждый элемент массива `items` представляет из себя объект со следующими полями:

Имя | Тип | Значение
--- | --- | ---
name | string | Название элемента кластера
url | string | Ссылка на поисковую выдачу по данному элементу кластера
count | number | Количество вакансий в данном элементе кластера

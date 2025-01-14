# Получить список доступных методов methods

{% note warning "Мы еще обновляем эту страницу" %}

Тут может не хватать некоторых данных — дополним в ближайшее время

{% endnote %}

{% if build == 'dev' %}

{% note alert "TO-DO _не выгружается на prod_" %}

- нужны правки под стандарт написания
- отсутствуют параметры или поля
- не указаны типы параметров
- не указана обязательность параметров
- отсутствуют примеры
- отсутствует ответ в случае ошибки

{% endnote %}

{% endif %}

> Scope: [`базовый`](../../scopes/permissions.md)
>
> Кто может выполнять метод: любой пользователь

{% note alert %}

Метод `methods` устарел и в срок до 1 сентября 2022 года будет удалён. Настоятельно рекомендуется использовать метод [method.get](./method-get.md).

{% endnote %}

## Параметры

Без параметров - показ списка методов, доступных текущему приложению.

### Дополнительные параметры

#|
|| **Поле** | **Описание** ||
|| `full=true` | показ всех методов. ||
|| `scope=имя_разрешения` | показ методов, входящих в данное разрешение. Если указан параметр без значения (`methods?scope=&auth=xxxxx`), то будут выведены все общие методы. ||
|#

## Примеры

```http
https://my.bitrix24.ru/rest/methods?scope=&auth=d161f25928c3184678924ec127edd29a - показать все общедоступные методы.
```

{% include [Сноска о примерах](../../../_includes/examples.md) %}

## Ответ в случае успеха

> 200 OK
```json
{
    "result":[
        "scope",
        "methods",
        "batch",
        "user.admin",
        "user.access",
        "access.name"
    ]
}
```
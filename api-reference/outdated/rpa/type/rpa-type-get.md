# Получить информацию о процессе по идентификатору rpa.type.get

{% note warning "Мы еще обновляем эту страницу" %}

Тут может не хватать некоторых данных — дополним в ближайшее время

{% endnote %}

{% if build == 'dev' %}

{% note alert "TO-DO _не выгружается на prod_" %}

- отсутствуют примеры
- отсутствует ответ в случае ошибки

{% endnote %}

{% endif %}

> Scope: [`rpa`](../../../scopes/permissions.md)
>
> Кто может выполнять метод: любой пользователь

Метод `rpa.type.get` отдаёт информацию о процессе по его ID.

#|
|| **Параметр** / **Тип** | **Описание** ||
|| **id**^*^ 
[`number`](../../../data-types.md) | ID процесса. ||
|#

{% include [Сноска о параметрах](../../../../_includes/required.md) %}

## Ответ в случае успеха

> 200 OK

```json
{
    "type": {
        "id":1,
        "title":"Название процесса",
        "image":"list",
        "createdBy":1,
        "settings":[],
        "permissions":[
            {
                "id":"1",
                "entity":"TYPE",
                "entityId":"1",
                "accessCode":"UA",
                "action":"ITEMS_CREATE",
                "permission":"X"
            }
        ]
    }
}
```

- `title` - название процесса
- `image` - это идентификатор иконки из [списка](https://dev.1c-bitrix.ru/api_d7/bitrix/rpa/lib/ui/icon.php)
- `createdBy` - идентификатор пользователя, который создал процесс
- `settings` - набор настроек процесса
- `permissions` - набор настроек [прав доступа](https://dev.1c-bitrix.ru/api_d7/bitrix/rpa/lib/model/permissiontable.php) этого процесса
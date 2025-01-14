# Удалить уведомления im.notify.delete

{% note warning "Мы еще обновляем эту страницу" %}

Тут может не хватать некоторых данных — дополним в ближайшее время

{% endnote %}

{% if build == 'dev' %}

{% note alert "TO-DO _не выгружается на prod_" %}

- нужны правки под стандарт написания
- не указаны типы параметров
- отсутствуют примеры
- не прописаны ссылки на несозданные ещё страницы

{% endnote %}

{% endif %}

> Scope: [`im`](../../scopes/permissions.md)
>
> Кто может выполнять метод: любой пользователь

Метод `im.notify.delete` удаляет уведомление.

#|
|| **Параметр** | **Пример** | **Описание** | **Ревизия** ||
|| **ID^*^**
[`unknown`](../../data-types.md) | `123` | Идентификатор уведомления | 18 ||
|| **TAG^*^**
[`unknown`](../../data-types.md) | `TEST` | Тег уведомления, уникальный в рамках системы. | 18 ||
|| **SUB_TAG^*^**
[`unknown`](../../data-types.md) | `SUB`\|`TEST` | Дополнительный тег, без проверки на уникальность | 18 ||
|#

{% include [Сноска о параметрах](../../../_includes/required.md) %}

{% note warning %}

Указывать нужно **один из трех** обязательных параметров на выбор: `ID` (идентификатор уведомления), `TAG` (тег уведомления) или `SUB_TAG` (дополнительный тег).

{% endnote %}

## Примеры

{% include [Пояснение о restCommand](../_includes/rest-command.md) %}

```php
$result = restCommand(
    'im.notify.delete',
    Array(
        'ID' => 13,
        'TAG' => 'TEST',
        'SUB_TAG' => 'SUB|TEST'
    ),
    $_REQUEST[
        "auth"
    ]
);
```

{% include [Сноска о примерах](../../../_includes/examples.md) %}

## Ответ в случае успеха

```json
{
    "result": true
}
```

**Результат выполнения**: `true` или ошибка.

## Ответ в случае ошибки

```json
{
    "error": "PARAMS_ERROR",
    "error_description": "Ошибка удаления уведомления"
}
```

### Описание ключей**:

- `error` – код возникшей ошибки
- `error_description` – краткое описание возникшей ошибки

### Возможные коды ошибок

#|
|| **Код** | **Описание** ||
|| **PARAMS_ERROR** | Ошибка удаления уведомления ||
|#

## Ссылки по теме

[Как работать с вложениями](http://dev.1c-bitrix.ru/learning/course/index.php?COURSE_ID=93&CHAPTER_ID=07681)
# Получить информацию о доступности функционала на портале feature.get

{% note warning "Мы еще обновляем эту страницу" %}

Тут может не хватать некоторых данных — дополним в ближайшее время

{% endnote %}

{% if build == 'dev' %}

{% note alert "TO-DO _не выгружается на prod_" %}

- нужны правки под стандарт написания
- не указана обязательность параметров
- отсутствуют примеры
- отсутствует ответ в случае ошибки

{% endnote %}

{% endif %}

> Scope: [`базовый`](../../scopes/permissions.md)
>
> Кто может выполнять метод: любой пользователь

Метод `feature.get` возвращает информацию о доступности функционала на конкретном портале.

## Параметры

#|
|| **Параметр** | **Описание** ||
|| **CODE**
[`string`](../../data-types.md) | Доступные ключи:
- rest_offline_extended - доступность офлайн событий
- rest_auth_connector - доступность ключа auth_connector в событиях ||
|#

## Примеры

```js
$result[] = CRest::call(
    'feature.get',
    [
        'CODE' => 'rest_offline_extended',
    ]
);
```

{% include [Сноска о примерах](../../../_includes/examples.md) %}

## Ответ в случае успеха

> 200 OK
```json
'result' =>
    [
        'value' => 'Y'
    ]
```

### Возвращаемые данные

- `value Y` - наличие функционала на портале. Y - есть на текущем портале, N - нет на портале
- `lang_selfhosted`, где lang заменяется на en, ru, ua, kz и т.д. (для коробок Битрикс24).


# Проверить существование потока tasks.flow.flow.isExists

{% note warning "Мы еще обновляем эту страницу" %}

Тут может не хватать некоторых данных — дополним в ближайшее время

{% endnote %}

> Scope: [`task`](../../scopes/permissions.md)
>
> Кто может выполнять метод: любой пользователь

Метод `tasks.flow.flow.isExists` проверяет, существует ли поток с указанным именем. Если указан `id`, проверяет, существуют ли потоки с таким же именем, кроме указанного.

## Параметры метода

#|
|| **Название** `тип` | **Описание** ||
|| **flowData^*^** [`object`](../../data-types.md) | Объект с данными для проверки существования потока ||
|| **name^*^** [`string`](../../data-types.md) | Название потока, которое нужно проверить ||
|| **id** [`integer`](../../data-types.md) | Идентификатор потока для исключения из проверки (необязательный). Получить id можно при помощи метода [tasks.task.get](../tasks-task-get.md) для задачи, уже добавленной в поток, либо создать новый поток при помощи метода [tasks.flow.flow.create](./tasks-flow-flow-create.md) ||
|#

## Примеры кода

{% list tabs %}

- JS
    ```js
    BX24.callMethod(
        'tasks.flow.flow.isExists',
        {
            flowData: {
                name: 'Flow Name'
            }
        },
        function(result) {
            if (result.error()) {
                console.error(result.error());
            } else {
                console.info(result.data());
            }
        }
    );
    ```

- cURL (oAuth)
    ```bash
    curl -X POST \
    -H "Content-Type: application/json" \
    -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
    -d '{
        "flowData": {
            "name": "Flow Name"
        }
    }' \
    https://your-domain.bitrix24.com/rest/tasks.flow.flow.isExists
    ```

- cURL (Webhook)
    ```bash
    curl -X POST \
    -H "Content-Type: application/json" \
    -d '{
        "flowData": {
            "name": "Flow Name"
        }
    }' \
    https://your-domain.bitrix24.com/rest/_USER_ID_/_CODE_/tasks.flow.flow.isExists
    ```

- PHP
    ```php
    require_once('crest.php'); // подключение CRest PHP SDK

    $flowData = [
        "name" => "Flow Name"
    ];

    // выполнение запроса к REST API
    $result = CRest::call(
        'tasks.flow.flow.isExists',
        [
            'flowData' => $flowData
        ]
    );

    // Обработка ответа от Битрикс24
    if ($result['error']) {
        echo 'Error: '.$result['error_description'];
    } else {
        print_r($result['result']);
    }
    ```

{% endlist %}

## Обработка ответа

HTTP-статус: **200**

```json
{
"result": {
    "exists": true
}
}
```

### Возвращаемые данные

#|
|| **Название** `тип` | **Описание** ||
|| **result** [`object`](../../data-types.md) | Объект с результатом операции ||
|| **exists** [`boolean`](../../data-types.md) | Существует ли поток с указанным именем ||
|#

## Обработка ошибок

HTTP-статус: **200**

```json
{
    "error": "0",
    "error_description": "Flow not found"
}
```

### Возможные коды ошибок

#|
|| **Код** | **Описание** | **Дополнительная информация** ||
|| `0` | Доступ запрещён или поток не найден | Возможно, тариф портала не позволяет работать с потоками, или у пользователя нет прав на выполнение проверки ||
|| `0` | Unknown error | Неизвестная ошибка ||
|#

{% include [системные ошибки](../../../_includes/system-errors.md) %}

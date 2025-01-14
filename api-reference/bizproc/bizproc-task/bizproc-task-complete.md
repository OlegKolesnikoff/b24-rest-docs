# Выполнить задания бизнес-процессов bizproc.task.complete

{% note warning "Мы еще обновляем эту страницу" %}

Тут может не хватать некоторых данных — дополним в ближайшее время

{% endnote %}

{% if build == 'dev' %}

{% note alert "TO-DO _не выгружается на prod_" %}

- надо собрать общую таблицу параметров, включая PARAMETERS
- подробности значений для PARAMETERS и STATUS вынести в отдельные таблицы
- непонятно, откуда разработчик должен понимать, какие именно Fields он может или должен заполнить
- не хватает примеров
- нет стандартных блоков

{% endnote %}

{% endif %}

{% if build == 'dev' %}

{% note alert "TO-DO _не выгружается на prod_" %}

- нужны правки под стандарт написания
- не указаны типы параметров
- отсутствуют примеры
- отсутствует ответ в случае успеха
- отсутствует ответ в случае ошибки
- не прописаны ссылки на несозданные ещё страницы.

{% endnote %}

{% endif %}

> Scope: [`bizproc`](../../scopes/permissions.md)
>
> Кто может выполнять метод: любой пользователь

Метод осуществляет выполнение указанного задания бизнес-процесса. В настоящий момент можно выполнить задания вида:

- [Утверждение документа](https://dev.1c-bitrix.ru/learning/course/index.php?COURSE_ID=57&LESSON_ID=3771)
- [Ознакомление с документом](https://dev.1c-bitrix.ru/learning/course/index.php?COURSE_ID=57&LESSON_ID=3783)
- [Запрос доп. информации](https://dev.1c-bitrix.ru/learning/course/index.php?COURSE_ID=57&LESSON_ID=3782&LESSON_PATH=5442.5446.5035.7837.3782).
  
Выполнить можно только своё задание (относящееся к пользователю, с чьим access-токеном выполняется метод), если оно ещё не было выполнено.

#|
|| **Параметр** | **Описание** | **Примечание** | **С версии** ||
|| **TASK_ID^*^** | Идентификатор задания, обязательный | |  ||
|| **STATUS^*^** | Целевой статус задания, обязательный. Список допустимых значений: 

- `1` или yes - ответ "Да" (утвержден)
- `2` или no - ответ "Нет" (отклонен)
- `3` или ok - ответ "Ок" (ознакомлен)
- `4` или cancel - ответ "Отмена" | Статусы: **1** и **2** для действия Утверждение документа; <br> **3** и **4** для действия Запрос доп. информации; **3** для действия Запроса доп.информации с отклонением. |  ||
|| **COMMENT** | Комментарий пользователя, обязательность зависит от параметров задания | |  ||
|#

{% include [Сноска о параметрах](../../../_includes/required.md) %}

## Пример

```js
function completeTask(id, status, comment, cb)
{
    var params = {
        TASK_ID: id,
        STATUS: status,
        COMMENT: comment
    };
    BX24.callMethod(
        'bizproc.task.complete',
        params,
        function(result)
        {
            if(result.error())
                alert("Error: " + result.error());
            else if (cb)
                cb();
        }
    );
}
```

## Выполнение задания Запрос дополнительной информации через REST

С версии **20.0.800** модуля Бизнес-процессы появилась возможность выполнять задания **Запрос доп.информации** через rest метод **bizrpoc.task.complete**.

Для того, чтобы понять, какие поля нужно заполнить, в метод [bizproc.task.list](.) в PARAMETERS добавлено новое свойство `Fields` - массив с описанием полей.

```json
"PARAMETERS": {
    "CommentLabel": "Комментарий",
    "CommentRequired": "N",
    "ShowComment": "Y",
    "StatusOkLabel": "Сохранить",
    "Fields": [
        {
            "Type": "datetime",
            "Name": "date",
            "Description": "",
            "Multiple": false,
            "Required": true,
            "Options": null,
            "Settings": null,
            "Default": "2020-07-08T15:16:12+02:00",
            "Id": "date"
        }
    ]
}
```

Значения **по умолчанию** хранятся в разделе **Default**. Значения конвертируются во "внешнее" представление (для дат - в формат rest ATOM (ISO-8601), а для файлов - в ссылку на файл).

Далее значения этих полей нужно передать в метод **bizrpoc.task.complete** в параметре **Fields**. Значения конвертируются в этот раз во "внутреннее представление" (т.е. даты из rest формата конвертируются во внутренний, а файлы из rest сохраняются и прикрепляются к бизнес-процессу).

 {% include [Сноска о примерах](../../../_includes/examples.md) %}
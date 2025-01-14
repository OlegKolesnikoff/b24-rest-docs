# Добавить коммерческое предложение crm.quote.add

{% note warning "Мы еще обновляем эту страницу" %}

Тут может не хватать некоторых данных — дополним в ближайшее время

{% endnote %}

{% if build == 'dev' %}

{% note alert "TO-DO _не выгружается на prod_" %}

- нужны правки под стандарт написания
- не указаны типы параметров
- не указана обязательность параметров
- отсутствуют примеры (должно быть три примера - curl, js, php)
- отсутствует ответ в случае ошибки
- отсутствует ответ в случае успеха
- сделать ссылку [crm.requisite.link.register] на страницу с методом https://dev.1c-bitrix.ru/rest_help/crm/requisite/methods/crm_requisite_link_register.php

{% endnote %}

{% endif %}

> Scope: [`crm`](../../scopes/permissions.md)
>
> Кто может выполнять метод: любой пользователь

Метод `crm.quote.add` создаёт новое коммерческое предложение. Если необходимо в предложении указать какие реквизиты покупателя/продавца (т.к. их может быть несколько у компании), то используйте метод [crm.requisite.link.register](../requisites/links/crm-requisite-link-register.md).

В создаваемом предложении обязательно должны быть указаны компании продавца и покупателя:
- `COMPANY_ID`, если покупатель - компания или `CONTACT_ID`, если покупатель - контакт.
- `MYCOMPANY_ID` - продавец. 
  
Идентификаторы, указанные в **crm.requisite.link.register** и в создаваемом предложении, должны соответствовать покупателю и продавцу.

#|
||  **Параметр** / **Тип**| **Описание** ||
|| **fields**
[`unknown`](../../data-types.md) | Набор полей - массив вида `array("поле"=>"значение"[, ...])`, содержащий значения полей предложения, где "поле" может принимать значения из возвращаемых методом [crm.quote.fields](./crm-quote-fields.md).

{% note info %}

Чтобы узнать требуемый формат полей, выполните метод [crm.quote.fields](./crm-quote-fields.md) и посмотрите формат пришедших значений этих полей. 

{% endnote %}

||
|#

## Пример

```js
BX24.callMethod(
    "crm.quote.add",
    {
        fields:
        {
            "TITLE": "Черновик",
            "STATUS_ID": "DRAFT",
            "OPENED": "Y",
            "ASSIGNED_BY_ID": 1,
            "CURRENCY_ID": "USD",
            "OPPORTUNITY": 5000,
            "COMPANY_ID": 1,
            "COMMENTS": "Новое коммерческое предложение.",
            "BEGINDATE": "2016-03-01T12:00:00",
            "CLOSEDATE": "2016-04-01T12:00:00"
        }
    },
    function(result)
    {
        if(result.error())
            console.error(result.error());
        else
            console.info("Создано предложение с ID " + result.data());
    }
);
```

{% include [Сноска о примерах](../../../_includes/examples.md) %}
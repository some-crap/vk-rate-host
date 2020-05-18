# рейтинг хостеров (Сервис Вконтакте)

## API, использующее приложение

Все запросы делать по адресу PASTE_URL. Обязательные GET параметры в каждом из методов:

| name | default | description |
| ----- | ---- | ------ |
| method | **Required** | Имя метода |
| vk_params | **Required** | Все параметры, отдаваемые ВК |

- Любой метод **обязан** возвращать JSON

- Дополнительные параметры в методах посылаются через **POST** метод

## Ошибки в методах
В случае, если в методе произошла ошибка, возвращается объект со свойствами error и error_code:
```
{
    "error": {
        "code": number,
        "message": string,
        "description": string
    }
}

### app.init - при первом запуске

- Возвращает: 

```
{
    "user_type": "user" | "hoster",
    //вроде больше и не надо
}
```

### rating.Get - получения полного? списка лидеров

нужны офсеты

- Возвращает:

```
{
    "hoster_id": number,
    "hoster_name": string,
    "hoster_site": string,
    "rating": number, //как у кинопоиска по 10 балов? может быть дробным
}[] // - массив
```

### hosterComments.GetComments - получение всех комментов по хостеру

Параметры:

| name | type | default | description |
| ----- | ---- | ------ |
| hoster_id | number | **Required** | Имя метода |


нужны офсеты

- Возвращает:

Свой коммент отображать в самом верху.

```
{
    "id": number, // думаю что лучше сократить с comment_id на id (хотя как тебе удобней все так давай),
    "user_id": number,
    "user_full_name": string,
    "reputation": number, // репутатиция, при отрицательном значении будет полускрыто (ща пример скину)
    "answers": {
        "is_hoster": boolean, // хз, однако ответ хостеров должен быть выше всех по идеи и будет пометка "Ответ хостера"
        "id": number, // ??
        "user_id": number,
        "user_full_name": string,
        "reputation": number,// хостера тоже можно будет завалить репутацией?) 
    }[]
}[] //массив
```

### hosterComments.Add - написать коммент

Параметры:

| name | type | default | description |
| ----- | ---- | ------ |
| hoster_id | number | **Required** | К какому хостингу шлем коммент |
| comment_id | number | не обязателен | Шлем только в том случае, если отвечаем на коммент |
| content | string | **Required** | Сам отзыв |

 - Ничего не возвращает
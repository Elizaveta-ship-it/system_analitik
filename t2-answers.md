# Требования к функции "Получение списка магазинов при переходе на экран выбора"

1. При переходе пользователя на экран выбора магазинов приложение должно инициировать GET-запрос к серверу.
2. Бэкенд обрабатывает запрос и возвращает JSON-объект, содержащий данные для отрисовки (рендеринга) интерфейса.
3. Ответ сервера представляет собой массив магазинов, где каждый элемент содержит следующие атрибуты:
   * название магазина (для отображения);
   * ссылка на логотип;
   * ближайший доступный интервал доставки;
   * внешняя ссылка (URL) для перехода по клику на плашку.
4. Список магазинов на экране должен быть отсортирован в алфавитном порядке по их названию.



## Пример REST API запроса:

```bash
https://petzel.ru/api/v1/stores
Accept: application/json
```

## Ответа:

```bash
{
  "stores": [
    {
      "name": "METRO",
      "logo": "https://petzel.ru/images/logos/metro.png",
      "nearest_delivery_window": {
        "start": "2026-01-06T21:00:00+03:00",
        "end": "2026-01-06T23:00:00+03:00"
      },
      "external_link": "https://metro.ru"
    },
    {
      "name": "Ашан",
      "logo": "https://petzel.ru/images/logos/auchan.png",
      "nearest_delivery_window": {
        "start": "2026-01-06T18:00:00+03:00",
        "end": "2026-01-06T20:00:00+03:00"
      },
      "external_link": "https://auchan.ru"
    },
    {
      "name": "ВкусВилл",
      "logo": "https://petzel.ru/images/logos/vkusvill.png",
      "nearest_delivery_window": {
        "start": "2026-01-06T00:20:00+03:00",
        "end": "2026-01-06T01:00:00+03:00"
      },
      "external_link": "https://vkusvill.ru"
    },
    {
      "name": "ВИКТОРИЯ",
      "logo": "https://petzel.ru/images/logos/victoria.png",
      "nearest_delivery_window": {
        "start": "2026-01-06T17:00:00+03:00",
        "end": "2026-01-06T19:00:00+03:00"
      },
      "external_link": "https://victoria.ru"
    }
  ]
}
```
## Примеры ошибок:

Код 404

```bash
{
  "error": {
    "code": "PARTNERS_NOT_FOUND",
    "message": "Для выбранного города нет доступных магазинов партнёров"
  }
}
```


Код 500

```bash
{
  "error": {
    "code": "INTERNAL_SERVER_ERROR",
    "message": "Внутренняя ошибка сервера. Попробуйте позже"
  }
}
```

Код 503

```bash
{
  "error": {
    "code": "SERVICE_UNAVAILABLE",
    "message": "Сервис магазинов временно недоступен. Повторите попытку"
  }
}
```


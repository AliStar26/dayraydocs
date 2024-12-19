# Фидбэк



Контроллер отзыва.

<details>
<summary>
Метод <code>GET /api/feedback</code>
</summary>

Извлекает полный список отзывов через сервис.


Response
```json
[
  {
    "id": 1,
    "userId": 101,
    "message": "Отличный сервис!",
    "rating": 5,
    "createdDate": "2024-12-17T10:00:00Z"
  },
  {
    "id": 2,
    "userId": 102,
    "message": "Нужны улучшения.",
    "rating": 3,
    "createdDate": "2024-12-16T15:30:00Z"
  }
]
```
</details>

<details>
<summary>
Метод <code>GET /api/feedback/id</code>
</summary>

Если отзыв с указанным идентификатором существует, возвращает его данные. В противном случае возвращает 404 Not Found



Response
```json
{
  "id": 1,
  "userId": 101,
  "message": "Отличный сервис!",
  "rating": 5,
  "createdDate": "2024-12-17T10:00:00Z"
}
```
Пример ответа (ошибка):

```json
{
  "status": 404,
  "message": "Feedback not found"
}
```
</details>

<details>
<summary>
Метод <code>POST /api/feedback</code>
</summary>

Создаёт новый отзыв и возвращает его данные вместе с идентификатором.


Response
```json
{
  "userId": 103,
  "message": "Хорошее качество продукции!",
  "rating": 4
}
```
Пример ответа (успех):

```json

{
  "id": 3,
  "userId": 103,
  "message": "Хорошее качество продукции!",
  "rating": 4,
  "createdDate": "2024-12-17T11:00:00Z"
}
```

</details>
# Заказы



Контроллер заказа.

<details>
<summary>
Метод <code>GET /api/order/id</code>
</summary>


Извлекает данные заказа по идентификатору. Если заказ не найден, возвращает 404 Not Found.

Response(Sucess)
```json
{
  "id": 1,
  "userId": 101,
  "items": [
    { "productId": 10, "quantity": 2 },
    { "productId": 12, "quantity": 1 }
  ],
  "totalAmount": 1500.0,
  "status": "Pending",
  "createdDate": "2024-12-17T10:00:00Z"
}
```
Response(Error)
```json
{
  "status": 404,
  "message": "Order not found"
}
```
</details>

<details>
<summary>
Метод <code>GET /api/order</code>
</summary>

Извлекает полный список заказов.

Response
```json
[
  {
    "id": 1,
    "userId": 101,
    "totalAmount": 1500.0,
    "status": "Pending",
    "createdDate": "2024-12-17T10:00:00Z"
  },
  {
    "id": 2,
    "userId": 102,
    "totalAmount": 2000.0,
    "status": "Completed",
    "createdDate": "2024-12-16T15:30:00Z"
  }
]
```
</details>

<details>
<summary>
Метод <code>POST /api/order/create-order</code>
</summary>

Создаёт новый заказ и возвращает его идентификатор.



Response
```json
{
  "userId": 101,
  "items": [
    { "productId": 10, "quantity": 2 },
    { "productId": 12, "quantity": 1 }
  ],
  "totalAmount": 1500.0
}
```
</details>
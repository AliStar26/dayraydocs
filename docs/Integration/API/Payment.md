# Платеж



<details>
<summary>
Метод <code>POST /api/payment/process-payment</code>
</summary>

Обрабатывает платёж и возвращает идентификатор нового платежа.



Пример тела json запроса:
```json
{
  "orderId": 101,
  "amount": 1500.0,
  "paymentMethod": "CreditCard"
}
```
Response
```json
{
  "id": 1
}
```
</details>

<details>
<summary>
Метод <code> GET /api/payment/id</code>
</summary>

Извлекает данные о платеже. Если платёж не найден, возвращает 404 Not

Пример тела json запроса:
```json
{
 "orderId": 101,
  "amount": 1500.00,
  "quantity": 2,
  "address": "123 Main Street, Springfield",
  "cardName": "John Doe",
  "cardNumber": "4111111111111111",
  "cardExpiry": "12/25",
  "cardCVV": "123"
}
```
Response
```json
{
  "status": 404,
  "message": "Payment not found"
}
```
</details>




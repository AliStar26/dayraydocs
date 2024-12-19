# Корзина



<details>
<summary>
Метод <code>GET /api/cart</code>
</summary>

Извлекает идентификатор пользователя из токена JWT и возвращает содержимое корзины пользователя.



Response

```json
{
  "items": [
    { "productId": 1, "name": "Товар 1", "quantity": 2 },
    { "productId": 2, "name": "Товар 2", "quantity": 1 }
  ],
  "totalPrice": 3500
}
```

</details>

<details>
<summary>
Метод <code>POST /api/cart/add</code>
</summary>

Использует идентификатор пользователя из токена для добавления товара в корзину.

```json
{
  "productId": 1,
  "quantity": 3
}
```

Response
```json
{
  "message": "Товар успешно добавлен в корзину."
}
```

</details>

<details>
<summary>
Метод <code>POST /api/cart/remove</code>
</summary>

Использует идентификатор пользователя из токена для удаления товара из корзины.


```json
{
  "productId": 2
}
```

Response

```json
{
   "message": "Товар успешно удален из корзины."

}
```

</details>

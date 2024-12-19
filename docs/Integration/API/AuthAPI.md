# Авторизация

> `/api/Auth`

Ниже представлена документация для контроллера AccountController, который предоставляет функционал управления учетными записями, аутентификации и авторизации.

<details>
<summary>
Метод <code>/api/account/register</code>
</summary>

|                       |                                 |
| :-------------------- | :------------------------------ |
| Тип запроса           | POST                            |


Пример тела json запроса:

```json

{
  "username": "testuser",
  "email": "test@example.com",
  "password": "P@ssword1"
}

```

Response

```json
{
  "message": "User registered successfully"
}
```

</details>

Аутентифицирует пользователя и выдает JWT токен.



<details>
<summary>
Метод <code>/api/account/login</code>
</summary>

|                       |                                 |
| :-------------------- | :------------------------------ |
| Тип запроса           | POST                            |


Пример тела json запроса:

```json

{
  "username": "testuser",
  "password": "P@ssword1"
}

```

Response

```json
{
   "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "userId": 1
}
```

</details>


Метод для обработки выхода пользователя (в текущей реализации выполняет только возврат статуса).


<details>
<summary>
Метод <code>/api/account/logout</code>
</summary>

|                       |                                 |
| :-------------------- | :------------------------------ |
| Тип запроса           | POST                            |




Response

```json
{
  "message": "Logout successful"
}
```

</details>
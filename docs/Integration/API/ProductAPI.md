# Продукты
>```/api/Product```

Контроллер продуктов.

<details>
<summary>
Метод <code>GET api/products/id</code>
</summary>
Получение информации о продукте по его ID.



Пример тела json запроса: 
```json  
{
  "id": 1,
  "name": "Product Name",
  "categoryId": 2,
  "price": 100.00
}
```

</details>
<details>
<summary>
Метод <code>GET api/products</code>
</summary>

 Получение списка продуктов с возможностью фильтрации по запросу.

```csharp
public async Task<ActionResult<IEnumerable<ProductDto>>> GetProducts([FromQuery] string? query)```
query (тип string?) — строка для поиска продуктов по названию.

Пример запроса:
GET api/products?query=laptop
Пример ответа:
```json
[
  {
    "id": 1,
    "name": "Product Name",
    "categoryId": 3,
    "price": 1200.00
  },
  {
    "id": 2,
    "name": "Product Name",
    "categoryId": 4,
    "price": 50.00
  }
]
```
</details>

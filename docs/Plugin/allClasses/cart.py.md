#### cart.py

## Используется для отображения товаров, добавленных в корзину.

```py
@cart_bp.route('/cart', methods=['GET'])
def view_cart():
    token = session.get('token')  # Токен для авторизации
    if not token:
        return redirect(url_for('login'))  # Перенаправляем на страницу логина, если токен отсутствует

    headers = {'Authorization': f'Bearer {token}'}
    try:
        response = requests.get(API_BASE_URL, headers=headers)
        response.raise_for_status()  # Проверяем статус ответа
        cart_data = response.json()  # Парсим JSON-ответ

        # Логируем данные для проверки
        print(cart_data)  # Это поможет увидеть структуру ответа

        # Переход к шаблону с корректными данными
        cart_items = cart_data.get('cartItems', [])  # Получаем cartItems как список
        total = sum(
    (item.get('productPrice', 0) * item.get('quantity', 0))
    for item in cart_items
)
        return render_template('cart.html', cart_data=cart_items, total=total)
    except requests.RequestException as e:
        print(f"Ошибка получения корзины: {e}")
        return "Ошибка загрузки корзины", 500



# Добавление товара в корзину
@cart_bp.route('/add_to_cart', methods=['POST'])
def add_to_cart():
    token = session.get('token')
    if not token:
        return redirect(url_for('login'))

    product_id = request.form.get('product_id')
    quantity = request.form.get('quantity', 1)
    headers = {'Authorization': f'Bearer {token}'}
    params = {'productId': product_id, 'quantity': quantity}

    try:
        response = requests.post(f"{API_BASE_URL}/add", headers=headers, params=params)
        response.raise_for_status()
        return redirect(url_for('cart.view_cart'))
    except requests.RequestException as e:
        print(f"Ошибка добавления в корзину: {e}")
        return "Ошибка добавления в корзину", 500


# Удаление товара из корзины
@cart_bp.route('/remove_from_cart', methods=['POST'])
def remove_from_cart():
    token = session.get('token')
    if not token:
        return redirect(url_for('login'))

    product_id = request.form.get('product_id')

    headers = {'Authorization': f'Bearer {token}'}
    data = {'productId': product_id}

    try:
        response = requests.post(f"{API_BASE_URL}/clear", headers=headers)
        response.raise_for_status()
        return redirect(url_for('cart.view_cart'))
    except requests.RequestException as e:
        print(f"Ошибка удаления из корзины: {e}")
        return "Ошибка удаления из корзины", 500


# Очистка корзины
@cart_bp.route('/clear_cart', methods=['POST'])
def clear_cart():
    token = session.get('token')
    if not token:
        return redirect(url_for('login'))

    headers = {'Authorization': f'Bearer {token}'}
    try:
        response = requests.post(f"{API_BASE_URL}/clear", headers=headers)
        response.raise_for_status()
        return redirect(url_for('cart.view_cart'))
    except requests.RequestException as e:
        print(f"Ошибка очистки корзины: {e}")
        return "Ошибка очистки корзины", 500


@cart_bp.route('/checkout', methods=['POST'])
def checkout():
    token = session.get('token')
    if not token:
        return redirect(url_for('login'))  # Перенаправляем на логин, если токен отсутствует

    headers = {'Authorization': f'Bearer {token}'}

    try:
        # Получаем данные корзины для создания заказа
        response = requests.get(API_BASE_URL, headers=headers)
        response.raise_for_status()
        cart_data = response.json()

        # Формируем данные для заказа
        order_items = [
            {
                "productId": item["productId"],
                "quantity": item["quantity"],
                "price": item["productPrice"]
            }
            
            for item in cart_data.get('cartItems', [])
        ]
        total = sum(
            (item["productPrice"] * item["quantity"])
            for item in cart_data.get('cartItems', [])
        )
        print(f"print(order_items){order_items}")

        order_data = {
            "userId": session.get("user_id"),  # Используем ID пользователя из сессии
            "orderItems": order_items
        }
        quantity = sum((item["quantity"])for item in cart_data.get('cartItems', []))
        print(f"quant : {quantity}")

        
        # Отправляем запрос на API для создания заказа
        order_response = requests.post("http://localhost:5107/api/Order/create-order", json=order_data)
        order_response.raise_for_status()

        # Получаем ID созданного заказа
        order_id = order_response.json()
        return render_template('pay.html', order_id=order_id, total=total, quantity = quantity)

    except requests.RequestException as e:
        print(f"Ошибка при создании заказа: {e}")
        return "Ошибка при создании заказа", 500
```

| Маршрут | Метод| Описание|Ответ|
| :--- | :--- | :---| :--- 
| /cart | GET	 | Отображает содержимое корзины пользователя. | HTML-страница с корзиной (cart.html), содержащей товары и общую сумму.
| /add_to_cart | POST |Добавляет товар в корзину.|Перенаправляет на маршрут /cart или возвращает ошибку.
| /remove_from_cart	 | POST | Удаляет конкретный товар из корзины.| Перенаправляет на маршрут /cart или возвращает ошибку.
| /clear_cart	 | POST | Очищает корзину пользователя.| Перенаправляет на маршрут /cart или возвращает ошибку.
| /checkout	 | POST | Оформляет заказ с текущим содержимым корзины.| HTML-страница для оплаты (pay.html), включающая данные заказа: order_id, total, quantity.

#### product_detail

## Этот код обрабатывает запросы на получение информации о продукте по его идентификатору, отправку отзыва о продукте, а также обработку добавления товара в корзину с учетом количества.


```py
@product_detail_bp.route('/product/<int:id>', methods=['GET', 'POST'])
def product_details(id):
    API_URL = current_app.config['API_URL']
    PRODUCT_API_URL = f"{API_URL}/Products/{id}"
    FEEDBACK_API_URL = f"{API_URL}/Feedback"

    # Запрос на получение данных о продукте
    try:
        response = requests.get(PRODUCT_API_URL)
        response.raise_for_status()
        product = response.json()
    except requests.exceptions.RequestException as e:
        print(f"Ошибка при запросе API: {e}")
        product = None
        error_message = "Не удалось загрузить данные о продукте. Попробуйте позже."
        return render_template('product_details.html', product=product, error_message=error_message)

    # Обработка отправки отзыва
    if request.method == 'POST':
        # Проверка на добавление отзыва
        if 'rating' in request.form and 'comment' in request.form:
            rating = request.form['rating']
            comment = request.form['comment']
            user_id = session.get("user_id")

            feedback_data = {
                'productId': id,
                'rating': rating,
                'comment': comment,
                'userId': user_id
            }

            try:
                response = requests.post(FEEDBACK_API_URL, json=feedback_data)
                response.raise_for_status()
                feedback_message = "Отзыв успешно отправлен!"
            except requests.exceptions.RequestException as e:
                print(f"Ошибка при отправке отзыва: {e}")
                feedback_message = "Произошла ошибка при отправке отзыва. Попробуйте снова позже."

            return render_template('product_details.html', product=product, feedback_message=feedback_message)

        # Обработка отправки формы для добавления в корзину
        elif 'quantity' in request.form:
            quantity = int(request.form['quantity'])

            # Проверяем, что количество не превышает доступное
            if quantity > product['count']:
                error_message = f"Вы не можете выбрать больше {product['count']} товаров."
                return render_template('product_details.html', product=product, error_message=error_message)

            # Здесь можно продолжить процесс добавления товара в корзину (например, через API или сессию)

    return render_template('product_details.html', product=product)
```


| Classes | |
| :--- | :--- |
| product_detail_bp | Контроллер для обработки запроса на получение данных о продукте и отправки отзыва |
| product_details | Функция для отображения данных о продукте, отправки отзыва и добавления товара в корзину |

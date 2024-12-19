#### products.py

## Этот код обрабатывает запросы на получение списка продуктов, фильтруя их по параметру поиска, и отображает их на странице.

```py
@products_bp.route('/products')
def products():
    API_URL = current_app.config['API_URL']
    PRODUCTS_API_URL = API_URL + "/Products"

    query = request.args.get('query', '')  # Получаем параметр поиска из URL

    # Добавляем параметр поиска в запрос к API
    try:
        response = requests.get(PRODUCTS_API_URL, params={"query": query})
        response.raise_for_status()
        products = response.json()
    except requests.exceptions.RequestException as e:
        print(f"Ошибка при запросе API: {e}")
        products = []
        error_message = "Не удалось загрузить продукты. Попробуйте позже."
        return render_template('products.html', products=products, error=error_message)
    
    return render_template('products.html', products=products)

```


| Classes | |
| :--- | :--- |
| products_bp | Контроллер для обработки запроса на получение продуктов |
| products | Функция для получения продуктов с учетом параметра поиска и отображения их на странице |

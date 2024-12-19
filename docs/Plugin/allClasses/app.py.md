# app.py

## Главный модуль приложения Flask, обрабатывает запрос на главную страницу, загружает категории из API и отображает их в шаблоне.



```py
@app.route('/')
def index():
    """
    Главная страница. Получает категории с API и передает их в шаблон.
    """
    try:
        # Запрос к API для получения категорий
        response = requests.get(CATEGORIES_API_URL)
        response.raise_for_status()
        categories = response.json()
    except requests.exceptions.RequestException as e:
        print(f"Ошибка при запросе API: {e}")
        categories = []
        error_message = "Не удалось загрузить категории. Попробуйте позже."
        return render_template('index.html', categories=categories, error=error_message)
    
    return render_template('index.html', categories=categories)
```


| Описание функциональности | |
| :--- | :--- |
| Flask Application| Главный модуль для запуска веб-приложения. Управляет маршрутизацией и регистрацией Blueprints. |
| Blueprints | Модули, обеспечивающие структуризацию приложения. |
| Config | Класс конфигурации приложения, содержащий параметры API и другие настройки. |
| Routes | Маршруты приложения, включая главную страницу и обработчики для интеграции с API. |

#### [registration.py](index 'index')

## Этот код отвечает за обработку запросов на страницу регистрации и отправку данных на сервер для регистрации нового пользователя.


```py
@registration_bp.route('/register', methods=['GET', 'POST'])
def register():
    API_URL = current_app.config['API_URL']  # URL вашего API
    REGISTER_API_URL = f"{API_URL}/Account/register"

    if request.method == 'POST':
        data = request.get_json()  # Получаем данные из формы

        # Проверяем, что все данные присутствуют
        if not data.get('username') or not data.get('phoneNumber') or not data.get('email') or not data.get('password'):
            return jsonify({'error': 'Все поля обязательны для заполнения'}), 400

        try:
            # Отправляем запрос на API для регистрации
            response = requests.post(REGISTER_API_URL, json=data)
            response.raise_for_status()

            if response.status_code == 200:
                return jsonify({'message': 'Регистрация успешна!'})
            else:
                return jsonify({'error': response.json().get('message', 'Ошибка регистрации')}), 400

        except requests.exceptions.RequestException as e:
            return jsonify({'error': str(e)}), 500

    return render_template('registration.html') 
```


| Classes | |
| :--- | :--- |
| registration_bp | Контроллер для регистрации пользователя
|register| Функция для обработки регистрации пользователя |

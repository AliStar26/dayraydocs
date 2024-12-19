#### login.py

## Этот код обрабатывает запросы на страницу входа, выполняет аутентификацию пользователя через API, сохраняет токен и userId в сессии, а также предоставляет возможность выхода из системы.

```py
@login_bp.route('/login', methods=['GET', 'POST'])
def login():
    API_URL = current_app.config['API_URL']
    LOGIN_API_URL = API_URL + "/Account/login"
    
    """
    Страница входа, обрабатывает форму и возвращает токен, если аутентификация успешна.
    """
    if request.method == 'POST':
        # Получаем данные из формы
        data = request.get_json()
        username = data.get('username')
        password = data.get('password')

        try:
            # Запрос к API для проверки данных
            response = requests.post(LOGIN_API_URL, json={'username': username, 'password': password})
            response.raise_for_status()  # Проверка на успешность запроса
        
            # Проверка на наличие токена в ответе
            if response.ok:
                # Сохраняем имя пользователя в session
                session['username'] = username
                session['token'] = response.json().get('token')
                session['user_id'] = response.json().get('userId')  # Сохраняем userId
                print(f"session['user_id'] {session['user_id']}")
                # Возвращаем ответ с токеном и именем пользователя
                return jsonify({'token': session['token'], 'username': session['username']})

        except requests.exceptions.RequestException as e:
            print(f"Ошибка при запросе API: {e}")
            return jsonify({'error': 'Неверный логин или пароль'}), 401

    return render_template('login.html')

@login_bp.route('/logout')
def logout():

    session.pop('username', None)    
    session.pop('customer_id', None)
    return redirect('/')
```


| Classes | |
| :--- | :--- |
| login_bp | Контроллер для обработки входа пользователя |
| login | Функция для обработки запроса на вход и сохранения токена и userId в сессии |
| logout | Функция для выхода пользователя и удаления данных сессии |

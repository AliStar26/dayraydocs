#### ai.py

## Код представляет собой Flask-приложение, в котором реализован функционал чат-бота


```py

@ai_bp.route('/chat', methods=['POST'])
def chat():
    data = request.get_json()
    if not data:
        logger.warning('No JSON data provided in chat request')
        return jsonify({"error": "No JSON data provided."}), 400

    user_message = data.get("message", "").strip()
    if not user_message:
        logger.warning('Empty message received in chat request')
        return jsonify({"error": "Message is empty."}), 400

    logger.info(f'Received chat request: {user_message}')

    # Генерируем ответ с помощью модели GPT
    try:
        answer = generate_answer(user_message)
        logger.info(f'Generated answer: {answer}')
        return jsonify({"reply": answer})
    except Exception as e:
        logger.error(f'Error generating answer: {e}')
        return jsonify({"reply": "Извините, произошла ошибка при обработке вашего запроса. Пожалуйста, попробуйте позже."})
```


| Маршрут | Метод| Описание|Ответ|
| :--- | :--- | :---| :--- 
| /chat | POST	 | 	Основной маршрут для взаимодействия с чат-ботом. Получает запрос от пользователя и возвращает ответ, основанный на базе знаний. |JSON-ответ с ключом reply, содержащим ответ от модели GPT. В случае ошибки возвращает сообщение об ошибке.



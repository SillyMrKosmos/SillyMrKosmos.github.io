<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <title>Minecraft Launcher</title>
    <!-- Подключаем Telegram API -->
    <script src="https://telegram.org/js/telegram-web-app.js"></script>
    <style>
        :root {
            --main-bg: #0a0a0a;
            --main-text: #00ff00;
            --button-bg: #1a1a1a;
            --button-hover: #003300;
        }
       
        body {
            margin: 0;
            font-family: 'Courier New', monospace;
            background-color: var(--main-bg);
            color: var(--main-text);
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            height: 100vh;
            text-align: center;
        }

        h1 {
            font-size: 2.5em;
            margin-bottom: 20px;
            text-shadow: 0 0 10px var(--main-text);
        }

        p {
            font-size: 1.2em;
            margin-bottom: 40px;
        }

        button {
            background-color: var(--button-bg);
            color: var(--main-text);
            border: 2px solid var(--main-text);
            padding: 15px 40px;
            font-size: 1.2em;
            font-weight: bold;
            border-radius: 50px; /* Скругленные кнопки */
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 0 15px rgba(0, 255, 0, 0.4);
        }

        button:hover {
            background-color: var(--button-hover);
            transform: scale(1.05);
        }

        button:active {
            transform: scale(0.98);
        }

        #status {
            margin-top: 30px;
            min-height: 20px;
            font-style: italic;
        }
    </style>
</head>
<body>

    <h1>⚡ Minecraft Launcher</h1>
    <p>Привет, <span id="username"></span>! Нажми кнопку, чтобы получить сборку.</p>
   
    <button id="getUpdateBtn">⬇️ Скачать актуальную сборку</button>
   
    <div id="status"></div>

    <script>
        const tg = window.Telegram.WebApp;
        tg.expand(); // Раскрываем на весь экран

        // Определяем пользователя
        const userId = tg.initDataUnsafe.user.id;
        const userName = tg.initDataUnsafe.user.first_name;
        document.getElementById('username').textContent = userName;

        // Настройка кнопки в шапке Telegram
        tg.MainButton.setText('Закрыть');
        tg.MainButton.onClick(() => tg.close());

        const btn = document.getElementById('getUpdateBtn');
        const status = document.getElementById('status');

        btn.onclick = async () => {
            btn.disabled = true;
            status.textContent = "📡 Запрашиваю файл у сервера...";

            try {
                const response = await fetch('http://ВАШ_ВНЕШНИЙ_IP:8080/api/get-update', {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({ user_id: userId })
                });

                const result = await response.json();

                if (result.status === "success") {
                    status.textContent = "✅ " + result.message;
                    btn.textContent = "✅ Готово!";
                    btn.style.backgroundColor = "#003300";
                } else if (result.status === "pending") {
                    status.textContent = "⏳ " + result.message;
                    btn.disabled = false;
                } else {
                    status.textContent = "❌ Ошибка: " + result.message;
                    btn.disabled = false;
                }
            } catch (error) {
                status.textContent = "❌ Нет связи с сервером. Проверьте IP.";
                btn.disabled = false;
            }
        };
    </script>
</body>
</html>

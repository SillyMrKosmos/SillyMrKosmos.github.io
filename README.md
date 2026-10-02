<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <title>Launcher</title>
    <script src="https://telegram.org/js/telegram-web-app.js"></script>
    <style>
        /* Сброс стилей браузера */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        :root {
            --bg: #000000;
            --text: #ffffff;
            --border: #ffffff;
            --btn-bg: #ffffff;
            --btn-text: #000000;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
            background-color: var(--bg);
            color: var(--text);
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            height: 100vh;
            text-align: center;
            line-height: 1.4;
        }

        h1 {
            font-size: 24px;
            font-weight: 700;
            letter-spacing: 1px;
            text-transform: uppercase;
            margin-bottom: 10px;
            opacity: 0.8;
        }

        p {
            font-size: 16px;
            max-width: 80%;
            margin-bottom: 50px;
            opacity: 0.6;
        }

        #getUpdateBtn {
            /* Квадратная кнопка без скруглений */
            width: 220px;
            height: 60px;
            border: 1px solid var(--border);
            background-color: var(--btn-bg);
            color: var(--btn-text);
            font-size: 15px;
            font-weight: 500;
            cursor: pointer;
            transition: all 0.2s ease;
        }

        #getUpdateBtn:hover {
            background-color: var(--bg);
            color: var(--text);
        }

        #getUpdateBtn:active {
            transform: translateY(1px);
        }

        #status {
            margin-top: 40px;
            font-size: 14px;
            font-family: "Courier New", Courier, monospace;
            opacity: 0.5;
            min-height: 16px;
        }

        /* Стиль для отключенной кнопки (полупрозрачность) */
        button:disabled {
            opacity:

On Fri, Oct 2, 2026 at 8:49 AM Давид Гельвер <gelverdavid6@gmail.com> wrote:
Your ID: 8548628409
Current chat ID: 8548628409

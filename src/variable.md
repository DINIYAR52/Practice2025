# Вариативная часть задания: Создание Telegram-бота для отображения футбольной статистики «Media Football League»

## Введение

В данном документе описана пошаговая инструкция по созданию Telegram-бота, который отображает статистические данные футбольной лиги «Media Football League». В качестве основы использованы открытые источники данных и API, а также пример кода на Python. Руководство предназначено для начинающих разработчиков, желающих освоить создание чат-ботов и работу с API.

---

## 1. Исследование предметной области и подготовка

### 1.1. Изучение предметной области

- Ознакомьтесь с правилами и структурой лиги «Media Football League»: команды, матчи, статистика.
- Определите ключевые метрики, которые хотите отображать (например, таблица команд, результаты матчей, статистика игроков).

### 1.2. Поиск источников данных

- Найдите открытые API или сайты с API, предоставляющие футбольную статистику.
- В нашем случае, предположим, что у «Media Football League» есть API или мы используем публичные статистические ресурсы, такие как [football-data.org](https://football-data.org/).

### 1.3. Анализ API и подготовка данных

- Получите API-ключ, если требуется.
- Проведите тестовые запросы к API для получения данных о командах, матчах и результатах.
  
## 2. Создание Telegram-бота: пошаговая инструкция

### 2.1. Регистрация бота в Telegram

1. Откройте Telegram и найдите бота [@BotFather](https://telegram.me/BotFather).
2. Отправьте команду `/newbot`.
3. Следуйте инструкциям: введите название бота и выберите уникальное имя пользователя.
4. Получите токен API — он понадобится для взаимодействия с Telegram API.

### 2.2. Установка необходимых инструментов

- Установите Python (если еще не установлен).
- Установите библиотеку `python-telegram-bot`:

### 2.3. Создание файла бота и подключение к API

Создайте файл `football_bot.py` и вставьте следующий пример кода:
python
import logging
from telegram import Update
from telegram.ext import ApplicationBuilder, CommandHandler, ContextTypes
import requests

Вставьте сюда ваш токен, полученный от BotFather
TOKEN = 'ВАШТОКЕНЗДЕСЬ'
Настройка логгирования
logging.basicConfig(
format='%(asctime)s - %(name)s - %(levelname)s - %(message)s',
level=logging.INFO
)
Обработчик команды /start
async def start(update: Update, context: ContextTypes.DEFAULTTYPE):
await update.message.replytext(
"Привет! Я бот для отображения футбольной статистики 'Media Football League'.\n"
"Используйте команду /standings, чтобы получить текущую таблицу команд."
)
Обработчик команды /standings
async def standings(update: Update, context: ContextTypes.DEFAULTTYPE):
Отправляем запрос к API
headers = {'X-Auth-Token': 'ВАШAPIКЛЮЧ'}
response = requests.get('https://api.football-data.org/v4/competitions/PL/standings', headers=headers)
if response.statuscode == 200:
data = response.json()
Обработка данных и создание сообщения
message = "Текущая таблица команд:\n"
for team in data'standings'0'table':
position = team'position'
teamname = team'team''name'
points = team'points'
message += f"{position}. {teamname} - {points} очков\n"
await update.message.replytext(message)
else:
await update.message.replytext("Не удалось получить данные. Попробуйте позже.")
Основная функция
def main():
app = ApplicationBuilder().token(TOKEN).build()
app.add_handler(CommandHandler('start', start))
app.add_handler(CommandHandler('standings', standings))
Copy
print("Бот запущен")
app.run_polling()
Copy
if name == 'main':
main()

### 2.4. Запуск бота

- Замените `'ВАШ_ТОКЕН_ЗДЕСЬ'` и `'ВАШ_API_КЛЮЧ'` на ваши реальные токены.
- Запустите скрипт:
bash
python footballbot.py

- В Telegram найдите вашего бота и отправьте команду `/start` и `/standings`.

## 3. Расширение функционала

- Добавьте команды для отображения результатов матчей, статистики игроков.
- Используйте дополнительные API или базы данных для более подробных данных.
- Реализуйте обработку ошибок и логирование.

---

## 4. Итог

Создание Telegram-бота для отображения футбольной статистики — это интересный и полезный проект, который помогает освоить работу с API, создание чат-ботов и основы программирования на Python. Следуя данной инструкции, даже начинающий разработчик сможет реализовать собственный бот и расширять его функциональность.

1. **Диаграмма взаимодействия бота с API**  
   ![Диаграмма](https://techdiy.info/wp-content/uploads/2022/10/what-is-the-difference-between-connection-timeout-and-connection-refused-1000x600.png)

2. **Регистрация бота в BotFather**  
   ![Скриншот](https://avatars.mds.yandex.net/i?id=0a0f18a7668044d2c084df9698f953686aa8eb3b-5178044-images-thumbs&n=13)

3. **Установка библиотеки `python-telegram-bot`**  
   ![Скриншот](https://avatars.mds.yandex.net/i?id=f38458a95c421081538b3da9b3213d0b5a69d43e46f897ac-12421090-images-thumbs&n=13)

4. **Диалог с ботом в Telegram**  
   ![Скриншот](blob:https://web.telegram.org/b6ce0d01-2472-4ed5-b118-1c135b6fb5b8)

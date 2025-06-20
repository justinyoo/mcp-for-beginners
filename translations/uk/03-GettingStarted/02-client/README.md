<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "2342baa570312086fc19edcf41320250",
  "translation_date": "2025-06-17T16:38:42+00:00",
  "source_file": "03-GettingStarted/02-client/README.md",
  "language_code": "uk"
}
-->
У наведеному вище коді ми:

- Імпортували бібліотеки
- Створили екземпляр клієнта та підключили його, використовуючи stdio як транспорт.
- Вивели списки промптів, ресурсів і інструментів та викликали їх усі.

Ось і все, клієнт, який може спілкуватися з MCP Server.

У наступному розділі вправ ми детально розберемо кожен фрагмент коду та пояснимо, що відбувається.

## Вправа: Написання клієнта

Як уже було сказано, давайте не поспішати з поясненням коду, і, звісно, ви можете писати код разом із нами.

### -1- Імпорт бібліотек

Імпортуємо потрібні бібліотеки, нам знадобляться посилання на клієнта та обраний транспортний протокол stdio. stdio — це протокол для програм, які запускаються на вашій локальній машині. SSE — інший транспортний протокол, який ми покажемо в майбутніх розділах, але наразі залишимо його як альтернативу. Поки що продовжимо з stdio.

### -2- Ініціалізація клієнта та транспорту

Потрібно створити екземпляр транспорту та екземпляр клієнта:

### -3- Виведення функцій сервера

Тепер у нас є клієнт, який може підключатися до сервера, якщо програму буде запущено. Проте він поки що не виводить список функцій, тому давайте зробимо це:

Чудово, тепер ми отримали всі функції. Тепер питання: коли їх використовувати? Цей клієнт досить простий, у сенсі, що ми маємо явно викликати функції, коли вони потрібні. У наступному розділі ми створимо більш просунутого клієнта, який матиме доступ до власної великої мовної моделі (LLM). А поки що подивимося, як можна викликати функції сервера:

### -4- Виклик функцій

Щоб викликати функції, потрібно переконатися, що ми передаємо правильні аргументи, а іноді і ім'я того, що хочемо викликати.

### -5- Запуск клієнта

Щоб запустити клієнта, введіть у терміналі таку команду:

## Завдання

У цьому завданні ви використаєте знання зі створення клієнта та напишете свій власний клієнт.

Ось сервер, який ви можете використовувати, викликаючи його через свій клієнтський код, спробуйте додати більше функцій до сервера, щоб зробити його цікавішим.

## Рішення

[Рішення](./solution/README.md)

## Основні висновки

Основні висновки цього розділу щодо клієнтів:

- Можна використовувати як для виявлення, так і для виклику функцій сервера.
- Можуть запускати сервер одночасно з собою (як у цьому розділі), але клієнти також можуть підключатися до вже запущених серверів.
- Це чудовий спосіб перевірити можливості сервера поряд з альтернативами, такими як Inspector, описаними в попередньому розділі.

## Додаткові ресурси

- [Створення клієнтів у MCP](https://modelcontextprotocol.io/quickstart/client)

## Приклади

- [Java калькулятор](../samples/java/calculator/README.md)
- [.Net калькулятор](../../../../03-GettingStarted/samples/csharp)
- [JavaScript калькулятор](../samples/javascript/README.md)
- [TypeScript калькулятор](../samples/typescript/README.md)
- [Python калькулятор](../../../../03-GettingStarted/samples/python)

## Що далі

- Далі: [Створення клієнта з LLM](/03-GettingStarted/03-llm-client/README.md)

**Відмова від відповідальності**:  
Цей документ був перекладений за допомогою сервісу автоматичного перекладу [Co-op Translator](https://github.com/Azure/co-op-translator). Хоча ми прагнемо до точності, будь ласка, майте на увазі, що автоматичні переклади можуть містити помилки або неточності. Оригінальний документ рідною мовою слід вважати авторитетним джерелом. Для критично важливої інформації рекомендується звертатися до професійного людського перекладу. Ми не несемо відповідальності за будь-які непорозуміння чи неправильні тлумачення, що виникли внаслідок використання цього перекладу.
# Приложение для создания и редактирования информации о встречах сотрудников

Написано для Node.js 8 и использует библиотеки:
* express
* sequelize
* graphql

## Задание
Код содержит ошибки разной степени критичности. Некоторых из них стилистические, а некоторые даже не позволят вам запустить приложение. Вам необходимо найти и исправить их.

Пункты для самопроверки:
1. Приложение должно успешно запускаться
2. Должно открываться GraphQL IDE - http://localhost:3000/graphql/
3. Все запросы на получение или изменения данных через graphql должны работать корректно. Все возможные запросы можно посмотреть в вкладке Docs в GraphQL IDE или в схеме (typeDefs.js)
4. Не должно быть лишнего кода
5. Все должно быть в едином codestyle

## Запуск
```
npm i
npm run dev
```

Для сброса данных в базе:
```
npm run reset-db
```
## Ход работы
1. Ошибка с Sequalize
При запуске приложения выводится какая-то ошибка, которая непонятно откуда исходит. Из логов видно, что она исходит из модуля sequalize. Первое, что приходит в голову - пакет был установлен с ошибкой, поэтому сношу node_modules и устанавливаю всё заново. После этого убеждаюсь, что ошибка где-то в коде, и начинаю искать файлы, где этот модуль используется. Попал на models/index.js. На первый взгляд, всё выглядит правильно. Однако в консоли выводится, что нужно обязательно указывать dialect в функции Sequalize. Так как объект с диалектом передаётся в конструктор, но получается, что его не обрабатывают, я решаю заглянуть в документацию Sequalize и посмотреть возможные проблемы: может аргументы идут не в том порядке или что-то пропущено. Так и оказалось, был пропущен один обязательный аргумент, из-за которого приложение и не запускалось. Добавляю его, и всё работает.
2. Убедился, что Graphql IDE открывается при рауте /graphql/
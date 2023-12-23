# Rocket frontend

Фронтенд часть тестового задания, с бэкенд частью можно ознакомиться
[здесь](https://github.com/sizieks/rocket-backend).

## Описание

Небольшое приложение на [Vue](https://vuejs.org/) с использованием UI-библиотеки
[Ant Design](https://antdv.com/). Отображает таблицу со списком сделок, получая
ответ от [сервера](https://github.com/sizieks/rocket-backend). Поиск позволяет
получить отфильтрованный на сервере результат по табличному столбцу
`ответственный`.

### Пример объекта

```javascript
{
  "id": "1hiamjbte067dc10fd27db",
  "name": "Случайная сделка #3",
  "price": 2276,
  "user": "Ермолай Павлов",
  "created_at": "2002-09-20T04:59:45.323Z",
  "status_name": "Успешно реализовано",
  "status_color": "#ffc8c8",
  "contact_name": "Глеб Морозов",
  "contact_phone": "+74433253382",
  "contact_email": "dolorsitamet@lorem.ipsum"
},
```

## Screenshots

Desktop @ 1440px

### Initial

![showcase-0](https://github.com/sizieks/rocket-frontend/assets/2656072/847a8a49-9413-4f41-a190-67192e5ef7be)

### Query

![showcase-1](https://github.com/sizieks/rocket-frontend/assets/2656072/e33f6dcb-9b9b-4d6c-ad06-bffee7db83ff)

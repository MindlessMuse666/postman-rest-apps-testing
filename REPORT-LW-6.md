![image](https://github.com/user-attachments/assets/3dfd8cff-2bf3-4bd2-9176-c3d6e1b68c79)

# Отчёт: Лабораторная работа №6 <a href="https://opensource.org/licenses/MIT"><img src="https://img.shields.io/badge/License-MIT-yellow.svg" alt="MIT-License image"></a>

**Дисциплина:** МДК 13.02

**Учебная группа:** 1ИСП-11-41

**Студент:** Бедин Владислав

**Исследуемая область:** Ubuntu (Linux), Node.js

**Тема работы:** Тестирование распределенных REST-приложений с помощью инструмента Postman


## 1. Создание переменной коллекции `base_url` со значением `https://swapi.dev/api/`

#### 1-4.png <Ссылка на фото через `html` с `center`>


## 2. GET-запрос на получение информации о планетах

### Запрос: {{base_url}}planets/

#### 5.png <Ссылка на фото через `html` с `center`>


## 3. Значения атрибутов

### 3.1. rotation_period

Атрибут `rotation_period` означает период вращения планеты вокруг своей оси (в часах).

### 3.2. orbital_period

Атрибут `orbital_period` означает период обращения планеты вокруг своей звезды (в днях).


## 3. GET-запрос на получение информации о космических кораблях

### Запрос: {{base_url}}starships/

#### 6-8.png  <Ссылка на фото через `html` с `center`>


## 4. GET-запрос с параметром на получение второй страницы о космических кораблях

### Запрос: {{base_url}}starships/?page=2

#### 9.png  <Ссылка на фото через `html` с `center`>


## 5. Тестирование успешности запроса

```javascript
pm.test("Status code is 200", () => {
    pm.response.to.have.status(200);
});
```

#### 10.png  <Ссылка на фото через `html` с `center`>


## 6. GET-запрос на получение всех звездолетов, в названии или модели которых есть подстрока `Star` или `star`

```javascript
pm.test("Starships with 'Star' in name or model", () => {
  const response = pm.response.json();
  const filteredStarships = response.results.filter(starship => {
    return starship.name.toLowerCase().includes("star") || starship.model.toLowerCase().includes("star");
  });

  pm.expect(filteredStarships.length).to.be.above(0, "No starships found with 'Star' in name or model");

  console.log("Filtered Starships:", filteredStarships);
});
```

#### 11.png  <Ссылка на фото через `html` с `center`>


## 7. Тестовая проверка скорости отчёта (пришел ли ответ за 300 мс)

```javascript
pm.test("Starships with 'Star' in name or model", () => {
  const response = pm.response.json();
  const filteredStarships = response.results.filter(starship => {
    return starship.name.toLowerCase().includes("star") || starship.model.toLowerCase().includes("star");
  });

  pm.expect(filteredStarships.length).to.be.above(0, "No starships found with 'Star' in name or model");

  console.log("Filtered Starships:", filteredStarships);
  
  pm.test("Response time is less than 300ms", () => {
    pm.expect(pm.response.responseTime).to.be.below(300);
  });
});
```

#### 12.png  <Ссылка на фото через `html` с `center`>


## 8. GET-запрос подробной информации обо всех звездолетах на языке *wookiee*

### Запрос: {{base_url}}starships/?format=wookiee

#### 13.png  <Ссылка на фото через `html` с `center`>


## 9. Тестовая проверка, что ответ от сервера содержит подстроку `warcworawawhoohurracao`

```javascript
pm.test("Response body contains warcworawawhoohurracao", () => {
  pm.expect(pm.response.text()).to.include("warcworawawhoohurracao");
});
```

#### 14.png  <Ссылка на фото через `html` с `center`>


## 10. Одновременный запуск трёх последних запроса с тестами

- В коллекции "SWAPI Requests" нажимаем на три точки (Options) и выбераем "Run Collection"
- Настраиваем Runner и нажимаем "Run SWAPI Requests"

#### 15.png  <Ссылка на фото через `html` с `center`>


## 11. Выбор персонажа и GET-запрос информации о нём

- **Выбранный персонаж:** Luke Skywalker (вариант 1)
- **Запрос:** {{base_url}}people/?search=Luke Skywalker

JSON-респонс о *Luke Skywalker*:

```
{
    "count": 1,
    "next": null,
    "previous": null,
    "results": [
        {
            "name": "Luke Skywalker",
            "height": "172",
            "mass": "77",
            "hair_color": "blond",
            "skin_color": "fair",
            "eye_color": "blue",
            "birth_year": "19BBY",
            "gender": "male",
            "homeworld": "https://swapi.dev/api/planets/1/",
            "films": [
                "https://swapi.dev/api/films/1/",
                "https://swapi.dev/api/films/2/",
                "https://swapi.dev/api/films/3/",
                "https://swapi.dev/api/films/6/"
            ],
            "species": [],
            "vehicles": [
                "https://swapi.dev/api/vehicles/14/",
                "https://swapi.dev/api/vehicles/30/"
            ],
            "starships": [
                "https://swapi.dev/api/starships/12/",
                "https://swapi.dev/api/starships/22/"
            ],
            "created": "2014-12-09T13:50:51.644000Z",
            "edited": "2014-12-20T21:17:56.891000Z",
            "url": "https://swapi.dev/api/people/1/"
        }
    ]
}
```

#### 16-20.png  <Ссылка на фото через `html` с `center`>

### 11.1. Рост персонажа *Luke Skywalker*

Рост узнаём из строки JSON-респонса: `"height": "172",`

Рост равен **172**.

### 11.2. Вес персонажа *Luke Skywalker*

Вес узнаём из строки JSON-респонса: `"mass": "77",`

Вес равен **172**.

### 11.3. Цвет глаз персонажа *Luke Skywalker*

Цвет глаз узнаём из строки JSON-респонса: `"eye_color": "blue",`

Цвет глаз - **голубой**.


## 12. Родная планета персонажа *Luke Skywalker*

1. Родную планету узнаём из строки JSON-респонса: `"homeworld": "https://swapi.dev/api/planets/1/",`
2. Делаем запрос к этой планете для определения её названия. GET-запрос: `https://swapi.dev/api/planets/1/`
3. Родная планета - **Tatooine**

#### 21.png  <Ссылка на фото через `html` с `center`>


## 13. Информация о родной планете персонажа *Luke Skywalker*

- **Родная планета персонажа:** Tatooine
- **Запрос:** {{base_url}}planets/1/

JSON-респонс о *Tatooine*:

```
{
    "name": "Tatooine",
    "rotation_period": "23",
    "orbital_period": "304",
    "diameter": "10465",
    "climate": "arid",
    "gravity": "1 standard",
    "terrain": "desert",
    "surface_water": "1",
    "population": "200000",
    "residents": [
        "https://swapi.dev/api/people/1/",
        "https://swapi.dev/api/people/2/",
        "https://swapi.dev/api/people/4/",
        "https://swapi.dev/api/people/6/",
        "https://swapi.dev/api/people/7/",
        "https://swapi.dev/api/people/8/",
        "https://swapi.dev/api/people/9/",
        "https://swapi.dev/api/people/11/",
        "https://swapi.dev/api/people/43/",
        "https://swapi.dev/api/people/62/"
    ],
    "films": [
        "https://swapi.dev/api/films/1/",
        "https://swapi.dev/api/films/3/",
        "https://swapi.dev/api/films/4/",
        "https://swapi.dev/api/films/5/",
        "https://swapi.dev/api/films/6/"
    ],
    "created": "2014-12-09T13:50:49.641000Z",
    "edited": "2014-12-20T20:58:18.411000Z",
    "url": "https://swapi.dev/api/planets/1/"
}
```


## . Лицензия

Этот проект распространяется под лицензией MIT - смотрите файл [LICENSE](LICENSE) для деталей.


## . Автор

Бедин Владислав ([MindlessMuse666](https://github.com/MindlessMuse666))
- GitHub: [MindlessMuse666](https://github.com/MindlessMuse666 "Владислав: https://github.com/MindlessMuse666")
- Telegram: [@mindless_muse](t.me/mindless_muse)
- Gmail: [mindlessmuse.666@gmail.com](mindlessmuse.666@gmail.com)

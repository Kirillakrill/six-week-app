<h1>six-week-app</h1>
This app for curs https://courses.openedu.ru/courses/course-v1:ITMOUniversity+NODEJS+spring_2021/course/

Практика недели 6 Задание недели 6

Цель Разработать веб-приложение с использованием фреймворка Express.

Приложение должно Находиться в публичном доступе; Работать по протоколу HTTPS; В заголовках всех ответов выдавать: Access-Control-Allow-Origin со значением «*»; Access-Control-Allow-Methods со значением «GET,POST,PUT,PATCH,OPTIONS,DELETE»; Соблюдать политику Trailing Slashes, при которой основная часть URI всегда заканчивается символом слэша «/»; Использовать фреймворк Express. Исключить комментарии Исключить использование console и любых других зависимостей, не перечисленных ниже.

Варианты размещения Heroku; Repl.it; Собственный сервер (вариант для продвинутых).

Структура приложения Структура веб-приложения должна состоять из файлов app.js и index.js, размещенных в рамках одной папки.

4.1 Файл app.js Данный файл должен в формате ESM экспортировать функцию инициалиации Express-приложения (примеры работы с экспортом). Не забудьте о ключе type="module" в файле package.json

Экспортируемая функция должна принимать пять аргументов:

express - конструктор Express-приложения (пример вызова конструктора);

bodyParser – middleware для Express для работы с телом запроса;

createReadStream – функция из стандартного модуля fs платформы node's

crypto, http – стандартные модули node's

В результате своей работы экспортируемая функция должна возвращать экземпляр готового к работе Express-приложения.

4.2 Файл index.js Сначала в данном файле должны быть импортированы внешние модули необходимые для работы приложения, а именно:

express,

body-parser – middleware для Express для работы с телом запроса;

createReadStream, – функция из стандартного модуля fs.

crypto и http – стандартные модули.

Затем из файла app.js необходимо импортировать функцию инициализации Express-приложения, которую необходимо вызвать, передав в неё express, bodyParser, createReadStream, crypto и http:

import appSrc from './app.js'; const app = appSrc(express, bodyParser, createReadStream, crypto, http); Полученному приложению необходимо дать указание о прослушивании входящих запросов с порта предоставляемого средой хостера (Heroku или Repl.it) или собственного:

app.listen(process.env.PORT); 5. Требования к логике приложения (app.js) Приложение должно содержать следующие маршруты:

/login/

/code/

/sha1/:input/

/req/ с параметром ?addr=

Маршрут отлова всех остальных вариантов запросов (используйте для этого app.all)

5.1. Маршрут /login/ Данный маршрут должен возвращать Ваш логин в системе OpenEDU (например, itmo2342351)

5.2. Маршрут /code/ Данный маршрут должен возвращать исходный код текущего файла (в данном случае файла app.js). Для этого необходимо воспользоваться функцией createReadStream модуля fs, предназначенной для чтения файлов.

При этом для получения пути к файлу необходимо воспользоваться значением import.meta.url.substring(7), чтобы получить расположение текущего файла в рамках файловой системы. (Внимание, при использовании Windows потребуется другое число, на 1-3 больше чем 7.)

5.3. Маршрут /sha1/:input/ Данный маршрут должен возвращать хэш sha1 от строки, представленной параметром URL (по имени input)

5.4. Маршрут /req/ Данный маршрут должен возвращать содержимое интернет-ресурса по адресу, содержащемуся в query-параметре URL по имени addr (в простом текстовом формате). Для этого следует воспользоваться методом get модуля http. Т.е. приложение должно обратиться по адресу, который ему передан, прочитать его содержимое и тут же вернуть в качестве ответа. Данный маршрут должен обрабатываться методами GET и POST c возможностью в последнем случае получить значение addr из тела запроса, например

curl 'https://demoapp.kodaktor.ru/req/?addr=http://node-server.online/r/assets/week.txt' 5

curl 'https://demoapp.kodaktor.ru/req/' -d 'addr=http://node-server.online/r/assets/week.txt' 5 5.5. Маршрут отлова остальных запросов Данный маршрут также должен возвращать ваш логин в системе.

Предоставление ответа В поле ввода ответа, которое представлено ниже, необходимо ввести корневой маршрут Вашего приложения, т.е. URI аналогичный следующему: https://myweek3work.herokuapp.com/ (не забывайте про политику Trailing Slashes)

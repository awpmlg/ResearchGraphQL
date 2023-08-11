# Оглавление

- [Доступ к приватным сообщениям GraphQL](#title1)
- [Случайное раскрытие закрытых полей GraphQL](#title2)
- [Поиск скрытой конечной точки GraphQL](#title3)
- [Обход защиты от грубой силы GraphQL](#title4)
- [CSRF через GraphQL](#title5)

## <a id="title1">[Доступ к приватным сообщениям GraphQL](https://portswigger.net/web-security/graphql/lab-graphql-reading-private-posts)</a>

Заходим на сайт и проверяем что на нем есть.

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/ExampleVulns/PortSwigger/img/1_1.png">

Видим посты в блоге, открываем.

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/ExampleVulns/PortSwigger/img/1_2.png">

Замечаем что пост с id 3 нельзя просмотреть через браузер.

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/ExampleVulns/PortSwigger/img/1_3.png">

Смотрим в историю http в берп.

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/ExampleVulns/PortSwigger/img/1_4.png">

Видим что есть GraphQL.

Отправляем запрос в InQL Scanner.

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/ExampleVulns/PortSwigger/img/1_5.png">

Узнаем что getBlogPost(id:xxx) имеет поле postPassword.

Добавим найденное поле к запросу и изменим аргумент id на 3

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/ExampleVulns/PortSwigger/img/1_6.png">

В ответ получаем скрытую информацию.

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/ExampleVulns/PortSwigger/img/1_7.png">

## <a id="title2">[Случайное раскрытие закрытых полей GraphQL](https://portswigger.net/web-security/graphql/lab-graphql-accidental-field-exposure)</a>

Заходим на сайт.

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/ExampleVulns/PortSwigger/img/2_1.png">

Видим что можно залогиниться, пытаемся.

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/ExampleVulns/PortSwigger/img/2_2.png">

Посмотрим историю http.

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/ExampleVulns/PortSwigger/img/2_3.png">

Видим запрос к GraphQL, отправляем в InQL.

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/ExampleVulns/PortSwigger/img/2_4.png">

Узнаем что есть getUser который выводит информацию и пользователях, включая пароль и логин. 

Отправляем запрос в репитор и изменяем с помощью InQL(еще нужно удалить “operationName” и переменные).

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/ExampleVulns/PortSwigger/img/2_5.png">

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/ExampleVulns/PortSwigger/img/2_6.png">

Получаем данные администратора.

## <a id="title3">[Поиск скрытой конечной точки GraphQL](https://portswigger.net/web-security/graphql/lab-graphql-find-the-endpoint)</a>

Заходим на сайт.

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/ExampleVulns/PortSwigger/img/3_1.png">

Смотрим историю http, в ней нет никаких конечных точек для GraphQL, следовательно пытаемся найти сами. Вводим /api и находим GraphQL.

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/ExampleVulns/PortSwigger/img/3_2.png">

Отправим этот запрос в репитор и изменим его, чтобы он содержал универсальный запрос, как пример /api?query=query{__typename}.

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/ExampleVulns/PortSwigger/img/3_3.png">

Ответ подтвердил, что мы нашли конечную точку GraphQL.

Далее вставим запрос для самоанализа(в url кодировке, так как запрос отправляется методом GET).

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/ExampleVulns/PortSwigger/img/3_4.png">

Приложение отвечает что самоанализ не разрешен, попробуем обойти, в наш запрос после __schema вставим символ новой строки.

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/ExampleVulns/PortSwigger/img/3_5.png">

Мы обошли запрет и получили всю информацию.

Далее создаем файл в формате json и записываем в него ответ сервера(только данные в формате json). Этот файл отправляем в InQL.

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/ExampleVulns/PortSwigger/img/3_6.png">

Узнали скрытую информацию о схеме.

## <a id="title4">[Обход защиты от грубой силы GraphQL](https://portswigger.net/web-security/graphql/lab-graphql-brute-force-protection-bypass)</a>

Заходим на сайт.

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/ExampleVulns/PortSwigger/img/4_1.png">

Видим окно логина, нам нужно забрутить пользователя carlos, но после 3 неправильных запросов идет блокировка на минуту.

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/ExampleVulns/PortSwigger/img/4_2.png">

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/ExampleVulns/PortSwigger/img/4_3.png">

Чтобы ее обойти можно использовать псевдонимы. Создаем запрос(так как руками его писать очень долго, можно написать скрипт который его сгенерирует из предоставленного списка паролей).

Пример:

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/ExampleVulns/PortSwigger/img/4_4.png">

Еще нужно удалить “operationName” и переменные.

Редактируем запрос:

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/ExampleVulns/PortSwigger/img/4_5.png">

Отправляем и получаем множество ответов на попутку залогинится, среди них находим со значением “true”:

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/ExampleVulns/PortSwigger/img/4_6.png">

Используем найденный токен и получаем доступ к аккаунту.

## <a id="title5">[CSRF через GraphQL](https://portswigger.net/web-security/graphql/lab-graphql-csrf-via-graphql-api)</a>

Заходим на сайт.

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/ExampleVulns/PortSwigger/img/5_1.png">

Используя данных для входа логинемся и меняем почту.

Видим, что запрос идет к GraphQL.

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/ExampleVulns/PortSwigger/img/5_2.png">

Пытаемся еще раз сменить почту с такими же токенами и получаем согласие(потенциальная csrf найдена).

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/ExampleVulns/PortSwigger/img/5_3.png">

Изменяем в запросе хедер Content-Type на application/x-www-form-urlencoded. В тело запроса записываем наш запрос и проверяем что все работает.

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/ExampleVulns/PortSwigger/img/5_4.png">

Создаем PoC CSRF.

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/ExampleVulns/PortSwigger/img/5_5.png">

Копируем html и вставляем в тело на нашем сервере.

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/ExampleVulns/PortSwigger/img/5_6.png">

Отправляем жертве и когда она посетит наш сайт то ее почта изменится.

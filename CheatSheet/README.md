<h1 align="center">☠️Cheat Sheet☠️</a> 

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
- - [NoSQL injection](#title131)
  - [SQL injection](#title132)
  - [OS command injection](#title133)
  - [HTML injection](#title134)
  - [Stored XSS](#title135)
- [DOS атаки](#title14)
- [Обход авторизации](#title15)
- [Arbitrary File Write + Path Traversal](#title16)
- [IDOR](#title17)

# <a id="title1">Универсальный запрос</a>

Запрос `{__typename}` к любой конечной точке GraphQL, он будет включать строку `{"data": {"__typename": "query"}}` где-то в своем ответе. Это является доказательством того, что URL-адрес соответствует службе GraphQL

# <a id="title2">Поиск конечных точек</a>
| Возможные | Эндпоинты |
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

# <a id="title9">Проверка SSRF</a>

# <a id="title10">Предложения(Suggestions)</a>

# <a id="title11">Утечка структур GraphQL</a>

# <a id="title12">Извлечение данных</a>

# <a id="title13">Инъекции</a>

### <a id="title131">NoSQL injection</a>

### <a id="title132">SQL injection</a>

### <a id="title133">OS command injection</a>

### <a id="title134">HTML injection</a>

### <a id="title135">Stored XSS</a>

# <a id="title14">DOS атаки</a>

# <a id="title15">Обход авторизации</a>

# <a id="title16">Arbitrary File Write + Path Traversal</a>

# <a id="title17">IDOR</a>

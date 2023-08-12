

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/1.png">

Текст к слайду⬆️: 

Добрый день! Представляю вашему вниманию исследование на тему “Анализ безопасности приложений, использующих GraphQL API”, доклад подготовил Савин Даниил.

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/2.png">

Текст к слайду⬆️: 

GraphQL — это язык запросов API, предназначенный для обеспечения эффективной связи между клиентами и серверами. Это позволяет пользователю точно указать, какие данные он хочет получить в ответе, помогая избежать больших объектов ответа и множественных вызовов. 

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/3.png">

Текст к слайду⬆️: 

Службы GraphQL устроены так, что клиенту не нужно знать, где находятся данные. Вместо этого клиенты отправляют запросы на сервер GraphQL, который извлекает данные из соответствующих мест.

Все операции GraphQL используют одну и ту же конечную точку и обычно отправляются как запрос POST. Это существенно отличается от API-интерфейсов REST, которые используют конечные точки для конкретных операций в ряде методов HTTP. В GraphQL тип и имя операции определяют способ обработки запроса, а не конечную точку, в которую он отправляется, или используемый метод HTTP. 

Службы GraphQL обычно реагируют на операции с объектом JSON в запрошенной структуре.

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/4.png">

Текст к слайду⬆️: 

С данными, описанными схемой GraphQL, можно манипулировать с помощью трех типов операций:

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/5.png">

Текст к слайду⬆️: 

Рассмотрим методы разведки.

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/6.png">

Текст к слайду⬆️: 

Если отправить запрос, представленный слева, к любой конечной точке GraphQL и ответ на него будет где-либо содержать строку представленную справа, то URL-адрес соответствует службе GraphQL.

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/7.png">

Текст к слайду⬆️: 

На слайде представлен список возможных эндпоинтов для приложения GraphQL.([ссылка](https://github.com/danielmiessler/SecLists/blob/fe2aa9e7b04b98d94432320d09b5987f39a17de8/Discovery/Web-Content/graphql.txt))

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/8.png">

Текст к слайду⬆️: 

([ссылка](https://github.com/dolevf/graphw00f))

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/9.png">

Текст к слайду⬆️: 

Некоторые конечные точки могут принимать альтернативные методы, такие как запросы `GET` или запросы `POST`, которые используют тип содержимого `x-www-form-urlencoded`.

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/10.png">

Текст к слайду⬆️: 

Самоанализ — это встроенная функция GraphQL, которая позволяет запрашивать у сервера информацию о схеме. 

Для получения всей схемы можно использовать расширение для Burp - InQL, либо ручную проверку.

Первым шагов, для выявления поддерживает ли GraphQL запросы самоанализа, нужно отправить зонд.

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/11.png">

Текст к слайду⬆️: 

Эти два способа можно комбинировать между собой.
([ссылка](https://github.com/nikitastupin/clairvoyance))

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/12.png">

Текст к слайду⬆️: 

([ссылка](https://github.com/awpmlg/ResearchGraphQL/tree/main/ExampleVulns/PortSwigger#%D0%BF%D0%BE%D0%B8%D1%81%D0%BA-%D1%81%D0%BA%D1%80%D1%8B%D1%82%D0%BE%D0%B9-%D0%BA%D0%BE%D0%BD%D0%B5%D1%87%D0%BD%D0%BE%D0%B9-%D1%82%D0%BE%D1%87%D0%BA%D0%B8-graphql))

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/13.png">

Текст к слайду⬆️: 

Уязвимости GraphQL обычно возникают из-за недостатков реализации и дизайна. Например, функцию самоанализа можно оставить активной, что позволит злоумышленникам запрашивать API, чтобы получить информацию о его схеме.

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/14.png">

Текст к слайду⬆️: 

Атаки на GraphQL обычно принимают форму вредоносных запросов, которые могут позволить злоумышленнику получить данные или выполнить несанкционированные действия.

На слайде представлены все разновидности атак:

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/15.png">

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/16.png">

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/17.png">

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/18.png">

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/19.png">

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/20.png">

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/21.png">

Текст к слайду⬆️: 

Пример уязвимости представлен на слайде

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/22.png">

Текст к слайду⬆️: 

Если GraphQL используется для авторизации и принимает данные от клиента, то можно использовать перебор, но если есть какие-либо системы защиты от перебора можно использовать методы их обхода. На слайде представлена одна из них - использование псевдонимов.

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/23.png">

Текст к слайду⬆️: 

Если мутация принимает данные по типу “host” и тому подобное, это может быть уязвимо для атаки SSRF.

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/24.png">

Текст к слайду⬆️: 

Если в приложение реализована функция самоанализа и функции вывода информации о пользователях или иной системной информации, приложение может раскрыть секретную информацию о пользователях.

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/25.png">

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/26.png">

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/27.png">

Текст к слайду⬆️: 

Если в запросе есть параметр который обращается в shell, то возможна инъекция команд.

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/28.png">

Текст к слайду⬆️: 

Если есть мутация позволяющая создавать или редактировать какие-либо записи.

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/29.png">

Текст к слайду⬆️: 

Если есть мутация позволяющая создавать или редактировать какие-либо записи.

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/30.png">

Текст к слайду⬆️: 

Некоторые запросы могут быть запрещены, для обхода используются названия операций.

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/31.png">

Текст к слайду⬆️: 

Если используется мутация для загрузки файла.

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/32.png">

Текст к слайду⬆️: 

*Примечание: Шаги по построению атаки GraphQL CSRF  и доставке эксплойта такие же как и для «обычных» уязвимостей CSRF.*

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/33.png">

Текст к слайду⬆️: 

([ссылка](https://github.com/awpmlg/ResearchGraphQL/tree/main/ExampleVulns/PortSwigger#csrf-%D1%87%D0%B5%D1%80%D0%B5%D0%B7-graphql))

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/34.png">

Текст к слайду⬆️: 

Тестирование приложений производится с помощью инструментов и расширений для них.

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/35.png">

Текст к слайду⬆️: 

Рассмотрим расширения для Burp, в таблице отмечено какой функционал они поддерживают.

*InQL проявил себя лучше всех и советую использовать именно его, если вам нужно расширение для Burp.*

[InQL](https://github.com/doyensec/inql)

[Graph Query Parser & Editor](https://github.com/br3akp0int/GQLParser)

[GraphQL Raider](https://github.com/denniskniep/GQLRaider)

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/36.png">

Текст к слайду⬆️: 

Далее представлены консольные инструменты, в таблице отмечено какой функционал они поддерживают.

[GraphCrawler](https://github.com/gsmith257-cyber/GraphCrawler)

[GraphQLmap](https://github.com/swisskyrepo/GraphQLmap)

[CrackQL](https://github.com/nicholasaleks/CrackQL)

[GraphQL Cop](https://github.com/dolevf/graphql-cop)

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/37.png">

Текст к слайду⬆️: 

Рассмотрим как предотвратить атаки на приложение

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/38.png">

Текст к слайду⬆️: 

Чтобы предотвратить многие распространенные атаки GraphQL, при развертывании API в рабочей среде выполните следующие действия:

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/39.png">

Текст к слайду⬆️: 

1)https://clck.ru/35GqWy - GraphQL cheatsheet для разработки;

2)https://clck.ru/35GqXs - Пентест GrapQL;

3)https://clck.ru/35GqYF - Если не разрешен самоанализ, но приложение раскрывает информацию в ошибках;

4)https://clck.ru/35GqYS - Инструмент для определения версии движка;

5)https://clck.ru/35GqYY - Пример брутфорс атаки;

6)https://clck.ru/35GqYg и https://clck.ru/35GqYq - Все про GraphQL;

7)https://clck.ru/35GqZC - Расширение для Burp;

8)https://clck.ru/35GqZc - Веб приложение для практики.

<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/40.png">

Текст к слайду⬆️: 

Доклад окончен, спасибо за внимание!

Готов ответить на ваши вопросы!

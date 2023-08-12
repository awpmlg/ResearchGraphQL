

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



<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/13.png">

Текст к слайду⬆️: 



<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/14.png">

Текст к слайду⬆️: 



<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/15.png">

Текст к слайду⬆️: 



<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/16.png">

Текст к слайду⬆️: 



<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/17.png">

Текст к слайду⬆️: 



<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/18.png">

Текст к слайду⬆️: 



<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/19.png">

Текст к слайду⬆️: 



<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/20.png">

Текст к слайду⬆️: 



<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/21.png">

Текст к слайду⬆️: 



<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/22.png">

Текст к слайду⬆️: 



<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/23.png">

Текст к слайду⬆️: 



<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/24.png">

Текст к слайду⬆️: 



<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/25.png">

Текст к слайду⬆️: 


<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/26.png">

Текст к слайду⬆️: 



<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/27.png">

Текст к слайду⬆️: 



<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/28.png">

Текст к слайду⬆️: 



<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/29.png">

Текст к слайду⬆️: 



<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/30.png">

Текст к слайду⬆️: 



<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/31.png">

Текст к слайду⬆️: 



<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/32.png">

Текст к слайду⬆️: 



<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/33.png">

Текст к слайду⬆️: 



<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/34.png">

Текст к слайду⬆️: 



<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/35.png">

Текст к слайду⬆️: 



<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/36.png">

Текст к слайду⬆️: 



<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/37.png">

Текст к слайду⬆️: 



<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/38.png">

Текст к слайду⬆️: 



<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/39.png">

Текст к слайду⬆️: 



<img src="https://github.com/awpmlg/ResearchGraphQL/blob/main/Presentation/img/40.png">

Текст к слайду⬆️: 


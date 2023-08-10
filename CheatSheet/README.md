# Cheat Sheet
> all about GraphQL vulns
<h1 align="center">Hi there, I'm Daniil</a> 
<img src="https://github.com/blackcater/blackcater/raw/main/images/Hi.gif" height="32"/></h1>
<h3 align="center">Computer science student, IT news writer from Russia 🇷🇺</h3>

[![Typing SVG](https://readme-typing-svg.herokuapp.com?color=%2336BCF7&lines=Computer+science+student)](https://git.io/typing-svg)
# Оглавление
- [Универсальный запрос](https://github.com/awpmlg/ResearchGraphQL/tree/main/CheatSheet#%D1%83%D0%BD%D0%B8%D0%B2%D0%B5%D1%80%D1%81%D0%B0%D0%BB%D1%8C%D0%BD%D1%8B%D0%B9-%D0%B7%D0%B0%D0%BF%D1%80%D0%BE%D1%81)
- [Поиск конечных точек](https://github.com/awpmlg/ResearchGraphQL/tree/main/CheatSheet#%D0%BF%D0%BE%D0%B8%D1%81%D0%BA-%D0%BA%D0%BE%D0%BD%D0%B5%D1%87%D0%BD%D1%8B%D1%85-%D1%82%D0%BE%D1%87%D0%B5%D0%BA)
- [Определение движка](https://github.com/awpmlg/ResearchGraphQL/tree/main/CheatSheet#%D0%BE%D0%BF%D1%80%D0%B5%D0%B4%D0%B5%D0%BB%D0%B5%D0%BD%D0%B8%D0%B5-%D0%B4%D0%B2%D0%B8%D0%B6%D0%BA%D0%B0)
- [Если не принимает обычные запросы](https://github.com/awpmlg/ResearchGraphQL/tree/main/CheatSheet#%D0%B5%D1%81%D0%BB%D0%B8-%D0%BD%D0%B5-%D0%BF%D1%80%D0%B8%D0%BD%D0%B8%D0%BC%D0%B0%D0%B5%D1%82-%D0%BE%D0%B1%D1%8B%D1%87%D0%BD%D1%8B%D0%B5-%D0%B7%D0%B0%D0%BF%D1%80%D0%BE%D1%81%D1%8B)
- [Запрос самоанализа](https://github.com/awpmlg/ResearchGraphQL/tree/main/CheatSheet#%D0%B7%D0%B0%D0%BF%D1%80%D0%BE%D1%81-%D1%81%D0%B0%D0%BC%D0%BE%D0%B0%D0%BD%D0%B0%D0%BB%D0%B8%D0%B7%D0%B0)
- [Обход защиты самоанализа](https://github.com/awpmlg/ResearchGraphQL/tree/main/CheatSheet#%D0%BE%D0%B1%D1%85%D0%BE%D0%B4-%D0%B7%D0%B0%D1%89%D0%B8%D1%82%D1%8B-%D1%81%D0%B0%D0%BC%D0%BE%D0%B0%D0%BD%D0%B0%D0%BB%D0%B8%D0%B7%D0%B0)
- [Обход ограничения кол-ва запросов](https://github.com/awpmlg/ResearchGraphQL/tree/main/CheatSheet#%D0%BE%D0%B1%D1%85%D0%BE%D0%B4-%D0%BE%D0%B3%D1%80%D0%B0%D0%BD%D0%B8%D1%87%D0%B5%D0%BD%D0%B8%D1%8F-%D0%BA%D0%BE%D0%BB-%D0%B2%D0%B0-%D0%B7%D0%B0%D0%BF%D1%80%D0%BE%D1%81%D0%BE%D0%B2)
- [Проверка CSFR](https://github.com/awpmlg/ResearchGraphQL/tree/main/CheatSheet#%D0%BF%D1%80%D0%BE%D0%B2%D0%B5%D1%80%D0%BA%D0%B0-csfr)
- [Проверка SSRF](https://github.com/awpmlg/ResearchGraphQL/tree/main/CheatSheet#%D0%BF%D1%80%D0%BE%D0%B2%D0%B5%D1%80%D0%BA%D0%B0-ssrf)
- [Предложения(Suggestions)](https://github.com/awpmlg/ResearchGraphQL/tree/main/CheatSheet#%D0%BF%D1%80%D0%B5%D0%B4%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D1%8Fsuggestions)
- [Утечка структур GraphQL](https://github.com/awpmlg/ResearchGraphQL/tree/main/CheatSheet#%D1%83%D1%82%D0%B5%D1%87%D0%BA%D0%B0-%D1%81%D1%82%D1%80%D1%83%D0%BA%D1%82%D1%83%D1%80-graphql)
- [Извлечение данных](https://github.com/awpmlg/ResearchGraphQL/tree/main/CheatSheet#%D0%B8%D0%B7%D0%B2%D0%BB%D0%B5%D1%87%D0%B5%D0%BD%D0%B8%D0%B5-%D0%B4%D0%B0%D0%BD%D0%BD%D1%8B%D1%85)
- [Инъекции](https://github.com/awpmlg/ResearchGraphQL/tree/main/CheatSheet#%D0%B8%D0%BD%D1%8A%D0%B5%D0%BA%D1%86%D0%B8%D0%B8)
- - [1]
  - [2]
  - [3]
  - [4]
- [DOS атаки](https://github.com/awpmlg/ResearchGraphQL/tree/main/CheatSheet#dos-%D0%B0%D1%82%D0%B0%D0%BA%D0%B8)
- [Обход авторизации](https://github.com/awpmlg/ResearchGraphQL/tree/main/CheatSheet#%D0%BE%D0%B1%D1%85%D0%BE%D0%B4-%D0%B0%D0%B2%D1%82%D0%BE%D1%80%D0%B8%D0%B7%D0%B0%D1%86%D0%B8%D0%B8)
- [Arbitrary File Write + Path Traversal](https://github.com/awpmlg/ResearchGraphQL/tree/main/CheatSheet#arbitrary-file-write--path-traversal)
- [IDOR](https://github.com/awpmlg/ResearchGraphQL/tree/main/CheatSheet#idor)

# Универсальный запрос

dfgdfgdfgfdg`fdgdfgdfg`

# Поиск конечных точек

```
sdfsdfsdfsdfgfhdfghfghdfg
```

# Определение движка

# Если не принимает обычные запросы

# Запрос самоанализа

# Обход защиты самоанализа

# Обход ограничения кол-ва запросов

# Проверка CSFR

# Проверка SSRF

# Предложения(Suggestions)

# Утечка структур GraphQL

# Извлечение данных

# Инъекции

# DOS атаки

# Обход авторизации

# Arbitrary File Write + Path Traversal

# IDOR

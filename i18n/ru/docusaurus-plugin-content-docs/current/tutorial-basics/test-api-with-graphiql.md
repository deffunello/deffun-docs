---
sidebar_position: 4
---

# Тестирование API с помощью GraphiQL

После успешного деплоя, вы можете протестировать API с помощью Graph*i*QL.
Graph*i*QL позволяет делать запросы к вашему API прямо из браузера.

## Примеры запросов

Для следующих запросов объявленных в схеме
```
type Query {
    getAll: [Company!]
    getById(id: ID!): Company
}
```
запросы в Graph*i*QL или другой IDE будут выглядеть так:
```
# Получим список компании и их названия и адреса
query {
    getAll {
        id
        name
        address
    }
}
# Получим название и адрес компании по её ID
query {
    getById(123) {
        id
        name
        address
    }
}
```

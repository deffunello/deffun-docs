---
sidebar_position: 6
---

# Аутентификация и авторизация

## Пользователи

Добавьте следующую директиву в вашу схему:
```graphql
directive @user on OBJECT | INTERFACE
```
Каждого пользователя надо пометить как @user:
```graphql
type MyUser @user {
    id: ID!
    username: String!
    name: String!
    age: Int!
}
```

Добавьте следующую директиву в вашу схему:
```graphql
directive @currentUser on FIELD_DEFINITION
```
Чтобы получить аутентифицированного пользователя:
```graphql
currentUser: MyUser! @currentUser
```

## Авторизованные запросы

Добавьте перечисление `AuthRules` и директиву `auth` в вашу схему:
```graphql
enum AuthRules {
    # встроенные правила для проверки аутентифицированных пользователей
    Authenticated, IsAuthenticated
    Authn, IsAuthn
    # если тип помечен как @user, то следующие правила будут добавлены автоматически
    Admin, IsAdmin
    Parent, IsParent
    Specialist, IsSpecialist
}
directive @auth(rules: [AuthRules]) on FIELD_DEFINITION | OBJECT | INTERFACE
```

Несколько примеров использования:
```graphql
type Mutation {
    createUser(input: MyUserInput): MyUser # любой может выполнить эту мутацию
    updateUser(id: ID, input: MyUserInput): MyUser @auth(rules: [IsAuthenticated]) # только аутентифицированный пользователь может выполнить эту мутацию
    doStuff: Stuff @auth(rules: [MyUser])
    ...
}
```

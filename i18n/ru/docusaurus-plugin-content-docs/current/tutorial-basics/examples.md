---
sidebar_position: 6
---

# Примеры схем

Готовые примеры схем для разного рода приложений.

Twitter (сгенерировано ChatGPT):
```graphql
type User {
    id: ID!
    name: String!
    username: String!
    tweets: [Tweet!]!
    followers: [User!]!
    following: [User!]!
}

type Tweet {
    id: ID!
    text: String!
    author: User!
    createdAt: String!
    likes: Int!
    retweets: Int!
}

type Query {
    user(id: ID!): User
    tweet(id: ID!): Tweet
}

type Mutation {
    createUser(name: String!, username: String!): User!
    createTweet(userId: ID!, text: String!): Tweet!
    deleteTweet(id: ID!): Boolean!
}

schema {
    query: Query
    mutation: Mutation
}
```

Twitter из интернета:
```graphql
type Tweet {
    id: ID!
    body: String
    date: Date
    Author: User
    Stats: Stat
}

type User {
    id: ID!
    username: String
    first_name: String
    last_name: String
    full_name: String
    name: String @deprecated
    avatar_url: Url
}

type Stat {
    views: Int
    likes: Int
    retweets: Int
    responses: Int
}

type Notification {
    id: ID
    date: Date
    type: String
}

type Meta {
    count: Int
}

scalar Url
scalar Date

type Query {
    Tweet(id: ID!): Tweet
    Tweets(limit: Int, skip: Int, sort_field: String, sort_order: String): [Tweet]
    TweetsMeta: Meta
    User(id: ID!): User
    Notifications(limit: Int): [Notification]
    NotificationsMeta: Meta
}

type Mutation {
    createTweet (
        body: String
    ): Tweet
    deleteTweet(id: ID!): Tweet
    markTweetRead(id: ID!): Boolean
}
```

---
title: "GraphQL ์์ํ๊ธฐ ๐ฅ"
date: 2021-06-01T16:57:25+09:00
categories: 
- development
- graphQL
tags: 
- development
- front-end
- graphQL
- ๊ทธ๋ํํ์
- API
- web
- restAPI
- query
- mutation
- subscription
keywords: 
- development
- front-end
cover: ""
draft: false
thumbnailImagePosition: left
thumbnailImage: "https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/graphql/img-1.png"
# coverImage: //d1u9biwaxjngwg.cloudfront.net/cover-image-showcase/city.jpg
metaAlignment: center
coverMeta: out
---
<!--toc-->

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/graphql/img-1.png)

# GraphQL


## GraphQL ์ด๋ ?
Graph QL(์ดํ gql)์ Structed Query Language(์ดํ sql)์ ๋ง์ฐฌ๊ฐ์ง๋ก ์ฟผ๋ฆฌ ์ธ์ด์๋๋ค. ํ์ง๋ง gql๊ณผ sql์ ์ธ์ด์  ๊ตฌ์กฐ ์ฐจ์ด๋ ๋งค์ฐ ํฝ๋๋ค. ๋ํ gql๊ณผ sql์ด ์ค์ ์์ ์ฐ์ด๋ ๋ฐฉ์์ ์ฐจ์ด๋ ๋งค์ฐ ํฝ๋๋ค. gql๊ณผ sql์ ์ธ์ด์  ๊ตฌ์กฐ ์ฐจ์ด๊ฐ ํ์ฉ ์ธก๋ฉด์์์ ์ฐจ์ด๋ฅผ ๊ฐ์ ธ์์ต๋๋ค. ์ด ๋์ ์ ์ด์ ํ์ ์๊ธฐ๋ ๋ค๋ฅด๊ณ  ๋ฐฐ๊ฒฝ๋ ๋ค๋ฆ๋๋ค. sql์ ๋ฐ์ดํฐ๋ฒ ์ด์ค ์์คํ์ ์ ์ฅ๋ ๋ฐ์ดํฐ๋ฅผ ํจ์จ์ ์ผ๋ก ๊ฐ์ ธ์ค๋ ๊ฒ์ด ๋ชฉ์ ์ด๊ณ , gql์ ์น ํด๋ผ์ด์ธํธ๊ฐ ๋ฐ์ดํฐ๋ฅผ ์๋ฒ๋ก ๋ถํฐ ํจ์จ์ ์ผ๋ก ๊ฐ์ ธ์ค๋ ๊ฒ์ด ๋ชฉ์ ์๋๋ค. sql์ ๋ฌธ์ฅ(statement)์ ์ฃผ๋ก ๋ฐฑ์ค๋ ์์คํ์์ ์์ฑํ๊ณ  ํธ์ถ ํ๋ ๋ฐ๋ฉด, gql์ ๋ฌธ์ฅ์ ์ฃผ๋ก ํด๋ผ์ด์ธํธ ์์คํ์์ ์์ฑํ๊ณ  ํธ์ถ ํฉ๋๋ค.

## ์ค์น

```
npm init
npm install graphql --save
```

## ์ฌ์ฉ

### query

- ๋ฐ์ดํฐ ์กฐํ. ์ฟผ๋ฆฌ๋ฅผ ํตํ์ฌ ๋ฑ ํ์ํ ๋ฐ์ดํฐ๋ง fetching ์ ํ๊ธฐ ๋๋ฌธ์ overfetch ํน์ underfetch ๋ฅผ ํ  ๊ฑฑ์ ์ ํ  ํ์๊ฐ ์์ต๋๋ค.

{{< alert info >}}
Overfetching : ๋ถํ์ํ ๋ฐ์ดํฐ๊น์ง ๋ค ๋ฐ์์ค๋ ๊ฒ
Underfetching : endpoint๊ฐ ๋ฐ์ดํฐ๋ฅผ ๋ ๋ฐ์์์ ์์ฒญ์ ์ฌ๋ฌ๋ฒ ๋ ๋ฆฌ๋ ๊ฒ
{{< /alert >}}

```
query {
  getOrders(input: {
    status: Pending
  }) {
    ok
    
  }
}
```

### mutation
- ๋ฐ์ดํฐ ์กฐ์. ์ฟผ๋ฆฌ ํ๋๋ ๋ณ๋ ฌ๋ก ์คํ๋์ง๋ง ๋ฎคํ์ด์ ํ๋๋ ํ๋์ฉ ์ฐจ๋ก๋๋ก ์คํ๋๋ค.

```
mutation {
  createOrder(input: {
    restaurantId: 2,
    items:[
      {
        dishId:9
        options: [
          {
            name: "spicy level",
            choice: "little"
          },
          {
            name: "Pickle",
          }
        ]
      }
    ]
  }) {
    ok
    error
  }
}
```

### subscription
- ์ค์๊ฐ ํต์ . ๊ตฌ๋/๋ฐํ ๋ชจ๋ธ์ ๊ธฐ๋ฐ์ผ๋ก WebSocket์ ํตํด ์ค์๊ฐ ์๋ฐฉํฅ ํต์  ๊ธฐ๋ฅ์ ์ ๊ณตํ๋ค. ๊ตฌ๋์ ํตํด ํน์ ํ ์ด๋ฒคํธ๊ฐ ๋ฐ์ํ์ ๋ ์๋ฒ์์ ํด๋ผ์ด์ธํธ๋ก ๋ฐ์ดํฐ๋ฅผ ์ค์๊ฐ์ผ๋ก ํต์ ํ๊ฒ ๋๋ค.

```
subscription {
  hotPotatos
}
```


## REST API VS GraphQL
{{< adsense >}}
REST API๋ URL, METHOD๋ฑ์ ์กฐํฉํ๊ธฐ ๋๋ฌธ์ ๋ค์ํ Endpoint๊ฐ ์กด์ฌ ํฉ๋๋ค. ๋ฐ๋ฉด, gql์ ๋จ ํ๋์ Endpoint๊ฐ ์กด์ฌ ํฉ๋๋ค. ๋ํ, gql API์์๋ ๋ถ๋ฌ์ค๋ ๋ฐ์ดํฐ์ ์ข๋ฅ๋ฅผ ์ฟผ๋ฆฌ ์กฐํฉ์ ํตํด์ ๊ฒฐ์  ํฉ๋๋ค. ์๋ฅผ ๋ค๋ฉด, REST API์์๋ ๊ฐ Endpoint๋ง๋ค ๋ฐ์ดํฐ๋ฒ ์ด์ค SQL ์ฟผ๋ฆฌ๊ฐ ๋ฌ๋ผ์ง๋ ๋ฐ๋ฉด, gql API๋ gql ์คํค๋ง์ ํ์๋ง๋ค ๋ฐ์ดํฐ๋ฒ ์ด์ค SQL ์ฟผ๋ฆฌ๊ฐ ๋ฌ๋ผ์ง๋๋ค.

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/graphql/img-2.png)



์ฐธ๊ณ : [https://tech.kakao.com/2019/08/01/graphql-basic/](https://tech.kakao.com/2019/08/01/graphql-basic/), [๊ณต์๋ฌธ์](https://graphql.org/), [ํ๋ ์ด๊ทธ๋ผ์ด๋](https://www.graphqlbin.com/v2/new), [ํํ ๋ฆฌ์ผ์ฌ์ดํธ](https://www.howtographql.com/)
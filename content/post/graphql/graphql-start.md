---
title: "GraphQL 시작하기 🔥"
date: 2021-06-01T16:57:25+09:00
categories: 
- development
- graphQL
tags: 
- development
- front-end
- graphQL
- 그래프큐엘
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
{{< adsense >}}
![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/graphql/img-1.png)

# GraphQL


## GraphQL 이란 ?
Graph QL(이하 gql)은 Structed Query Language(이하 sql)와 마찬가지로 쿼리 언어입니다. 하지만 gql과 sql의 언어적 구조 차이는 매우 큽니다. 또한 gql과 sql이 실전에서 쓰이는 방식의 차이도 매우 큽니다. gql과 sql의 언어적 구조 차이가 활용 측면에서의 차이를 가져왔습니다. 이 둘은 애초에 탄생 시기도 다르고 배경도 다릅니다. sql은 데이터베이스 시스템에 저장된 데이터를 효율적으로 가져오는 것이 목적이고, gql은 웹 클라이언트가 데이터를 서버로 부터 효율적으로 가져오는 것이 목적입니다. sql의 문장(statement)은 주로 백앤드 시스템에서 작성하고 호출 하는 반면, gql의 문장은 주로 클라이언트 시스템에서 작성하고 호출 합니다.

## 설치

```
npm init
npm install graphql --save
```

## 사용

### query

- 데이터 조회. 쿼리를 통하여 딱 필요한 데이터만 fetching 을 하기 때문에 overfetch 혹은 underfetch 를 할 걱정을 할 필요가 없습니다.

{{< alert info >}}
Overfetching : 불필요한 데이터까지 다 받아오는 것
Underfetching : endpoint가 데이터를 덜 받아와서 요청을 여러번 날리는 것
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
- 데이터 조작. 쿼리 필드는 병렬로 실행되지만 뮤테이션 필드는 하나씩 차례대로 실행된다.

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
- 실시간 통신. 구독/발행 모델을 기반으로 WebSocket을 통해 실시간 양방향 통신 기능을 제공한다. 구독을 통해 특정한 이벤트가 발생했을 때 서버에서 클라이언트로 데이터를 실시간으로 통신하게 된다.

```
subscription {
  hotPotatos
}
```


## REST API VS GraphQL
REST API는 URL, METHOD등을 조합하기 때문에 다양한 Endpoint가 존재 합니다. 반면, gql은 단 하나의 Endpoint가 존재 합니다. 또한, gql API에서는 불러오는 데이터의 종류를 쿼리 조합을 통해서 결정 합니다. 예를 들면, REST API에서는 각 Endpoint마다 데이터베이스 SQL 쿼리가 달라지는 반면, gql API는 gql 스키마의 타입마다 데이터베이스 SQL 쿼리가 달라집니다.

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/graphql/img-2.png)



참고: [https://tech.kakao.com/2019/08/01/graphql-basic/](https://tech.kakao.com/2019/08/01/graphql-basic/), [공식문서](https://graphql.org/), [플레이그라운드](https://www.graphqlbin.com/v2/new), [튜토리얼사이트](https://www.howtographql.com/)
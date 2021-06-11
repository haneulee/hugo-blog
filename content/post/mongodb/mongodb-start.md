---
title: "MongoDB 시작하기 🌱 "
date: 2021-06-04T10:03:44+09:00
categories: 
- development
- mongoDB
tags: 
- development
- front-end
- mongoDB
- database
- server
- noSQL
- schema
- db
keywords: 
- development
- front-end
cover: ""
draft: false
thumbnailImagePosition: left
thumbnailImage: "https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/mongodb/img-1.png"
# coverImage: //d1u9biwaxjngwg.cloudfront.net/cover-image-showcase/city.jpg
metaAlignment: center
coverMeta: out
---
<!--toc-->

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/mongodb/img-1.png)

# MongoDB

## MongoDB 란 ? 
mongoDB는 문서지향(Document-Oriented) 저장소를 제공하는 NoSQL 데이터베이스 시스템으로, 현존하는 NoSQL 데이터베이스 중 인지도 1위를 유지하고 있습니다. mongoDB에서는 데이터가 Document로 불리며, 이 데이터의 집합을 Collection(RDMS에서는 Table)이라고 합니다. 스키마 제약 없이 자유롭고, BSON(Binary JSON) 형태로 각 문서가 저장되며 배열(Array)이나 날짜(Date) 등 기존 RDMS에서 지원하지 않던 형태로도 저장할 수 있기 때문에 JOIN이 필요 없이 한 문서에 좀 더 이해하기 쉬운 형태 그대로 정보를 저장할 수 있다는 것이 특징입니다. 

특히 mongoDB는 문서지향 데이터베이스로, 이것은 객체지향 프로그래밍과 잘 맞고 JSON을 사용할 때 아주 유용합니다. 따라서 자바스크립트를 기반으로 하는 Node.js와 호환이 매우 좋기 때문에, Node.js에서 가장 많이 사용되는 데이터베이스입니다. 물론 mysql 같은 관계형 데이터베이스 사용도 가능합니다.

-----------------------

- Join이 없으므로 Join이 필요 없도록 데이터 구조화가 필요
- 다양한 종류의 쿼리문을 지원(필터링, 수집, 정렬, 정규표현식 등)
- 관리의 편의성
- 스키마 없는(Schemaless) 데이터베이스를 이용한 신속 개발. 필드를 추가하거나 제거하는 것이 매우 쉬워짐
- 쉬운 수평 확장성
- 인덱싱 제공

-----------------------

{{< adsense >}}

## NoSQL
기존의 데이터베이스들은 대부분 관계형 모델에 기반을 두고 있으므로 대부분 SQL이라는 질의문에 의해 데이터베이스를 수정, 갱신, 저장, 검색하도록 구성되어 있습니다. 그러나 최근 들어 이러한 관계형 데이터베이스 모델과는 다른 데이터베이스 관리 시스템에 대한 관심이 증가하고 있는데, 이러한 시스템을 일컬어 NoSQL(Not Only SQL)이라고 부르며 mongoDB는 이러한 데이터베이스 시스템 중 하나입니다. 빅데이터를 다룰 때 RDBMS로만 트래픽을 감당하기 어려워져 이를 해결하기 위해 탄생한 것이 NoSQL입니다. 관계형 데이터 모델을 사용하지 않고 SQL을 사용하지 않는 그 이외의 모든 데이터베이스 시스템 또는 데이터 스토어를 일컬어 NoSQL이라고 칭합니다. 가장 큰 특징은 확장성과 기용성, 높은 성능, 그리고 다양한 데이터 형태를 수용할 수 있다는 것입니다. 

## MongoDB 설치

```
// tapping
brew tap mongodb/brew
brew install mongodb-community
brew services start mongodb-community
// mongo 버전 확인
mongod --version
// mongo 실행
mongo

```

## Mongoose
mongoose란, mongoDB라는 NoSQL 데이터베이스를 지원하는 노드의 확장모듈입니다. mongoose는 mongoDB의 ODM입니다. ODM은 Object Document Mapping의 약자로, 문서를 DB에서 조회할 때 자바스크립트 객체로 바꿔주는 역할을 합니다. mongoDB의 ODM에는 mongodb-native 등 여러 개가 있지만 그중 mongoose가 가장 많이 사용됩니다. 




<br>



참고 : 
[https://edu.goorm.io/learn/lecture/557/%ED%95%9C-%EB%88%88%EC%97%90-%EB%81%9D%EB%82%B4%EB%8A%94-node-js/lesson/174384/mongodb%EB%9E%80](https://edu.goorm.io/learn/lecture/557/%ED%95%9C-%EB%88%88%EC%97%90-%EB%81%9D%EB%82%B4%EB%8A%94-node-js/lesson/174384/mongodb%EB%9E%80), [공식문서](https://docs.mongodb.com/manual/mongo/)
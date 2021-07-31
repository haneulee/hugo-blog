---
title: "Apollo에서 Authentication 인증하기 💫"
date: 2021-07-31T13:57:53+09:00
categories: 
- development
tags: 
- development
- front-end
- @apollo/client
- apollo
- graphql
- Authentication
- 인증
- 토큰
- 로그인
- login
- jwt
keywords: 
- development
- front-end
cover: ""
thumbnailImagePosition: left
thumbnailImage: "https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/graphql/apollo-graphql.png"
# coverImage: //https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/hugo/github-site.png
metaAlignment: center
coverMeta: out
draft: false
---

!--toc-->

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/graphql/apollo-graphql.png)

---

# Apollo에서 Authentication 인증하기 💫

## authLink

백엔드에서 role기반(Host, Listener, Any)의 권한부여를 작업했기 때문에 클라이언트에서도 마찬가지로 서버에게 유저 정보에 대해 알려줘야 합니다.

```ts
import {
  ApolloClient,
  createHttpLink,
  InMemoryCache,
  makeVar,
} from "@apollo/client";
import { LOCALSTORAGE_TOKEN } from "./constants";
import { setContext } from "@apollo/client/link/context";

const token = localStorage.getItem(LOCALSTORAGE_TOKEN);
export const isLoggedInVar = makeVar(Boolean(token));
export const authTokenVar = makeVar(token);

const httpLink = createHttpLink({
  uri: "http://localhost:4000/graphql",
});

const authLink = setContext((_, { headers }) => {
  return {
    headers: {
      ...headers,
      "x-jwt": authTokenVar() || "",
    },
  };
});

export const client = new ApolloClient({
  link: authLink.concat(httpLink),
  cache: new InMemoryCache({
    typePolicies: {
      Query: {
        fields: {
          isLoggedIn: {
            read() {
              return isLoggedInVar();
            },
          },
          token: {
            read() {
              return authTokenVar();
            },
          },
        },
      },
    },
  }),
});
```

위처럼 [authLink](https://www.apollographql.com/docs/react/networking/authentication/)에 setContext를 넘겨줘서 기존의 httpLink과 연결시켜주면 됩니다.  
apollo client에서 Context Link를 사용합니다.

위 코드와 같이 설정을 해주면 이제 request header에는 x-jwt라는 키값에 인증 토큰이 들어가게 되고,  
서버에서는 위 토큰을 받아서 유저 정보를 파악할 수 있게 됩니다.  
그래서 Role 기반 권한부여를 구현할 수 있게 됩니다.

## 팟캐스트 & 에피소드 렌더링

apollo client의 useQuery 훅을 이용하면 쉽게 구현이 가능합니다.  
[useQuery](https://www.apollographql.com/docs/react/api/react/hooks/#usequery)는 함수는 쿼리어(gql)과 옵션 값을 입력 받아, 서버에 전달하여 query 문에 대한 결과 값을 가져옵니다.  
useQuery는 data, loading, errors를 리턴해줍니다.

그 외에도 [refetch](https://www.apollographql.com/blog/apollo-client/caching/when-to-use-refetch-queries/)와 [fetchMore](https://www.apollographql.com/docs/react/pagination/core-api/) 등이 있습니다.  
useQuery의 결과 값으로 솔루션에서는 podcast의 배열 값을 받습니다.  
그 배열값을 javascript의 Array.map을 이용하여 렌더링 합니다.

---

참고:
[https://d2.naver.com/helloworld/4245995](https://d2.naver.com/helloworld/4245995),  
[apollo-hooks로 refetch시키기](https://athilog.github.io/react/apollo-hooks%EB%A1%9C%20refetch%EC%8B%9C%ED%82%A4%EA%B8%B0/),

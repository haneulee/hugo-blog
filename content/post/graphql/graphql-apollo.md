---
title: "GraphQL과 Apollo 함께 쓰기 🔥"
date: 2021-07-21T11:07:36+09:00
categories:
  - development
tags:
  - development
  - front-end
  - frontend
  - graphQL
  - 그래프큐엘
  - API
  - web
  - restAPI
  - query
  - mutation
  - subscription
  - apollo
  - 아폴로
  - reacthookform
  - reactrouterdom
  - useReactiveVar
  - login
  - token
keywords:
  - development
  - front-end
cover: ""
thumbnailImagePosition: left
thumbnailImage: "https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/graphql/apollo-graphql.png"
metaAlignment: center
coverMeta: out
draft: false
---

<!--toc-->

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/graphql/apollo-graphql.png)

---

# GraphQL과 Apollo 함께 쓰기 🔥

## Apollo 란 ?

Apollo란 GraphQL의 클라이언트 라이브러리 중 하나로 GraphQL을 사용한다면 거의 필수적으로 사용하는 상태 관리 플랫폼입니다.

**장점**

- Query 및 Mutation 직접 전송
  - API 서버에서 데이터를 가져오기 위해 번거로운 네트워크단의 HTTP 요청을 신경 쓸 필요가 없어진다.
- 전송받은 데이터 캐싱
  - 클라이언트의 반복 요청을 줄여 서버 부하를 줄일 수 있을 뿐만 아니라, 서비스를 이용하는 사람들에게 더 나은 사용자 경험을 제공할 수 있다.
- Local state 관리
  - 클라이언트 만의 Local state를 만들어 Query, Mutation, Resolver의 사용이 가능하다. 서버에서 받아온 데이터와 클라이언트에서 관리하는 데이터를 병합할 수 있다.

---

## apollo client 설정

typePolicies, Query field가 customizing 설정이 되어 있지만, 필수는 아니기 때문에 uri만 제공해줘도 무방합니다.  
export const client = new ApolloClient({uri, cache: new InMemoryCache()}) 이런식으로만 하셔도 괜찮습니다.  
위와 같이 설정한 client는 앱 최상단에 <ApolloProvider> 컴포넌트로 감싸서 사용하면 됩니다.

```ts
import { ApolloClient, InMemoryCache, makeVar } from "@apollo/client";
import { LS_TOKEN } from "./constants";

const token = localStorage.getItem(LS_TOKEN);
export const isLoggedInVar = makeVar(Boolean(token));
export const authTokenVar = makeVar(token);

export const client = new ApolloClient({
  uri: "https://nuber-eats-challenge.herokuapp.com/graphql",
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

## react router dom 설정

react router dom을 사용하려면 Route를 Router(BrowserRouter, 또는 HashRouter)로 감싸서 사용하시면 됩니다.

```ts
import { BrowserRouter as Router, Route, Switch } from "react-router-dom";
import { Login } from "../pages/login";

export const LoggedOutRouter = () => {
  return (
    <Router>
      <Switch>
        <Route path="/">
          <Login />
        </Route>
      </Switch>
    </Router>
  );
};
```

[BrowserRoute](https://reactrouter.com/web/api/BrowserRouter)  
[HashRouter](https://reactrouter.com/web/api/HashRouter)

{{< adsense >}}

## [reactive variables](https://www.apollographql.com/docs/react/local-state/reactive-variables/) - 로그인 토큰 및 로그인 상태

```ts
export default function App() {
  const isLoggedIn = useReactiveVar(isLoggedInVar);
  return isLoggedIn ? <LoggedInRouter /> : <LoggedOutRouter />;
}
```

**useReactiveVar(reactive variables)** : apollo client의 cache 밖에서의 local state를 다루기 위해 사용

useReactiveVar를 이용하여 로그인 여부를 저장하고, 로그인 하였을 때에는 makeVar로 생성한 변수(isLoggedInVar)에 값을 변형하여 리액트에서 바로바로 반응할 수 있게끔 설정을 해줍니다.

<App> 컴포넌트에서 <LoggedInRouter> 컴포넌트를 사용할지 <LoggedOutRouter>컴포넌트를 사용할 것인지를 결정되게 됩니다. 또한, 로그인 토큰과 관련하여서도 react variables를 사용할 수 있습니다.

makeVar를 이용하여 로그인 토큰도 localStorage에 연결된 token 값에 반응하도록 설정할 수 있습니다.  
이런 방법으로 로그인 토큰이 저장된 로컬 스토리지를 react로 쉽게 연결하여 사용할 수 있습니다.

## 로그인 Mutation

```ts
const LOGIN_MUTATION = gql`
  mutation login($input: LoginInput!) {
    login(input: $input) {
      ok
      error
      token
    }
  }
`;
```

graphql의 mutation을 클라이언트에서 이용하려면 먼저 gql을 사용하여, 쿼리문을 먼저 작성하도록 합니다.  
login은 mutation이므로 useMutation을 사용하시면 됩니다.

```ts
const [login, { data: loginResults, loading }] = useMutation<
  login,
  loginVariables
>(LOGIN_MUTATION, {
  onCompleted,
});
```

typescript를 사용하고 있기 때문에 위와 같이 useMutation에 login, loginVariables 타입을 넘겨줍니다.  
인자로 넘겨준 것은 위의 쿼리어로 만든 LOGIN_MUTATION과 [옵션값](https://www.apollographql.com/docs/react/data/mutations/#options)입니다.

[query/mutation](https://graphql-kr.github.io/learn/queries/)

## [useForm](https://react-hook-form.com/kr/v6/api#useForm) - react hook form

```ts
interface ILoginForm {
  email: string;
  password: string;
}

const { register, handleSubmit, getValues, errors, formState } =
  useForm<ILoginForm>({ mode: "onChange" });
```

useForm 함수는 위와 같이 사용하며 타입스크립트를 지원하기 때문에 위와 같이 타입을 제공해주면 자동완성이 쉽게 되기 때문에 편하고 실수할 일이 적어집니다.

```ts
const onValid = () => {
  const { email, password } = getValues();
  login({
    variables: {
      input: {
        email,
        password,
      },
    },
  });
};

<form className="grid gap-3 w-full max-w-xs" onSubmit={handleSubmit(onValid)}>
  <input
    className="border border-gray-300 focus:outline-none px-5 py-3 focus:border-gray-500 transition-colors duration-500"
    ref={register({
      required: "Email is required",
      pattern:
        /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/,
    })}
    name="email"
    type="email"
    placeholder="Email"
    required
  />
</form>;
```

handleSubmit은 onValid에 form 값이 valid했을 때 data를 같이 넘겨줍니다.  
[register](https://react-hook-form.com/kr/v6/api#register) react hook form에서 중요한 내용입니다.
입력 폼에 사용할 여러 옵션을 설정할 수 있습니다.

---

참고:
[https://www.apollographql.com/](https://www.apollographql.com/),  
[https://www.apollographql.com/docs/react](https://www.apollographql.com/docs/react),

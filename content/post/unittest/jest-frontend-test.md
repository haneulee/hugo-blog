---
title: "Jest Components Test 제스트 컴포넌트 테스트 🔥"
date: 2021-08-07T02:54:15+09:00
categories:
  - development
tags:
  - development
  - front-end
  - unittest
  - jest
  - javascript
  - facebook
  - react
  - nextjs
  - 테스트주도개발
  - 제스트
  - TDD
  - 페이스북
  - 단위테스트
keywords:
  - development
  - front-end
cover: ""
thumbnailImagePosition: left
thumbnailImage: "https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/unittest/img-jest.png"
# coverImage: //https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/hugo/github-site.png
metaAlignment: center
coverMeta: out
draft: false
---

<!--toc-->

# Jest Components Test 제스트 컴포넌트 테스트 🔥

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/unittest/img-jest.png)

## 리액트 컴포넌트 테스트 🏃🏻‍♀️

---

### 기본 구조 및 테스트 방법

- src/pages/**test**/create-account.spec.tsx

```ts
beforeEach(async () => {
  await waitFor(() => {
    mockedClient = createMockClient();
    renderResult = render(
      <ApolloProvider client={mockedClient}>
        <CreateAccount />
      </ApolloProvider>
    );
  });
});
```

frontend 유닛테스트의 기본구조  
apollo client를 이용하여 데이터를 받아오는 부분 때문에 apollo를 mocking 할 필요가 있습니다.  
위와 같은 방법 이외 [MockedProvider](https://www.apollographql.com/docs/react/development-testing/testing/#the-mockedprovider-component)를 이용하는 방법도 있으니 참고 바랍니다.

create-account에서는 유저에게 계정에 대한 입력을 받습니다.  
첫째 입력이 잘못되었을 때, 에러 핸들링을 잘하고 있는가, 둘째 입력이 잘 되었을 때 생성 요청에 대한 핸들링이 잘 되는가를 테스트해야 한다.

---

### create-account의 로직

테스트는 유저에게 입력을 받고 받은 입력이 올바른지 파악해야 합니다.

(1) 올바르지 않다면 에러메세지 출력  
(2) 올바르다면 백엔드에 createAccount Mutation 보내고, 루트 페이지로 이동하기 입니다.

```ts
it("renders OK", async () => {
  await waitFor(() => expect(document.title).toBe("CreateAccount | Podcast"));
});
it("renders validation errors", async () => {});
it("submits mutation with form values", async () => {});
afterAll(() => {
  jest.clearAllMocks(); // test 후 모든 것을 제자리로 돌려 놓음(hooks mock 이후)
});
```

{{< adsense >}}

---

### 유저입력이 올바르지 않을 때 에러 핸들링 테스트

```ts
it("renders validation errors", async () => {
  const { getByRole, getByPlaceholderText } = renderResult;
  const email = getByPlaceholderText(/email/i);
  const button = getByRole("button");
  await waitFor(() => {
    // 여기에선 state가 바뀌는 것을 기다리기 위해 사용
    userEvent.type(email, "wont@work");
  });
  let errorMessage = getByRole("alert");
  expect(errorMessage).toHaveTextContent(/Please enter a valid email/i);
  await waitFor(() => {
    userEvent.clear(email);
  });
  errorMessage = getByRole("alert");
  expect(errorMessage).toHaveTextContent(/Email is required/i);
  await waitFor(() => {
    userEvent.type(email, "working@email.com");
    userEvent.click(button);
  });
  errorMessage = getByRole("alert");
  expect(errorMessage).toHaveTextContent(/Password is required/i);
});
```

위 코드의 renders validation errors에 해당하는 부분입니다.
위 코드의 첫번째 줄 [renderResult](https://testing-library.com/docs/react-testing-library/api/#render-result)는 테스트 셋팅 부분인 beforeEach부분에서 설정된 부분입니다.

렌더링 결과에 대해 html을 선택할 수 있게끔 만들어진 함수 집합들입니다.  
email 엘리먼트는 placeholder가 정규표현식으로 email을 포함하는데, case insensitive하게 검색을 하여 선택을 하였습니다. button은 role 속성이 button인 것을 검색하여 선택하도록 하였습니다. 그리고 email 엘리먼트에는 wont @work 라는 잘못된 이메일을 userEvent를 통해 입력하도록 하여 그 후의 코드에서 테스트 할 수 있게 하였습니다.

---

### 올바른 입력을 받아서 계정 만들기

이번에는 userEvent를 통해 이메일과 패스워드, role에 올바른 입력값들을 넣어주어서 가짜 서버에 createAccount를 요청합니다.

```ts
mockedClient.setRequestHandler(
  CREATE_ACCOUNT_MUTATION,
  mockedCreatedAccountMutationResponse
);
// jest.spyOn(Object, method)..mockImplementation(callback:()=>result);
jest.spyOn(window, "alert").mockImplementation(() => null); // 이렇게 결과값까지 mock할 수 있구나
await waitFor(() => {
  userEvent.type(email, formData.email);
  userEvent.type(password, formData.password);
  userEvent.click(button);
});
```

위 코드에서 mockedClient.setRequestHandler가 보이시나요? apollo client에 CREATE_ACCOUNT_MUTATION이라는 요청이 들어오면 mockedCreatedAccountMutationResponse로 응답을 리턴하라는 의미입니다. 유닛테스트이기 때문에 클라이언트에서 요청하는 서버 응답값은 흉내내는 것입니다.  
그리고 요청한 값들에 대해 제대로 처리 되었는지 확인하면 create account테스트는 완료됩니다.

---

### 패키지 일부함수만 mocking하기

풀커버리지를 해야 하는 것을 고려하면 최대한 많은 부분에서 테스트 해야 합니다.  
그래서 useHistory 역시 테스트 대상입니다.

history.push('/');

history는 react-router-dom 패키지의 useHistory에 있습니다.  
이것을 mocking 하려면 아래 그림의 코드와 같이 해주셔야 합니다.

```ts
// how to mock hooks
const mockPush = jest.fn();
jest.mock("react-router-dom", () => {
  // jest가 module을 전부 cover하면서 beforeEach에서 쓰고 있는 Router까지 고장남
  const realModule = jest.requireActual("react-router-dom"); // 실제 모듈을 필요로 함
  return {
    ...realModule, // 실제 모듈 기능 + mock이 필요한 부분만 mock
    useHistory: () => {
      return { push: mockPush };
    },
  };
});
```

위의 코드처럼 작성을 하시고 expect를 이용하여 history.push를 호출 했는지 여부를 테스트 할 수 있게 되며, 조금더 풀커버리지에 가까워졌습니다.

---

### data fetching

data는 어디서 오죠? 서버에서 gql을 이용하여 끌어 오는거죠? 유닛테스트에서는 거기까지 테스트할 순 없죠? 그럼 mocking하면 됩니다. mocking을 한 후에, mocking한 함수가 호출되었는가? 호출되었는데 내가 원하는 데이터를 입력하고, 원하는 데이터를 받아오나? 체크하시면 됩니다.

데이터 중에 특히나 주의여겨 보셔야 할 것은 **typename 입니다.  
graphql이 데이터 처리를 위해 타입을 확인하는 것이라서 **typename을 지정해주셔야 합니다. 그렇지 않으면 테스트 결과가 원하는대로 처리되지 않을 가능성이 높습니다.
참고. ApolloProvider에 mocked client를 입력한 것이 아니라 MockedProvider를 이용하셨다면 addTypename={false} 옵션을 이용하실 수도 있습니다.

---

### 렌더링 테스트

render함수를 이용하여 renderResult를 받고 나서 원하는 테스트를 하면 됩니다.  
mocking한 client에서 받은 텍스트를 가진 엘리먼트가 있는지 getByText를 이용해도 좋고, 클래스를 찾아도 좋습니다.

---

<주의사항>  
form의 handleSubmit의 콜백함수 같은 경우에는 테스트가 어렵습니다. 안에 들어가있는 콜백함수를 mocking하지 않으니 콜이 되었는지 여부를 모를 수 있습니다. [enzyme](https://enzymejs.github.io/enzyme/)과 같은 패키지를 사용하거나 블루프린트에 세팅되어 있는 test-utils의 fireEvent 등을 이용해서 가능하다고 하는 글도 있지만, handleSubmit안에 있기 때문에 mocking 하기가 쉽지 않습니다.

---

참고 :
[jset 공식문서](https://jestjs.io/docs/api),
[jset mocking](https://www.daleseo.com/jest-fn-spy-on/),

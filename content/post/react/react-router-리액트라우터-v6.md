---
title: "React Router 리액트 라우터 V6"
date: 2022-12-08T18:29:23+01:00
categories:
  - development
tags:
  - development
  - front-end
  - React Router 리액트라우터 V6
keywords:
  - development
  - front-end
cover: ""
thumbnailImagePosition: left
thumbnailImage: "https://res.cloudinary.com/practicaldev/image/fetch/s---dvPKy6Q--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://miro.medium.com/max/1400/0%2AID7KJ8DuspcjB343"
# coverImage: //https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/hugo/github-site.png
metaAlignment: center
coverMeta: out
draft: false
---

<!--toc-->

![](https://res.cloudinary.com/practicaldev/image/fetch/s---dvPKy6Q--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://miro.medium.com/max/1400/0%2AID7KJ8DuspcjB343)

# React Router 리액트 라우터 V6

<!--adsense-->

--- 

## BrowserRouter vs createBrowserRouter

### BrowserRouter

```
import { BrowserRouter, Route, Routes } from "react-router-dom";
import Header from "./components/Header";
import Home from "./components/Home";
import About from "./components/About";

function Router() {
    return (
        <BrowserRouter>
            <Header/>
            <Routes>
                <Route path="/" element={<Home />} />
                <Route path="/about" element={<About />} />
            </Routes>
        </BrowserRouter>
    )
}

export default Router;
```

### createBrowserRouter

{{< alert info >}}
React Router 의 라우터    
DOM History API를 사용하여 URL을 업데이트하고 기록 스택을 관리    
{{< /alert >}}

```
// index.tsx

import React from "react";
import ReactDOM from "react-dom/client";
import router from "./Router";
import { RouterProvider } from "react-router-dom";

const root = ReactDOM.createRoot(
    document.getElementById("root") as HTMLElement
);
root.render(
    <React.StrictMode>
        <RouterProvider router={router} />
    </React.StrictMode>
)

// Router.tsx

import { BrowserRouter, Route, Routes } from "react-router-dom";
import Header from "./components/Header";
import Home from "./components/Home";
import About from "./components/About";
import User from "./components/User";
import Root from "./components/Root";

const router = createBrowserRouter([
    {
        path: "/",
        element: <Root />,
        children: [
            {
                path: "",
                element: <Home />,
            },
            {
                path: "about",
                element: <About />,
            },
            {
                path: "users/:userId",
                element: <User />,
            }
        ]
    }
])

export default router;

// Root.tsx

import React from "react";
import { Outlet } from "react-router-dom";

function Root() {
    return (
        <div>
            <Outlet />
        </div>
    )
}
export default Root;
```

--- 

## errorElement

다른 컴포넌트에서 발생하는 에러로부터 보호  
createBrowserRouter와 같은 데이터 라우터에서만 사용 가능!!  

```
const router = createBrowserRouter([
    {
        path: "/",
        element: <Root />,
        children: [
            {
                path: "",
                element: <Home />,
                errorElement: <ErrorComponent />
            },
            {
                path: "about",
                element: <About />,
            }
        ],
        errorElement: <NotFound />
    }
])
```

--- 

## useNavigate

location.push 대신 useNavigate를 사용할 수 있다.

```
import { useNavigate } from "react-router-dom";

function Header() {
    const navigate = useNavigate();
    const onClick = () => {
        navigate("/about")
    }
}
```

--- 

## useParams

```
import { useParams } from "react-reouter-dom";

function User() {
    const { userId } = useParams();
    return <div>{userId}</div>
}
export default User;
```

--- 

## Outlet

Outlet은 하위 경로 요소를 렌더링하기 위해 상위 경로 요소에서 사용한다.  
하위 경로가 렌더링될 때 상위 경로 컴포넌트에서 중첩된 UI를 보여줄 수 있다.  
상위 경로가 정확히 일치하면 하위 index 경로를 렌더링하거나 index 경로가 없으면 아무것도 렌더링하지 않는다.

- 중복 사용 가능
- Link의 to 경로를 적을 때, "/"를 빼고 적어야 상위 경로를 포함하여 이동한다.

```
// User.tsx
import { Link, useParams, Outlet } from "react-reouter-dom";

function User() {
    const { userId } = useParams();
    return <>
        <div>{userId}</div>
        <Link to="sub"></Link>
        <Outlet />
    </>
}
export default User;

// Router.tsx
const router = createBrowserRouter([
    {
        path: "/",
        element: <Root />,
        children: [
            {
                path: "",
                element: <Home />,
            },
            {
                path: "about",
                element: <About />,
            },
            {
                path: "users/:userId",
                element: <User />,
                children: [
                    {
                        path: "sub",
                        element: <SubUser />
                    }
                ]
            }
        ]
    }
])

// SubUser.tsx
function SubUser() {
    return <>Hello</>
}
export default SubUser;
```

--- 

## useOutletContext

상위 경로 요소에서 하위 경로 요소를 데이터를 보내고 싶을 때 사용!  
원하는 경우 context provider를 만들 수 있지만 Outlet에 기본 제공되는 context를 사용할 수도 있습니다.

```
// User.tsx
import { Link, useParams, Outlet } from "react-reouter-dom";

function User() {
    const { userId } = useParams();
    return <>
        <div>{userId}</div>
        <Link to="sub"></Link>
        <Outlet
            context={{ userName: "test" }}
        />
    </>
}
export default User;

// SubUser.tsx
import { useOutletContext } from "react-reouter-dom";

interface SubUserContext {
    userName: string;
}
function SubUser() {
    const { userName } = useOutletContext<SubUserContext>();
    return <>{userName}</>
}
export default SubUser;
```

--- 

## useSearchParams

useSearchParams 훅은 현재 위치에 대한 URL의 쿼리 문자열을 읽고 수정하는 데 사용한다.  
useState 훅과 마찬가지로 useSearchParams는 현재 위치의 search params와 이를 업데이트하는 데 사용할 수 있는 함수라는 두 가지 값의 배열을 반환한다.  
setSearchParams 함수는 탐색과 같이 작동하지만 URL의 검색 부분에 대해서만 작동한다.  

```
import { Link, useParams, Outlet, useSearch } from "react-reouter-dom";

function User() {
    const { userId } = useParams();
    const [ readSearchParams, setSearchParams ] = useSearchParams();
    setTimeout(() => {
        setSearchParams({
            daty: "today",
            tomorrow: "123",
        })
    }, 3000)
    return <>
        <div>{userId}</div>
        <Link to="sub"></Link>
        <Outlet
            context={{ userName: "test" }}
        />
    </>
}
export default User;
```

--- 

## useLoaderData

useLoaderData 훅을 사용하여 createBrowserRouter의 loader 함수를 호출 할 수 있다.  

--- 

## conclusion ✅

react router dom v6 버전은 기존의 라우팅 기능보다 훨씬 광범위한 기능을 제공하고 있다.  
action을 사용하여 form submit도 할 수 있고, loader를 사용하여 다른 하위 컴포넌트로 데이터를 보낼 수도 있다.  
또한, Remix의 개념을 이번 버전에 많이 반영한 것 같다.  
[Remix](https://remix.run/)도 한번 체크해보기!  




---  

- 참고 :  
  [https://reactrouter.com/en/main/routers/create-browser-router#createbrowserrouter](https://reactrouter.com/en/main/routers/create-browser-router#createbrowserrouter),  
  [https://reactrouter.com/en/main/route/error-element#errorelement](https://reactrouter.com/en/main/route/error-element#errorelement),  
  [https://reactrouter.com/en/main/hooks/use-navigate](https://reactrouter.com/en/main/hooks/use-navigate),  
  [https://reactrouter.com/en/main/hooks/use-params](https://reactrouter.com/en/main/hooks/use-params),  
  [https://reactrouter.com/en/main/components/outlet](https://reactrouter.com/en/main/components/outlet),
  [https://reactrouter.com/en/main/hooks/use-outlet-context](https://reactrouter.com/en/main/hooks/use-outlet-context),
  [https://reactrouter.com/en/main/hooks/use-search-params](https://reactrouter.com/en/main/hooks/use-search-params),  

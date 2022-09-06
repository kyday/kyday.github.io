---
title: React-router-dom v6
categories: [dev]
comments: true
---

## 개요

리액트에서 자주 쓰이는 React-router-dom v6에 대해서 간단하게 정리하려고 한다.
라우팅은 쉽게 설명하면 사용자가 URL (해당 사이트 주소)를 입력을 하면 그거에 맞는 페이지를 보여주는 것을 말한다.

## react-router-dom v6 install

React 프로젝트에서 npm 또는 yarn 패키지 관리를 통해 설치를 할 수 있다.

```
 yarn add react-router-dom@6
```

## BrowserRouter

리액트 프로젝트에서 React Router를 설치하고 나서 대표적으로 BrowserRouter를 많이 사용하고 있고  
웹 브라우저에서 권장 인터페이스로 HTML5를 사용해 URL과 UI를 동기해주는 라우터 컴포넌트이다.
다음과 같이 BrowserRouter를 랩핑을 해야 한다.

```
import { StrictMode } from 'react';
import App from '@src/App';
import { createRoot } from 'react-dom/client';
import { BrowserRouter } from 'react-router-dom';

const container = document.getElementById('root');
const root = createRoot(container);

root.render(
  <StrictMode>
    <BrowserRouter>
      <App />
    </BrowserRouter>
  </StrictMode>,
);

```

## Routes / Route

React Router에서 렌더링을 하는 주요 방법중에 하나로 path에 따라서 (사용자가 입력하는 주소를 감지하는 역할) UI를 보여주는 라우팅 기능을 한다.
위치가 변경될 때마다 `<Routes>` 컴포넌트에 모든 children `<Route>` 를 살펴보고나서 가장 일치하는 항목을 찾기 렌더링 한다.
다음과 같이 설정할 수 있고 `path="*"` 라우터가 일치하는 정보가 없을 경우에 사용할 수 있고, 여러 라우팅을 매칭할 때 역시 URL 뒤에 `*` 을 붙이면 된다.
element에는 path에 따라서 컴포넌트를 지정할 수 있다.

```
import React from "react";
import { BrowserRouter, Route, Routes } from "react-router-dom";

 <Routes>
        <Route path="/" element={<Main />} />
        <Route path="/home/*" element={<Home />} />
        <Route path="/*" element={<NotFound />} />
  </Routes>

```

## Link / NavLink

- Link 컴포넌트는 브라우저의 주소만 변경할 뿐, 페이지를 새로 불러오지는 않는다.
  NavLink 컴포넌트는 Link 컴포넌트와는 달리 스타일을 적용할 수 있다.

- Rename `<NavLink exact>` to `<NavLink end>` 으로 이름이 변경되었다.

```
<NavLink
  to="/messages"
- style={{ color: 'blue' }}
- activeStyle={{ color: 'green' }}
+ style={({ isActive }) => ({ color: isActive ? 'green' : 'blue' })}
>
  Messages
</NavLink>
```

```
<NavLink
  to="/messages"
- className="nav-link"
- activeClassName="activated"
+ className={({ isActive }) => "nav-link" + (isActive ? " activated" : "")}
>
  Messages
</NavLink>
```

## useLocation

React Router에서 현재 사용자가 머물고 있는 URL에 대한 정보를 알려주는 hooks이다.
다음과 같이 객체 형태로 데이터를 받을 수 있다.

```
{
  hash: ""
  pathname: ""
  search: ""
  state: ""
}
```

## useParams

useParams는 동적 라우팅을 할 때 사용할 수 있는 hooks로 보통 list page에서 detail 페이지로 넘어갈 때
특정 값이 추가되어 해당하는 각기 다른 id 값으로 페이지를 이동할 수 있다.

```
import * as React from 'react';
import { Routes, Route, useParams } from 'react-router-dom';

function ProfilePage() {
  // Get the userId param from the URL.
  let { userId } = useParams();
  // ...
}

function App() {
  return (
    <Routes>
      <Route path="users">
        <Route path="/info/:userId" element={<ProfilePage />} />
        <Route path="me" element={...} />
      </Route>
    </Routes>
  );
}
```

## useNavigate

useNavigate를 이용해서 페이지를 이동 시킬 수 있는 hooks이다.
인자에 정수를 넣어줘서 이동 시킬 수도 있다.

```
navigate(-1); // 뒤로가기
navigate(-2); // 뒤로 2페이지 가기
navigate(1); // 앞으로 가기
```

```
import { useNavigate } from "react-router-dom";

function SignupForm() {
  const navigate = useNavigate();

  async function handleSubmit(event) {
    event.preventDefault();
    await submitForm(event.target);
    navigate("../success", { replace: true });
  }

  return <form onSubmit={handleSubmit}>{/* ... */}</form>;
}
```

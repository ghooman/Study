## 📌 react-router-dom
React는 SPA(Single Page Application)이다.   
react-router-dom은 SPA에서 화면 전환을 위해 사용하는 모듈이다.   
***
### 설치 및 라우터 시작
```
npm install react-router-dom@6
```
위 커맨드로 라우터를 설치한다.
```javascript
// index.js

import { BrowserRouter } from 'react-router-dom';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <BrowserRouter>
    <App />
  </BrowserRouter>
);
```
그리고 index.js(도입부)에서 아래와 같이 라우터를 사용하겠다고 알려준다.   
BrowserRouter는 Router를 사용하겠다는 전체적인 Wrap과 같은 거다.   
이때 중요한것이 Import에 'react-router-dom'을 해줘야한다.   
***
### 예시 페이지
```javascript
//Home.js

import React from "react";

const Home = () => {
  return (
    <div>
      <h1>HOME!! 🏠</h1>
      <p>가장 먼저 보이는 페이지</p>
    </div>
  );
};
export default Home;
```
```javascript
// About.js

import React from "react";
const About = () => {
  return (
    <div>
      <h1>소개</h1>
      <p>이 프로젝트는 리액트를 공부하는 용으로 사용됩니다. </p>
    </div>
  );
};
export default About;
```
***
### App.js
```javascript
import { Routes, Route, Link } from "react-router-dom";
import About from "./route/About";
import Home from "./route/Home";

const App = () => {
  return (
    <div>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />}/>
      </Routes>
    </div>
  );
};

export default App;
```
1. 우선 상단에서 여러가지 컴포넌트를 import 해오고
2. <Routes> 만들고 그 안에 <Route>를 작성한다.
3. <Route path="/url경로" element={ <보여줄html> } /> 이렇게 작성하면 된다.
***

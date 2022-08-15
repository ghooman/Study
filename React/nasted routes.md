## nasted routes
서브경로 만들 수 있는 중첩 라우트다.

### 사용법
예를 들어서   

/about/member로 접속하면 회사멤버 소개하는 페이지   
/about/location으로 접속하면 회사위치 소개하는 페이지   

를 만들고 싶다고 해보자.
```javascript
<Route path="/about/member" element={ <div>멤버들</div> } />
<Route path="/about/location" element={ <div>회사위치</div> } />
```
이렇게 만들어도 되겠지만
```javascript
<Route path="/about" element={ <About/> } >  
  <Route path="member" element={ <div>멤버들</div> } />
  <Route path="location" element={ <div>회사위치</div> } />
</Route>
```
이렇게 만들어도 된다.   
<br/>
Route안에 Route를 넣을 수 있는데 이걸 Nested routes라고 부른다.   
저렇게 쓰면   
/about/member로 접속시 `<About> & <div>멤버들</div>`을 보여준다.   
/about/location으로 접속시 `<About> & <div>회사위치</div>`을 보여준다.   

**💡 여기서 중요한 점은 nested된 것이 어디에 보여줄지 표기해야 잘 보여진다. 💡**
```javascript
// About.js

import { Outlet } from "react-router-dom"

function About(){
  return (
    <div>
      <h4>about페이지임</h4>
      <Outlet></Outlet>
    </div>
  )
}
```
위에서 import해온 Outlet은 nested routes안의 element들을 어디에 보여줄지 표기하는 곳이다.   
그래서 이렇게 해두면   
/about/member로 접속시 Outlet자리에 아까의 div 박스들이 잘 보인다.   
그래서 유사한 서브페이지들이 많이 필요하다면 이렇게 만들어도 된다.

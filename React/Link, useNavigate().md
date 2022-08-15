## 📌 Link
유저들은 주소창에 url 입력해서 들어가지 않고 링크타고 들어간다.   
링크를 만들고 싶으면 react-router-dom에서 Link 컴포넌트 import 해오고 원하는 곳에서 `<Link>` 쓰면 된다.   
```javascript
<Link to="/">홈</Link>
<Link to="/detail">상세페이지</Link>
```
이러면 각각 url 경로로 이동하는 링크를 생성할 수 있다.
***
##  📌 useNavigate()
페이지 이동은 Link 써도 되지만 그게 못생겼으면 이거 쓰면 된다.
```javascript
import { useNavigate } from "react-router-dom"

function App(){
  let navigate = useNavigate()
  
  return (
    (생략)
    <button onClick={()=>{ navigate('/detail') }}>이동버튼</button>
  )
}
```
우선 useNavigate를 "react-router-dom"에서 import해오고   
navigate(일반적으로 많이 씀)변수에 할당한다.   
useNavigate() 쓰면 그 자리에 유용한 함수가 남는다. 페이지 이동시켜주는 함수이다.   
그럼 이제 navigate('/detail') 이런 코드가 실행되면 /detail 페이지로 이동가능하다.   
navigate(2) 숫자넣으면 앞으로가기, 뒤로가기 기능개발도 가능하다.   
-1 넣으면 뒤로 1번 가기   
2 넣으면 앞으로 2번 가기 기능이다. 

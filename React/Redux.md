## 📌 Redux
공식문서를 참조한 정의는 다음과 같다.   
>  자바스크립트로 구동되는 어플리케이션에서 예측 가능한 상태관리를 도와주는 상태관리 라이브러리

쉽게 말하면 Redux는 props 없이 state를 공유할 수 있게 도와주는 라이브러리이다.   
<img width="364" alt="캡처" src="https://user-images.githubusercontent.com/85857465/180614082-583c3571-f37b-49b4-9614-8abdd869e885.png">   
이거 설치하면 js 파일 하나에 state들을 보관할 수 있는데 그걸 모든 컴포넌트가 직접 꺼내쓸 수 있다.   
그래서 귀찮은 props 전송이 필요없어진다. (컴포넌트가 많아질 수록 좋겠다.)   
그래서 사이트가 커지면 쓸 수 밖에 없어서 개발자 구인시에도 redux같은 라이브러리 숙련도를 대부분 요구한다고 한다.
***
**✔️ 설치**
```
npm install @reduxjs/toolkit react-redux
```
터미널에 입력하면 된다.   
참고로 `redux toolkit`이라는 라이브러리를 설치할 건데 redux의 개선버전이라고 보면 된다.(문법이 좀 더 쉬워짐)   
근데 설치하기 전에 package.json 파일을 열어서   

"react"
"react-dom" 

항목의 버전을 확인해야 된다.   

이거 두개가 18.1.x 이상이면 사용 가능하다.
***
**✔️ 셋팅**   
src폴더에 store.js파일(state들을 보관하는 파일이다.)을 만들어서 아래 코드를 복붙한다.
```javascript
import { configureStore } from '@reduxjs/toolkit'

export default configureStore({
  reducer: { }
}) 
```

`index.js` 파일을 밑에 처럼 작성해 준다.
```javascript
import { Provider } from "react-redux";
import store from './store.js'

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
    <Provider store={store}>
      <BrowserRouter>
        <App />
      </BrowserRouter>
    </Provider>
  </React.StrictMode>
); 
```
Provider라는 컴포넌트와 store.js를 import해온다.   
그리고 밑에 <Provider store={import해온거}> 이걸로 <App/> 을 감싸면 된다.   
그럼 이제 <App>과 그 모든 자식컴포넌트들은 store.js에 있던 state를 맘대로 꺼내쓸 수 있다.
***
**✔️ 사용법**
>Redux store에 state 보관하는 법 

store.js 파일 열어서 이렇게 코드짜면 state 하나 만들 수 있다.   

step 1. createSlice( ) 로 state 만들고   
step 2. configureStore( ) 안에 등록하면 된다.
```javascript
import { configureStore, createSlice } from '@reduxjs/toolkit'

let user = createSlice({
  name : 'user',
  initialState : 'kim'
})

export default configureStore({
  reducer: {
    user : user.reducer
  }
})
```
1. createSlice() 상단에서 import 해온 다음에   
{ name : 'state이름', initialState : 'state값' } 넣으면 state 하나 생성 가능하다.     
(createSlice()는 useState() 와 용도가 비슷하다고 보면 된다.)   

2. state 등록은 configureStore() 안에 하면 된다.   
{ 작명 : createSlice만든거.reducer } 이러면 등록 끝이다.   
여기 등록한 state는 모든 컴포넌트가 자유롭게 사용 가능하다.   

>Redux store에 있던 state 가져다쓰는 법
```javascript
import { useSelector } from "react-redux"

function Cart(){
  let a = useSelector((state) => { return state })
  console.log(a)

  return (생략)
}
```

아무 컴포넌트에서 상단에 useSelctor를 import해오고   
useSelector((state) => { return state } ) 쓰면 store에 있던 모든 state가 그 자리에 남는다.   
출력해 보면 { user : 'kim' } 출력 된다.

```javascript
let a = useSelector((state) => state.user)
```
이런식으로 쓰면 kim이 출력 된다.

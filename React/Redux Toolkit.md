## 📌 Redux
공식문서를 참조한 정의는 다음과 같다.   
>  자바스크립트로 구동되는 어플리케이션에서 예측 가능한 상태관리를 도와주는 상태관리 라이브러리

쉽게 말하면 Redux는 props 없이 state를 공유할 수 있게 도와주는 라이브러리이다.   
<img width="364" alt="캡처" src="https://user-images.githubusercontent.com/85857465/180614082-583c3571-f37b-49b4-9614-8abdd869e885.png">   
이거 설치하면 js 파일 하나에 state들을 보관할 수 있는데 그걸 모든 컴포넌트가 직접 꺼내쓸 수 있다.   
그래서 귀찮은 props 전송이 필요없어진다. (컴포넌트가 많아질 수록 좋겠다.)   
그래서 사이트가 커지면 쓸 수 밖에 없어서 개발자 구인시에도 redux같은 라이브러리 숙련도를 대부분 요구한다고 한다.
***
## 📌 Redux Toolkit
Redux Toolkit은 Redux를 더 사용하기 쉽게 만들기 위해 Redux에서 공식 제공하는 개발도구이다.    
Redux Toolkit은 아래와 같은 Redux의 단점을 보완하고자 만들어졌다.
- 리덕스의 복잡한 스토어 설정
- 리덕스를 유용하게 사용하기 위해서 추가되어야 하는 많은 패키지들
- 리덕스 사용을 위해 요구되는 다량의 상용구(boilerplate) 코드들

이러한 Redux의 한계를 깨닫고 "효율적인 Redux 개발을 위한 공식적이고 독단적인 배터리 포함 도구 세트" Redux Toolkit (RTK)가 개발되었다.
***
### ✔️ 설치
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
### ✔️ 셋팅
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
그리고 밑에 <Provider store={import해온거}> 이걸로 App 컴포넌트를 감싸면 된다.   
그럼 이제 App 컴포넌트와 그 모든 자식 컴포넌트들은 store.js에 있던 state를 맘대로 꺼내쓸 수 있다.
***
### ✔️ 사용법
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

>Redux store에 있던 state 가져다 쓰는 법
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
***
### ✔️ store의 state 변경하는 법   
>1. store.js 안에 state 수정해주는 함수부터 만든다.
```javascript
let user = createSlice({
  name : 'user',
  initialState : 'kim',
  reducers : {
    changeName(state){
      return 'john ' + state
    }
  }
}) 
```
slice 안에 reducers: { } 열고 거기 안에 함수 만들면 된다.   
- 함수 작명 마음대로 한다.   
- 파라미터 하나 작명하면 그건 기존 state가 된다.   
- return 우측에 새로운 state 입력하면 그걸로 기존 state를 갈아치워준다.   

이제 changeName() 쓸 때 마다 'kim' -> 'john kim' 이렇게 변한다.   

>2. 다른 곳에서 쓰기좋게 export 해둔다.
```javascript
export let { changeName } = user.actions
```
이런 코드를 store.js 밑에 추가하면 된다.   
slice이름.actions 라고 적으면 state 변경함수가 전부 그 자리에 출력된다.   
그걸 변수에 저장했다가 export 하라는 뜻이다.   

>3. 원할 때 import 해서 사용한다. dispatch()로 감싸서 사용해야 된다.

예를 들어서 Cart.js 에서 버튼같은거 하나 만들고
그 버튼 누르면 state를 'kim' -> 'john kim' 이렇게 변경하고 싶으면
```javascript
(Cart.js)

import { useDispatch, useSelector } from "react-redux"
import { changeName } from "./../store.js"

(생략) 

<button onClick={()=>{
  dispatch(changeName())
}}>버튼임</button>
```
이렇게 코드짜면 된다.
- store.js에서 원하는 state변경함수 가져오면 되고   
- useDispatch 라는 것도 라이브러리에서 가져온다.   
- 그리고 dispatch( state변경함수() ) 이렇게 감싸서 실행하면 state 진짜로 변경된다. 
***
### ✔️ redux state가 array/object인 경우 변경하는 법
{name : 'kim', age : 20} 이렇게 생긴 자료를 state로 만들어본다.   
'kim' -> 'park' 이렇게 변경하고 싶으면
```javascript
let user = createSlice({
  name : 'user',
  initialState : {name : 'kim', age : 20},
  reducers : {
    changeName(state){
      return {name : 'park', age : 20}
    }
  }
}) 
```
이렇게 쓰면 changeName() 사용시 변경된다.   
return 오른쪽에 적은걸로 기존 state를 바꿔주기 때문이다.   
  
```javascript
let user = createSlice({
  name : 'user',
  initialState : {name : 'kim', age : 20},
  reducers : {
    changeName(state){
      state.name = 'park'
    }
  }
}) 
```
근데 state를 직접 수정해도 변경이 잘 된다.   
state를 직접 수정하는 문법을 사용해도 잘 변경되는 이유는   
Immer.js라는 라이브러리가 state 사본을 하나 더 생성해준 덕분인데 Redux 설치하면 딸려와서 그렇다고 한다.   

그래서 결론은 array/object 자료의 경우 state변경은   
state를 직접 수정해도 잘 되니까 직접 수정하면 된다.
***
### ✔️ state 변경함수가 여러개 필요한 경우
예를 들어서 +1 하는 기능 또는 +10, +100을 하는 기능을 만들고 싶으면   
여러개의 함수를 만들지 않고 파라미터문법 이용하면 비슷한 함수 여러개 만들 필요가 없다고 한다.   

state변경함수에도 파라미터문법 사용가능함.
```javascript
let user = createSlice({
  name : 'user',
  initialState : {name : 'kim', age : 20},
  reducers : {
    increase(state, a){
      state.age += a.payload
    }
  }
}) 
```
state변경함수의 둘째 파라미터를 작명하면 이제   
increase(10)   
increase(100)   
이런 식으로 파라미터입력을 해서 함수사용이 가능하다.   
파라미터자리에 넣은 자료들은 a.payload 하면 나온다.   

(참고)   
- a 말고 action 이런 식으로 작명 많이 한다고 한다. 
- action.type 하면 state변경함수 이름이 나오고
- action.payload 하면 파라미터가 나온다.

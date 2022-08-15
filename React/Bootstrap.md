## 📌 Bootstrap
반응형 웹 디자인을 위해 css의 클래스 선택자에 정의된 스타일시트와 자바스크립트 플러그인의 라이브러리   

설치하면 버튼디자인 메뉴디자인 직접 할 필요없이   
Bootstrap 홈페이지에 있는 예제코드만 복붙하면 메뉴, 버튼, 3분할 레이아웃 등 원하는 UI들을 쉽게 생성가능하다.   
***
### ✔️ 설치
Bootstrap은 원조라이브러리고
이걸 리액트에 맞게 변형한 React Bootstrap을 설치한다.   

react bootstrap이라고 구글 검색하면 맨 처음에 나오는 사이트에 접속한다. https://react-bootstrap.github.io/   
그리고 get started 혹은 introduction 메뉴로 들어가서 설치 방법을 따라한다.   
```
npm install react-bootstrap bootstrap 
```
에디터에서 터미널 열고 위에처럼 입력한다.(명령어 맨날 바뀌니까 사이트 들어가서 확인해야한다.)   

어떤 스타일은 Bootstrap CSS 파일을 요구하는 경우가 있다.   
그래서 그냥 그 사이트에 있는 CSS 파일을 index.html 파일의 head 태그 안에 복붙해면 된다.   
```javascript
<link
  rel="stylesheet"
  href="https://cdn.jsdelivr.net/npm/bootstrap@5.2.0-beta1/dist/css/bootstrap.min.css"
  integrity="sha384-0evHe/X+R7YkIZDRvuzKMRqM+OrBnVFBL6DOitfPri4tjfHxaWutUpFmBp4vmVor"
  crossorigin="anonymous"
/>
```
길어서 싫으면 App.js에
`import 'bootstrap/dist/css/bootstrap.min.css';`
이렇게 작성해도 된다.
***
### ✔️ 사용법
버튼이 필요하면 React-Bootstrap 사이트에서 검색해서 예제코드를 복붙하면 버튼 생성 끝이다.   
`<Button variant="primary">Primary</Button>` 이런거 복사붙여넣기하면 파란 버튼이 나온다.   

```javascript
import {Button} from 'react-bootstrap'

function App(){
  return (
    <div>
      <Button variant="primary">Primary</Button>
    </div>
  )
}
```
다만 복사붙여넣기할 때 대문자로 시작하는 컴포넌트 이름은 상단에 import 해와야한다.

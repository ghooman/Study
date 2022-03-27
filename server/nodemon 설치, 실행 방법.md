## nodemon
개발시에 코드를 수정하고 서버를 껐다가 다시 켜야하는게 매우 번거롭기 때문에 코드 수정이 있으면 서버를 자동으로 restart해주는 모듈.   
`설치 방법은 다음과 같다.`

>npm install nodemon -g

설치하고 난 뒤, 터미널에 다음과 같이 입력하면 연결이 가능하다.
>nodemon server/basic-server.js

다른 방법도 있다.   

`package.json`안에 script부분을 다음과 같이 작성해주면 서버를 실행시킬 때 명령어를 다음과 같이 할 수 있다.   
![스크린샷 2022-03-28 오전 3 48 10](https://user-images.githubusercontent.com/85857465/160296076-3bcbbeb1-fffc-48f3-be69-ee9dc90be594.png)   
`start 부분 작성`   
그리고 터미널에는 npm start 만 써주면 된다.

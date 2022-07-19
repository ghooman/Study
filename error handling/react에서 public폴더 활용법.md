리액트로 개발을 끝내면 build 작업이라는걸 하는데 지금까지 짰던 코드를 한 파일로 압축해주는 작업이다.   
src 폴더에 있던 코드와 파일은 다 압축이 되는데 public 폴더에 있는 것들은 그대로 보존해준다.   
그래서 형태를 보존하고 싶은 파일은 public 폴더에 넣으면 되는데 js 파일은 그럴 일은 거의 없고 이미지, txt, json 등 수정이 필요없는 static 파일들의 경우엔 public 폴더에 보관해도 상관없다.

>public 폴더에 있는 이미지 사용할 땐
```javascript
<img src="/logo192.png" /> 
```
그냥 /이미지경로 사용하면 된다.   
그래서 페이지에 이미지 100장을 넣어야하는 경우 public 폴더에 밀어넣으면 import 100번 안해도 되니 편리하다.   
css 파일에서도 /이미지경로 사용하면 된다.

하지만 권장되는 방식은 이렇다.
```javascript
<img src={process.env.PUBLIC_URL + '/logo192.png'} /> 
```

왜냐면 리액트로 만든 html 페이지를 배포할 때 ghoopark.com 경로에 배포하면 아무런 문제가 없지만   
ghoopark.com/어쩌구/ 경로에 배포하면 /logo192.png 이렇게 쓰면 파일을 찾을 수 없다고 나올 수도 있다.   
그래서 /어쩌구/ 를 뜻하는 process.env.PUBLIC_URL 이것도 더해주면 된다고 한다.(공식사이트 참조)   

ghoopark.com/어쩌구/ 경로에 리액트로 만든 페이지를 배포할 일이 아예 없으면 굳이 안해도 된다.

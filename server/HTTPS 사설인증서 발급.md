## 📌 HTTPS 사설인증서 발급
MacOS 사용자 기준   
홈브류 통해 설치 가능

### 1. mkcert 설치
$ brew install mkcert   

---
### 2. $ mkcert -install
---
### 3. 로컬호스트
$ mkcert -key-file key.pem -cert-file cert.pem localhost 127.0.0.1 ::1   

이제 그럼 두개의 키다 생성된다.   

cert.pem <-공개키
key.pem <-개인키   

key.pem은 개인키 이기 때문에 절대 깃에 올라가지 않아야 한다.
cert.pem은 공개키로 공개되어되 상관없다.   

키를 발급받으면 계속 쓰기 때문에 다시 설치 받을필요 없이 이 키를 필요한곳에 잘 복사 붙혀넣기 하면 된다.   

---
### 4. HTTPS 서버작성
키를 발급 받았으면 서버에 적용하는 작업이 필요하다.   

**1) Node.js https 모듈 이용**
```javascript
const https = require('https');
const fs = require('fs');

https
  .createServer(
    {
      key: fs.readFileSync(__dirname + '/key.pem', 'utf-8'),
      cert: fs.readFileSync(__dirname + '/cert.pem', 'utf-8'),
    },
    function (req, res) {
      res.write('Congrats! You made https server now :)');
      res.end();
    }
  )
  .listen(3001);
```

접속하면 URI창 왼쪽에 좌물쇠가 보인다.   

**2) express.js 이용**
```javascript
const https = require('https');
const fs = require('fs');
const express = require('express');

const app = express();

https
  .createServer(
    {
      key: fs.readFileSync(__dirname + '/key.pem', 'utf-8'),
      cert: fs.readFileSync(__dirname + '/cert.pem', 'utf-8'),
    },
    app.use('/', (req, res) => {
      res.send('Congrats! You made https server now :)');
    })
  )
  .listen(3001);
```

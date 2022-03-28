# 📌 HTTP 트랜잭션 해부
[HTTP 트랜잭션 해부](https://nodejs.org/ko/docs/guides/anatomy-of-an-http-transaction/) 참고.

---
### 1. 서버 생성
모든 node 웹 서버 애플리케이션은 웹 서버 객체를 만들어야 한다. 이 때 createServer를 이용한다.   
```javascript
const http = require('http');

const server = http.createServer((request, response) => {
  // 여기서 작업이 진행됩니다!
});
```
이 서버로 오는 `HTTP` 요청마다 `createServer`에 전달된 함수가 한 번씩 호출된다. `HTTP` 요청이 서버에 오면 `node`가 트랜잭션을 다루려고 `request`와 `response` 객체를 전달하며 요청 핸들러 함수를 호출한다. 요청을 실제로 처리하려면 `listen` 메서드가 `server` 객체에서 호출되어야 한다. 대부분은 서버가 사용하고자 하는 포트 번호를 `listen`에 전달하기만 하면 된다.   

---
### 2. 메서드, URL, 헤더
요청을 처리할 때, 우선 메서드와 `URL`을 확인한 후 이와 관련된 적절한 작업을 실행해야한다. `node`는 `request` 객체에 각 프로퍼티를 넣어두었으므로 쉽게 작업 가능하다.
```javascript
const { method, url } = request;

const { headers } = request;
const userAgent = headers['user-agent'];
```
여기서 `method`는 일반적인 `HTTP` 메서드/동사가 될 것이고, `url`은 전체 `URL`에서 서버, 프로토콜, 포트를 제외한 것으로, 세 번째 슬래시 이후의 나머지 전부이다.   

`request`에 `headers`라는 전용 객체가 있고, 클라이언트가 어떻게 헤더를 설정했는지에 관계없이 모든 헤더는 소문자로만 표현된다는 것을 기억하자. 이는 어떤 목적이든 헤더를 파싱하는 작업을 간편하게 해준다.

---
### 3. 요청 바디
`POST`나 `PUT` 요청을 받을 때 애플리케이션에 요청 바디는 중요할 것이다. 핸들러에 전달된 `request` 객체는 `ReadableStream` 인터페이스를 구현하고 있는데, 이 스트림의 `'data'`와 `'end'` 이벤트에 이벤트 리스너를 등록해서 데이터를 받을 수 있다.   

각 `'data'` 이벤트에서 발생시킨 청크는 `Buffer`이다. 이 청크는 문자열 데이터이므로 이 데이터를 배열에 담고, `'end'` 이벤트에서 이어 붙인 다음 문자열로 만드는 것이 가장 좋다.
```javascript
let body = [];
request.on('data', (chunk) => {
  body.push(chunk);
}).on('end', () => {
  body = Buffer.concat(body).toString();
  // 여기서 `body`에 전체 요청 바디가 문자열로 담겨있습니다.
});
```

# 📌 Mini Node Server
이번에 만들어야할 웹 서버의 기능은 매우 단순했다. 버튼을 클릭함에 따라 각기 다른 요청을 보내며, 각각 보낸 단어를 소문자 또는 대문자로 바꾸면 되는 것이었다.   
![mini-node-server](https://user-images.githubusercontent.com/85857465/160459136-2fb9be64-0aa7-4952-bcfa-1dc21febb2fa.gif)   

### Sprint 구현하기
<img width="424" alt="스크린샷 2022-03-29 오전 3 03 32" src="https://user-images.githubusercontent.com/85857465/160459326-9a452994-b691-4426-befd-965c3b60a25a.png">   

`URL`이 `/lower`이고, `POST` 요청이 왔다면 서버는 문자열을 소문자로 만들어 응답해야 했고, `URL`이 `/upper`인 `POST` 요청에는 문자열을 대문자로 만들어 응답해야 했다. 또한, `CORS` 관련 헤더를 `OPTIONS` 응답에 적용해야 했다.   

따라서, 먼저 `Method`가 `POST`인지 `OPTIONS`인지 분기하고, `POST` 요청이 왔다면 `URL`을 확인하고 알맞은 요청을 보내주는 식으로 구현했다.
```javascript
const http = require('http');
const PORT = 5000;
const ip = 'localhost';

const server = http.createServer((request, response) => {
  if (request.method === 'OPTIONS') {
    // 클라이언트의 preflight request에 대한 응답을 돌려준다
    response.writeHead(200, defaultCorsHeader);
    response.end();
  }
  if (request.method === 'POST') {
    let body = [];
    request
      .on('data', (chunk) => {
        // 위의 HTTP 트랜잭션 해부 문서에서 공부했던 것처럼,
        // body 배열에 chunk를 담고
        body.push(chunk);
      })
      .on('end', () => {
        // end 이벤트에서 이어 붙이고 문자열로 만든다
        body = Buffer.concat(body).toString();
        response.writeHead(201, defaultCorsHeader);
        if (request.url === '/lower') {
          response.end(body.toLowerCase());
        } else if (request.url === '/upper') {
          response.end(body.toUpperCase());
        } else {
          response.writeHead(404, defaultCorsHeader);
          response.end();
        }
      });
  }
});

server.listen(PORT, ip, () => {
  console.log(`http server listen on ${ip}:${PORT}`);
});

// 응답 헤더
const defaultCorsHeader = {
  'Access-Control-Allow-Origin': '*',
  'Access-Control-Allow-Methods': 'GET, POST, PUT, DELETE, OPTIONS',
  'Access-Control-Allow-Headers': 'Content-Type, Accept',
  'Access-Control-Max-Age': 10,
};
```

**reference code**   
이 코드는 애초에 문자열 변수 `data`를 선언하여 `'data'` 이벤트에서 `chunk`를 더해주고, `'end'` 이벤트에서 그 `data`를 소문자 혹은 대문자로 바꾸어 응답하는 형태의 코드이다. 훨씬 간단하게 구현한 모습이다.
```javascript
const http = require('http');
const PORT = 5000;
const ip = 'localhost';

const server = http.createServer((req, res) => {
  if (req.method === 'POST') {
    if (req.url === '/lower') {
      let data = '';
      req.on('data', chunk => {
        data = data + chunk;
      });
      req.on('end', () => {
        data = data.toLowerCase();
        res.writeHead(201, defaultCorsHeader);
        res.end(data);
      });
    } else if (req.url === '/upper') {
      let data = '';
      req.on('data', chunk => {
        data = data + chunk;
      });
      req.on('end', () => {
        data = data.toUpperCase();
        res.writeHead(201, defaultCorsHeader);
        res.end(data);
      });
    } else {
      res.writeHead(404, defaultCorsHeader);
      res.end();
    }
  }
  if (req.method === 'OPTIONS') {
    res.writeHead(200, defaultCorsHeader);
    res.end();
  }
});

server.listen(PORT, ip, () => {
  console.log(`http server listen on ${ip}:${PORT}`);
});

const defaultCorsHeader = {
  'Access-Control-Allow-Origin': '*',
  'Access-Control-Allow-Methods': 'GET, POST, PUT, DELETE, OPTIONS',
  'Access-Control-Allow-Headers': 'Content-Type, Accept',
  'Access-Control-Max-Age': 10
};
```

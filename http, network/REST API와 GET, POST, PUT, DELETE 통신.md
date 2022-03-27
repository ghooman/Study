## 📌 REST (Representational State Transfer)
REST API는 웹에서 데이터를 전송 및 처리하는 방법을 정의한 인터페이스를 말한다.   
모든 데이터 구조와 처리방식은 REST에서 URL을 통해 정의되며, 그래서 매우 직관적으로 이해할 수 있다.

## 📌 HTTP Method와 CRUD
일반적으로 API를 설계할때, URL로는 자원(resource)을 명시하고, HTTP Method로는 행위를 명시합니다.   

>REST 구성
- 자원(resource): URI
- 행위(verb): HTTP Method

>HTTP Method를 통해 해당 자원에 대한 CRUD Operation을 적용하여 아래와 같이 사용한다.   
- Create: 데이터 생성 (POST)
- Read: 데이터 조회 (GET)
- Update: 데이터 수정 (PUT)
- Delete: 데이터 삭제 (DELETE)

```
API 설계시 멱등성을 고려
- 멱등성: 동일한 요청을 한 번 보내는 것과 여러 번 연속으로 보내는 것이 같은 효과를 지니고, 서버의 상태도 동일하게 남을 때 해당 HTTP 메서드가 멱등성을 가졌다고 말한다.
- 올바르게 구현하는 경우, GET, HEAD, PUT, DELETE 메서드는 멱등성을 가지고, POST 메서드는 멱등성을 가지지 않는다.
- 참고: https://developer.mozilla.org/ko/docs/Glossary/Idempotent
```

## 1. GET Method
get은 보통 조회를 할 때 사용한다.
- DB로 생각했을때는 `SELECT`에 해당
   
예를들어, 회원가입한 사용자의 정보를 알고 싶다면, 아래처럼 사용한다.   
```http
GET http://localhost:8080/rest/api/v1/user/1
```

## 2. POST Method
post는 보통 데이터를 추가할 때 사용한다.
- DB로 생각했을때는 `INSERT`에 해당

회원 가입을 하는 경우, POST 방식으로 사용자의 정보를 함께 전송한다.
```http
POST http://localhost:8080/rest/api/v1/user
{
  "username": "아무개",
  "password": "1234",
  "email": "test@google.com",
  }
```
보통 생성 과정이 성공적으로 끝나면, 응답값으로 201 CREATED를 보낸다. (아래 글 참고, 출처: mdn)   

HTTP 201 Created는 요청이 성공적으로 처리되었으며, 자원이 생성되었음을 나타내는 성공 상태 응답 코드입니다. 해당 HTTP 요청에 대해 회신되기 이전에 정상적으로 생성된 자원은 회신 메시지의 본문(body)에 동봉되고, 구체적으로는 요청 메시지의 URL이나, Location (en-US) 헤더의 내용에 위치하게 됩니다.

이 상태코드(status code)는 일반적으로 POST 요청(request)에 대한 응답결과(result)로써 사용합니다.   
>출처: https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/201

## 3. PUT Method
PUT은 데이터를 수정 할 때 사용한다.
- DB로 생각했을때는 `UPDATE`에 해당
 
사용자의 정보를 수정하고 싶은 경우, 수정하고 싶은 사용자 정보와 함께 PUT 방식으로 요청한다.
- 위 POST와 동일한 URL로 요청하지만, HTTP 메소드가 다르기 때문에 다르게 동작한다.

```http
PUT http://localhost:8080/rest/api/v1/user/{user_id}

예시: 
PUT http://localhost:8080/rest/api/v1/user/1

{
    "password": "4321"
 }
```

## 4. DELETE Method
DELETE는 데이터를 삭제할 때 사용한다.
- DB로 생각했을때는 `DELETE`에 해당
 
사용자의 정보를 지우고 싶은 경우(탈퇴 처리), DELETE 방식으로 사용자의 ID의 값과 함께 요청한다.
```http
DELETE http://localhost:8080/rest/api/v1/user/{user_id}

예시: 
DELETE http://localhost:8080/rest/api/v1/user/1
```

## 📌 응답코드
- 200 : 클라이언트 요청 정상수행 (응답에 대한 메시지가 포함)
- 201 : 리소스 생성 요청에 대한 정상처리
- 202 : 리소스 생성 요청이 비동기적으로 처리될 때 사용
- 204 : 클라이언트 요청 정상수행 (응답에 대한 메시지 미포함, 보통 삭제요청에 사용)
- 400 : 클라이언트 요청이 부적절할 때 사용 (부적절한 이유를 응답 Body에 넣어줘야 함)
- 401 : 클라이언트가 인증되지 않은 상태에서 보호된 리소스를 요청할 때 사용
- 403 : 클라이언트가 인증상태와 무관하게 응답하고 싶지 않은 리소스를 요청할 때 사용 (400 사용을 권장)
- 404 : 클라이언트가 요청한 리소스가 존재하지 않을 때 사용
- 405 : 클라이언트가 불가능한 메소드를 사용했을 때

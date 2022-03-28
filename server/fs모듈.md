# 📌 fs module
node.js가 내장하고 있는 여러 모듈 중 하나이다. fs는 File system의 약자로서, fs모듈은 파일을 읽고, 저장하는등 파일과 관련된 모듈들을 내장하고 있다.

### fs.readFile
fs.readFile() 은 로컬에 존재하는 파일을 읽어오는 메소드다. fs.readFile 은 비동기적으로 파일 내용 전체를 읽으며 세가지의 인자를 넘길 수 있다.   
[fs.readFile 공식문서](https://nodejs.org/dist/latest-v12.x/docs/api/fs.html#fs_fs_readfile_path_options_callback) 참조   

**형태**
```javascript
fs.readFile(path[, options], callback)
```

### 1. path
첫번째 인자에 오는 `path`는 불러올 파일의 위치(경로)이고, 밑에 네가지 타입이 올 수 있다.
```
<string> || <Buffer> || <URL> || <integer> 
```

---
### 2. options
두번째 인자는 가지고 오는 데이터를 어떻게 인코딩을 정해주는 인자이다. 생략이 가능한 인자이지만, 온다면 밑에 두 타입이 올 수 있는데 만약 스트링 타입으로 오게 된다면
인코딩을 넘기게 되는데 주로 utf8을 적어준다.
```
<Object> | <string>
```

---
### 3. callback()
세번째 인자는 콜백함수로써, 이 콜백함수는 err와 data를 인자로 받는다.
```
err  <Error>
data <string> | <Buffer>
```

---
### 예시
```javascript
const fs = require("fs"); // 모듈 불러오기
fs.readFile('/etc/passwd','utf8', (err, data) => {
  if (err) throw err;
  console.log(data);
});
```

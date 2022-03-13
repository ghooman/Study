## 📌continue문
어떠한 행위를 하다가 continue문을 만나면 해야할 명령문을 실행하지 않고 그 다음 명령문을 실행하는 명령문 이다.   

**예제)**
```javascript
let text = '';

for (let i = 0; i < 10; i++) {
  if (i === 3) {
    continue;
  }
  text = text + i;
}

console.log(text);
// expected output: "012456789"
```

***
## 📌break문
break문은 for,while문 등에서 break문을 만나면 바로 빠져나가는 명령문 이다.

**예제)**
```javascript
let i = 0;

while (i < 6) {
  if (i === 3) {
    break;
  }
  i = i + 1;
}

console.log(i);
// expected output: 3
```

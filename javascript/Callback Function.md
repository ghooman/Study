# Callback Function

## 📌 콜백함수(Callback Function)란?
`파라미터로 함수를 전달하는 함수`
콜백함수(Callback Function)란 파라미터로 함수를 전달받아, 함수의 내부에서 실행하는 함수이다.

```javascript
let number = [1, 2, 3, 4, 5]
number.forEach(el => console.log(el * 2));

/*
<output>
2
4
6
8
10
*/
```
  
콜백함수는 이미 우리의 코드 속에서 자주 사용되고 있다.
예를 들어, `forEach`함수의 경우 함수 안에 익명의 함수를 넣어서 `forEach`문을 동작시킨다.
***

## 📌 콜백 함수(Callback Function)사용 원칙
__✔️ 익명의 함수 사용__

```javascript
let number = [1, 2, 3, 4, 5];

number.forEach(function(x) {
  console.log(x * 2);
});
```

위의 예제를 화살표 함수에서 일반 함수로 바꾼 예제이다.   
콜백함수는 이름이 없는 '익명의 함수'를 사용한다. 함수의 내부에서 실행되기 때문에 이름을 붙이지 않아도 된다.

__✔️ 함수의 이름(만) 넘기기__

```javascript
function whatYourName(name, callback) {
  console.log('name: ', name);
  callback();
}

function finishFunc() {
  console.log('finish function');
}

whatYourName('jihoo', finishFunc);

/*
<output>
name: jihoo
finish function
*/
```

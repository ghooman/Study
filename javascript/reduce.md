## 📌 reduce
reduce()는 배열 각 요소에 대하여 reducer 함수를 실행하고, map과 filter와 달리 배열이 아닌 하나의 결괏값을 반환한다는 차이점이 있다.

---
__문법)__
>
```javascript
const numbers = [1, 2, 3, 4];
const numbersSum = numbers.reduce((acc, cur) => {
  console.log(acc, cur); ///acc = accumulator, cur = currentValue
  return acc + cur;
});
>
console.log(numbersSum);
>
  //1 2
  //3 3
  //6 4
  //10
```

reduce 함수에서 값을 계속 누적하여 갖고 있는 <span style="color:#0eb93c">__누산기__</span>인 acc와 현재 요소인 cur를 매개변수로 하여 모든 요소의 합을 반환하는 로직이다.
<span style="color:#f4c216">console.log(acc, cur)</span>의 결괏값을 차례로 살펴보면 어떻게 계산이 누적되고 있는지 알 수 있다.
<span style="color:#0eb93c">__누산기__</span>라는 개념이 생소할 수 있는데 간단하게 표현하자면 `reduce 함수를 수행하면서 생기는 값을 임시적으로 보관하는 형태`이다.

또한 reduce에는 초기값이라는 생소한 값을 입력할 수 있다. 아래 예시의 함수의 끝에 10이라는 숫자가 추가된 걸 볼 수 있는데, 이처럼 초기값은 숫자부터 배열까지 다양한 값을 입력할 수 있다.

초기값을 입력하게 되면 배열의 첫 번째 요소부터가 아니라 초기값부터 계산이 시작된다.
>
```javascript
const numbers = [1, 2, 3, 4];
const numbersSum = numbers.reduce((acc, cur) => {
  console.log(acc, cur); ///acc = accumulator, cur = currentValue
  return acc + cur;
}, 10);
>
console.log(numbersSum);
>
  //10 1
  //11 2
  //13 3
  //16 4
  //20
  ```

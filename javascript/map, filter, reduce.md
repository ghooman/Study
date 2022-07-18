## 📌 map()
map()은 주어진 배열의 요소를 순회하면서 콜백함수를 실행하며 새로운 배열을 리턴해주는 함수이다.   
map()은 3개의 인자를 받을 수 있고, value를 제외한 두 인자값은 필요에 따라 생략 가능하다.
```javascript
const arr = [1,2,3,4,5];
const newArr = arr.map((value, index, array) => {
  value *= 2;
  console.log(value, index, array);
});
```
value = 배열의 현재 요소의 값 (1,2,3,4,5)   
index = 배열 번호 (0,1,2,3,4)   
array = map을 호출한 원본배열 [1,2,3,4,5]   

따라서 출력결과는   
2, 0, [1,2,3,4,5]   
4, 1, [1,2,3,4,5]    
6, 2, [1,2,3,4,5] ... 식으로 마지막 배열까지 출력된다.   

```javascript
const arr = [1,2,3,4,5];
const newArr = arr.map((value, index, array) => {
  return value *= 2;
});

console.log(newArr)  // [2, 4, 6, 8, 10]
```
***
## 📌 filter()
map과 비슷하게 배열을 순회하며 콜백함수를 수행해 새로운 배열을 리턴하나, map과 달리 조건문을 통해 배열들을 리턴한다.   

또한 반환값이 숫자, 문자열, 배열 등으로 다양한 map과 달리 filter는 boolean 타입만 리턴한다. 따라서 반환값이 true인 경우만 배열에 추가된다.   

filter 또한 세개의 인자값을 가지며, value를 제외한 두가지 인자값은 생략가능하다.
```javascript
const arr = [1,2,3,4,5];
const newArr = arr.filter((value, index, array) => {
  console.log(value, index, array);
  return value % 2 == 0;		//짝수인 요소만 newArr에 넣기
});

console.log(newArr);
```
출력해보면   
1, 0, [1,2,3,4,5]   
2, 1, [1,2,3,4,5]   
3, 2, [1,2,3,4,5] ...   

newArr은 [2,4] 가 들어간걸 확인해볼 수 있다.
***
## 📌 reduce()
reduce는 배열의 각 요소를 순회하며 콜백함수를 실행하여 결과값을 하나 반환한다.   

reduce는 4개의 인자값을 가진다.   
두개는 필수이며, 나머지 두개는 생략 가능하다.   
accumulator = 현재까지 요소가 반환한 값을 누적   
currentValue = 순환하는 요소중 현재 요소의 값   
index = 배열의 현재 인덱스   
array = reduce를 호출한 배열   
```javascript
const arr = [1,2,3,4,5];

const sum = arr.reduce((acc, val) => acc + val);

console.log(sum);
```
arr의 모든 요소의 합을 구하는 코드   
출력하면 15를 확인할 수 있다.   

여기서 초기값을 설정할수도 있는데,
```javacsript
const arr = [1,2,3,4,5];

const sum = arr.reduce((acc, val) => acc + val, 10);

console.log(sum);
```
콜백함수 뒤에 initialValue라는 옵션값을 설정해주면 초기값을 정할 수 있다.   
예시에선 10으로 설정했으므로 10에서 1,2,3,4,5를 더해가는 식으로 25를 출력할 수 있다.   

필수가 아닌 값이지만, 만약 이런 원시값이 아닌 객체를 넣었을 경우 initialValue를 설정해주어야 제대로 된 값이 나온다.
```javascript
let list = [
  {name : "mori", age : 20},
  {name : "kain", age : 18},
  {name : "gardia", age : 30},
  {name : "sandy", age : 10}
];

let answer = list.reduce((acc, obj) => {
	if(obj.age < 20) {
    acc.push(obj.name);
	}
}, []);

console.log(answer);
```
만약 여기서 initialValue인 []를 설정해주지 않는다면 오류가 생긴다.

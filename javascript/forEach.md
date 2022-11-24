# 📌 forEach
forEach() 메서드는 배열에 활용이 가능한 메서드로, 파라미터로 주어진 함수를 배열 요소 각각에 대해 실행하는 메서드이다.
map() 메서드와 거의 비슷하지만 차이점은 따로 return 하는 값이 없다는 점이다.
***

__문법)__
>
```javascript
const myArr = [1, 2, 3];
>
const newMyArr = myArr.forEach((currentElement, index, array) => {
  console.log(`요소: ${currentElement}`);
  console.log(`index: ${index}`);
  console.log(array);
});
>
  //요소: 1, index: 0, (3) [1, 2, 3]
  //요소: 2, index: 1, (3) [1, 2, 3]
  //요소: 3, index: 2, (3) [1, 2, 3]
>  
> console.log(newMyArr); //undefined
```

forEach 메서드도 map메서드와 동일하게 파라미터로 콜백 함수를 받는데, 그 콜백 함수의 파라미터는 요소, index 그리고 현재 map메서드를 호출한 배열이다.

forEach 메서드도 세번째 배열은 잘 사용되지 않고 일반적으로 첫 번째 요소와, 두 번째 index가 많이 사용된다.

앞에서도 언급했지만, map 메서드와 차이점은 따로 콜백 함수가 return 하는 값을 따로 모아서 어떤 처리를 하는 과정이 없기 때문에, 메서드를 호출한 코드를 함수에 할당하면 undefined가 할당된다. 

그래서 forEach 메서드는 변수에 할당하기 보다는 반복문이나 조건문과 같이 그냥 바로 호출되는 것이 일반적이다.

>
```javascript
const myArr = ['강아지', '고양이', '햄스터', '거북이', '이구아나'];
>
myArr.forEach((el, i) => {
  console.log(i);
  console.log(el);
  if(el === '고양이') {
    myArr.shift();
  }
})
>
console.log(myArr); // ['고양이', '햄스터', '거북이', '이구아나']
```

그리고 forEach 메서드의 콜백함수 내에서 메서드를 호출한 배열을 변경하는 것이 가능한데,
위 코드처럼 특정상황에서 요소 하나를 삭제해버리게 되면 그다음 요소를 찾을 때, 변경된 배열에서 해당하는 index를 찾기 때문에 이 코드의 실행결과를 보면 고양이 다음에 거북이가 출력되는데, 메서드가 실행된 이후의 myArr를 살펴보면, 강아지가 배열에서 삭제된 걸 확인할 수 있다.
***
__참고)__
forEach의 상위호환이라고 해서 배열의 요소들을 순회할 때 그냥 무조건 map 메서드를 활용하는 경우를 본 적이 있었는데,
개인적으로는 return 값으로 새로운 배열이 필요하지 않는 경우라면 forEach 메서드를 활용하는 것이 옳다고 생각한다.

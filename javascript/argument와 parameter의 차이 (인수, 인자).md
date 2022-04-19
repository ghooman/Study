## 📌 argument
```javascript
plusNumber(1, 2);

// 전달인자 1, 2
```

함수를 호출할 때 값을 전달한다고 해서 `전달인자`라고 부른다.   
매개변수와 달리 전달인자는 고정되어 있지 않고, 호출할 때마다 수시로 변하는 값(Value)이기 때문에 변수가 아닌 값(Value)으로 정의한다.

## 📌 parameter
```javascript
function plusNumber(a, b) {
  return a + b;
}

// 매개변수 a, b
```
함수 내부에 있는 인자로써, 특정한 값으로 정해져 있는 것이 아니라, 함수가 호출하면서 건네준 argument의 값이 변수 ( Variable )에 담기게 된다.   
들어오는 인자가 매개체 역할을 하기 때문에 `매개변수`라고 하며 영문으로 `parameter` 라고 한다.

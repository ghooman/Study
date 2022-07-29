## 📌 Number(str)
Number 메서드는 문자열을 인자로 받으면 해당 문자열을 숫자로 바꿔준다.
```javascript
var num = Number('1234'); // 1234
```

아래처럼 문자열이 숫자가 아닌 경우 num에는 NaN이 저장된다.
```javascript 
let num = Number('1000원'); // NaN
```

소수점이 있는 경우에는 모두 숫자형으로 바뀌게 된다.
```javascript
let num = Number('10.123'); // 10.123
```
***
## 📌 parseInt(str)
기본적으로 Number(str)와 동일하게 문자열을 인자로 받으면 해당 문자열을 숫자로 바꿔준다.   
아래의 코드는 '1234'라는 문자열을 1234라는 숫자로 형 변환하여 변수 num에 담는 코드이다.
```javascript
let num = parseInt('1234'); // 1234
```

문자열이 숫자가 아닌 경우가 Number()와 조금 다른데, 문자열이 숫자로 시작하는 경우에는 숫자가 끝날 때까지만 형 변환을 하여 num에 저장된다.   
시작이 숫자가 아니면 Number()와 마찬가지로 num이 NaN이 저장된다.
```javascript 
let num = parseInt('1000원'); // num에 1000이 저장
let num = parseInt('가격 : 1000원'); // num에 NaN이 저장
```

소수점이 포함된 경우엔, 10.123에서 정수만 뽑아서 표시가 되며, 숫자형으로 바뀌게 된다.
```javscript
let num = parseInt('10.123'); // 10
```
</br>
</br>
즉, parseInt와 Number는 비슷하면서도 다른 부분이 있다. 둘 모두 숫자형으로 타입을 바꿔주지만, 문자열이 숫자로 시작하는 경우와 소수점을 표시하는 부분에 대해서는 차이점이 있으니, 이 차이를 알고 잘 활용한다면 좋을듯싶다.

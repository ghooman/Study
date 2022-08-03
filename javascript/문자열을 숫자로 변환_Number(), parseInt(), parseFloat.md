## 📌 Number()
- 문자열의 수를 숫자로 바꿔준다.
- 만약 인수를 형변환 할 수 없다면 NaN을 리턴한다.   
```javascript
const str = '1234';

Number(str);  // 1234
Number('1234.5');  // 1234.5
Number(undefined);  // NaN
Number('abcd');  // NaN
Number('1000won')  // NaN
Number(null)  // 0
Number('')  // 0
```
***
## 📌 parseInt()
- 문자열 인자(숫자 + 문자)를 받는다.
- 그 인자를 parse(해부하다, 품사문법적 관계를 설명하다)한다.
- integer(정수) 또는 NaN을 리턴한다.
```javascript
const str = '1234';

parseInt(str);  // 1234
parseInt('1234.5');  // 1234
parseInt(undefined);  // NaN
parseInt('abcd');  // NaN
parseInt('1000won')  // 1000
parseInt(null)  // NaN
```
***
## 📌 parseFloat
- 문자열 인자(숫자 + 문자)를 받는다.
- 그 인자를 parse(해부하다, 품사문법적 관계를 설명하다)한다.
- 부동 소수점 숫자(float point number)를 반환한다.
```javascript
const str = '1234';

const num1 = parseFloat(str);  // 1234
const num2 = parseFloat('1234.5');  // 1234.5
const num3 = parseFloat(undefined);  // NaN
const num4 = parseFloat('abcd');  // NaN
parseInt('1000won')  // 1000
parseInt(null)  // NaN
```

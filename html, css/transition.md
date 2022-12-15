# 📌 Transition
transition은 css 프로퍼티의 값이 변화할 때, 일정 시간에 걸쳐 일어나도록 한다.
```scss
<style>
  div {
	width: 100px;
  	heigth: 100px;
  	background: orange;
  	transition : all 2s;
  }
  div:hover {
  	border-radius : 50%;
  	background : green;
  }
</style>
```
기본 상태인 오렌지색 사각형이 있다가 마우스를 올리면(hover시) 2초에 걸쳐 초록색 원으로 변한다.
***
| 프로퍼티 |	설명 |	기본값 |
|-|-|-|
| transition-property |	트랜지션의 대상이 되는 CSS 프로퍼티를 지정한다	| all |
| transition-duration | 0s(duration)을 초 단위(s) 또는 밀리 초 단위(ms)로 지정한다 | 0s |
| transition-timing-function | 트랜지션 효과를 위한 수치 함수를 지정한다. | ease |
| transition-delay | 프로퍼티가 변화한 시점과 트랜지션이 실제로 시작하는 사이에 대기하는 시간을 초 단위(s) 또는 밀리 초 단위(ms)로 지정한다 | 0s |
| transition | 모든 트랜지션 프로퍼티를 한번에 지정한다(shorthand syntax)	|

## transition-property
트랜지션의 대상이 되는 css 프로퍼티명을 지정한다. 지정하지 않는 경우 모든 프로퍼티가 트랜지션의 대상이 된다. 복수의 프로퍼티를 지정하는 경우 쉼표로 구분한다.
```scss
<style>
  div {
      width: 100px;
      height: 50px;
      background-color: orange;
      transition-property: width;
      transition-duration: 2s;
  }

  div:hover {
      width: 300px;
      background-color: green;
  }
</style>
```
transition-property에 width값을 넣어서 width에만 transition이 적용된다. 2초에 걸쳐 width가 늘어나지만 색은 바로 파란색이 된다.
## tranfition-duration
트랜지션이 일어나는 지속시간을 초 단위로 지정한다. 값을 지정하지 않을 시 기본값(0s)가 적용되어 트랜지션 효과를 볼 수 없다.
```scss
<style>
  div {
    width: 100px;
    height: 50px;
    padding: 10px;
    color: white;
    background-color: red;
    margin-bottom: 10px;
    transition-property: width, opacity;
  }
  div:nth-child(1) {
    transition-duration: 0.5s;
  }
  div:nth-child(2) {
    transition-duration: 2s, 1s;
  }
  div:nth-child(3) {
    transition-duration: 5s, 2.5s;
  }
  div:hover {
    width: 300px;
    opacity: .1;
  }
</style>
```
3개의 사각형이 있고 duration을 다 다르게 한 설정이다. 앞 예제와 달리 transition-property도 복수로 지정해서 duration 값도 복수로 지정했다. 첫번째 자식요소의 경우 width가 0.5s, opacity가 0s만에 변한다.

## transition-timing-function
트랜지션 효과의 변화 흐름, 시간에 따른 변화 속도와 같은 일종의 변화의 리듬을 지정한다.   
ease, linear, ease-in, ease-out, ease-in-out   
다섯가지 값이 존재하고 각 키워드에 맞는 속도, 가속, 감속의 형태가 적용된다.

## transition-delay
프로퍼티가 변화하는 시점과 트랜지션이 실제로 시작하는 사이에 대기하는 시간을 지정한다. 트랜지션이 지정한 시간 후에 실행되는 것이다.

## transition
모든 트랜지션 프로퍼티를 한버에 지정할 수 있는 축약어이다.
```
transition: property duration function delay // 기본값 all 0 ease 0
```

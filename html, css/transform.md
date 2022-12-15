# 📌 Transform
요소를 회전하거나 확대/축소 또는 기울기를 조절하는 속성이다.
## ✔️ 사용 방법
### 2D 변형
**1) transform: rotate(angle);**   

  - 요소를 회전시키는 속성
  - deg, rad, grad, turn 등의 단위를 사용한다.
  - turn은 1회전을 의미하며, 360deg(360도)와 같은 효과를 낸다.
  - 값이 양수면 시계 방향, 음수면 반시계 방향이다.
  - rotate X, rotate Y에 값을 넣으면 선택한 축에 따라 회전한다.
    
**2) transform: translate();**

  - 요소를 이동시키는 속성
  - px, %등 css 크기 단위를 사용한다.
  - 값이 양수일 경우 오른쪽(x축)과 아래쪽(y축)으로 이동한다.
  - 값이 음수일 경우 왼쪽(x축)과 위쪽(y축)으로 이동한다.
  - X와 Y의 값(X, Y)을 같이 넣으면 x축과 y축으로 이동한다.

**3) transform: scale();**
	
  - 요소를 확대하거나 축소시키는 속성
  - 1보다 큰 수는 확대, 1보다 작으면 축소시킨다.
  - scaleX, scaleY에 값을 넣으면 선택한 방향에 따라 확대/축소시킨다.
    
**4) transform: skew();**
	
  - 요소를 기울이는 속성
  - skew X, skew Y에 값을 넣으면 선택한 축에 따라 요소를 기울인다.
    
**5) transform: scale() translate() rotate() skew();**
	
  - 공백(스페이스)으로 구분지어 여러 속성들을 함께 사용할 수 있다.
    
**6) transform: matrix(n, n, n, n, n, n);**
	
  - 모든 2D transform 메소드를 한 번에 설정
    
**7) transform-origin: % or keyword;**
	
  - 요소에 transform을 적용하는 변환 중심을 설정
  - 백분율을 지정하거나 대응 가능한 키워드를 사용하여 값을 설정
    (0% = left or top, 50% = center, 100% = right or bottom)

### 3D 변형

**1) transform-origin: % or keyword;**

  - 변환을 적용하는 변환 중심 설정
  - 백분율을 지정하거나 대응 가능한 키워드를 사용하여 값을 설정
      (0% = left or top, 50% = center, 100% = right or bottom)

**2) transform-style: flat or preserve-3d**

  - 변환이 자식(child) 요소들에게도 적용될지 설정
  - 기본값은 flat으로 자식 요소의 3D 변환을 사용하지 않음
  - preserve-3d; 자식 요소의 3D 변환 사용
    
**3) transform: perspective;**

  - 원근감을 표현할 때 사용할 픽셀 수 설정
    
**4) perspective-origin: % or keyword;**

  - 원근감 표현할 때 사용할 기준 축 설정
  - 백분율을 지정하거나 대응 가능한 키워드를 사용하여 값을 설정 
      (0% = left or top, 50% = center, 100% = right or bottom)
    
**5) backface-visivility: visible or hidden**

  - 요소의 앞면만을 표현(뒷면 표시 안함) 여부를 설정
  - hidden을 설정하면 뒷면 표시를 하지 않는다.
    
**6) transform: rotate3d(x, y, z angle);**

  - 주어진 각도만큼 x, y, z축 기준으로 회전
    
**7) transform: translate3d(x, y, z);**

  - 현재 위치에서 주어진 x, y, z축의 거리만큼 이동
    
**8) transform: scale3d(x, y, z);**

  - 주어진 배율만큼 x, y, z축 방향으로 늘리거나 줄임
    
**9) transform: perspective(n);**

  - 3D 요소에 원근감을 표현할 때 사용할 픽셀 수 결정
    
**10) transform: matrix3d(n x 16);**

  - 4 x 4 행렬을 이용한 16개 매개변수로 모든 3D 변형 메소드를 한 번에 설정
    
`perspective 속성과 함수의 차이점`
- perspective 속성
  - 적용 대상: 관찰 대상의 부모 요소
  - 관찰 대상이 여럿이면 부모 요소에 속성 사용.
    (관찰 대상이란 원근법을 의미함)
  - 원근법의 기준점을 설정: perspective-origin
   
- perspective() 함수
  - 관찰 대상 자체가 적용 대상
  - 관찰 대상이 하나면 관찰 대상 자체에 함수 사용
  - 관찰하는 기준점 설정 시 transform-origin 사용
        
💡perspective 속성은 관찰 대상이 여럿이기 때문에 부모/조상 요소에 적용하여 하위 요소들을 관찰하는 원근거리를 설정   
💡transform: perspective() 변환 함수는 관찰 대상에 직접 적용하여 그 대상을 관찰하는 원근 거리를 설정

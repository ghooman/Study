아무런 설정도 하지 않은 HTML 파일에서 기본적으로 사방에 여백이 생긴다.   
이게 거슬려서 없애는 방법을 찾아보았다.   
```html
<head>
<style type="text/css">
body {
    margin: 0;
    padding: 0;
}
</style>
</head>
```
CSS를 사용해서 body에 있는 여백을 없애준다.   
여백은 margin, padding 두 가지 종류가 있으므로 둘 다 0으로 리셋해준다.   
head안의 style 부분에 적어주거나, 사용하는 CSS파일에 적어준다.

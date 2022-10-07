구글 개발자 사이트에서 가져오기.   
https://developers.google.com/speed/libraries

```html
<head>
 <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.1/jquery.min.js"></script>
    <script type="text/javascript">
      $(document).ready(function () {
        $("#headers").load("./header.html");
      });
    </script>
 <head>
 
  <body>
    <!-- import header -->
    <div id="headers"></div>
  </body>
 ```
 헤드 부분에 jQuery를 가져와서 import하는 문법 예시.

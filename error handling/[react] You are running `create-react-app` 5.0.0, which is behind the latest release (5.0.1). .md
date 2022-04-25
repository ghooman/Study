## 실행코드
리액트를 셋팅하는 기본코드를 입력하자 처음보는 에러가 발생되었다.
>npx create-react-app vanilla-redux

## 에러발생
>You are running `create-react-app` 5.0.0, which is behind the latest release (5.0.1).
>We no longer support global installation of Create React App.
>Please remove any global installs with one of the following commands:
>- npm uninstall -g create-react-app
>- yarn global remove create-react-app

## 해결방법
>1. npm uninstall -g create-react-app
>2. yarn global remove create-react-app
>3. npm add create-react-app
>4. npx create-react-app myapp

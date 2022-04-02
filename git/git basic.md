## 📌 1. 초기 설정
`git config --global user.name "John Doe"`   
`git config --global user.email johndoe@example.com`

## 📌 2. 로컬저장소와 깃 생성
디렉토리를 만들거나(make directory = mkdir), 깃을 만들 디렉토리로 이동(change directory = cd)한다.

**1) 로컬저장소 생성/ 이동**   
`mkdir (폴더 경로)`   
`ex) mkdir /Users/a./instagram`   
경로이름을 복사해서 적당히 붙여넣었다.

`cd (폴더 경로)`   
`ex) cd /Users/a./instagram`   
또는 vscode에서 해당 폴더를 열고 새 터미널[⌃⇧`]을 연다.

**2) 깃 생성**   
`git init`   
이 명령은 .git 이라는 하위 디렉토리를 만든다. .git 디렉토리에는 저장소에 필요한 뼈대 파일(Skeleton)이 들어 있다. 이 명령만으로는 아직 프로젝트의 어떤 파일도 관리하지 않는다.

## 📌 3. 업로드 할 파일 준비
**1) 파일 상태확인**   
`git status`   
수정된 파일이 있는지, 작업 내역 없이 깨끗한 디렉토리인지 등.. 파일의 상태를 볼 수 있는 명령어다.

**2) Staging Area에 파일 올리기**   
`git add (올릴 파일)`

```
git add 뒤에 스테이지에 올릴 파일 이름을 적는다.   

git add: 가장 기초적, rm 명령으로 제거된 파일은 add되지않음   

git add --all   
git add .   
: status에 나온 변경사항을 모두 스테이지에 올려준다.   

git add -u :  하나 이전의 스테이지와 비교해서 변경된 부분만 add. 새롭게 만들어진 파일은 add 하지않음.   
git add -A : 새로만든 것, 수정, 삭제 등 모든 변경된 파일을 add 해준다.
```

**3) 커밋하기**   
`git commit -m "메세지"`   

**4) commit history 확인**
`git log`

## 📌4. Github에 push하기

**1) 원격저장소 추가**   
`git remote add (단축이름) (url)`   
`ex) git remote add origin https://github.com/idid/instagram-clone.git`   

단축이름은 origin 말고 다른 이름도 가능하다.   
이렇게 추가 되었으면 이제 파일을 집어넣을 일만 남았다.   

**2) 원격저장소 제거**   
`git remote remove (기존 저장소 별명)`   
`ex) git remote remove origin`   
기존의 원격저장소를 삭제하고 싶다면 위 명령을 써보라. 참고로 origin은 자동으로 등록되는 원격저장소 이름이다.   

**3) 원격저장소 확인**   
`git remote -v`   
혹시 이전에 원격저장소를 연결한 경우가 있다면, 원격저장소가 있는지 이 명령어로 확인한다.   
-v는 좀더 상세하게 알아보고 싶을 때 덧붙인다.

**4) 원격저장소에 push 하기**   
`git push (원격저장소 이름) (브랜치 이름)`   
`git push origin master`

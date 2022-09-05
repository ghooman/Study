## 오류 발생
새로운 레포지토리에 push하는 과정에서 master 브랜치가 자동으로 생성되었고 master 브랜치에 push를 한 상황이었다. 하지만 main 브랜치가 기본 브랜치로 잡혀있어서 master 브랜치의 내용을 main 브랜치로 넘기려는 과정에서 오류가 발생하였다.

## 해결 방법
main 브랜치가 비어있었기 때문에 master 브랜치의 내용을 pull & request 과정에서 오류가 발생하였다.   
```
git checkout master

git branch main master -f

git checkout main

git push origin main -f
```
해당 순서로 명령어를 입력하게 되면   
master 브랜치의 내용이 main 브랜치에 덮히게 된다.

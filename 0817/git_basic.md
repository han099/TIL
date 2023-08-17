# 오전 실습 

- 로컬저장소에서 파일생성
- README.md 생성
- 개인 프로필 코드 작성
- github에서 new repository 생성(username으로!) 
- 로컬저장소 작업물을 commit 후 push

    *github profile readme 검색시 많은 레퍼런스 활용가능*
--- 
# 실습 관련 git 명령어 정리 (복습)
## 프로젝트 시작할 때 
### 로컬에서 처음 시작하기
```
git init
```
* git init하면 (main)으로 확인할 수 있음
### 원격에서 처음 시작하기
```
git clone https:// ~
```

## 버전 기록할 때
```
git add .
git commit -m '커밋메시지'
```
* git status로 파일 상태 확인 해보기 
* git log로 커밋 확인하기

## 원격저장소 최초 설정할 때
```
git remote add origin url
```

## 원격저장소에 업데이트
```
git push origin main
```
---

*gitignore*
```
버전관리와 상관없는파일들은 .gitignore 파일을 생성하고 해당내용을 관리한다.

이미 커밋된 파일은 반드시 삭제해야 .gitignore로 적용

-> 프로젝트 시작전에 미리 설정해야 좋음
```
---
### github 관련사이트
- https://desktop.github.com/
- https://education.github.com/pack/join
- https://git-scm.com/book/ko/v2
- https://backlog.com/git-tutorial/kr/


---

# Branch

*독립적인 작업흐름* 
- 각 브랜치마다 버전이 쌓이게 되고(개발)
- 이 버전을 반영하려면 merge를 하게 된다.
- merge상황은 그냥 조모임일 뿐


## Branch 주요 명령어

```bash
git branch #현재 브랜치
git branch 브랜치 이름 #브랜치 생성
git checkout 브랜치 이름 #브랜치 이동
git branch -d 브랜치 이름 #브랜치 삭제
```
```bash
git merge 브랜치 이름 # 브랜치 통합
# merge : 브랜치를 합치는 명령어
git log --oneline --gragh # 브랜치 상황확인
# '--gragh'를 통해 직관적 확인 가능
```

## GitHub으로 협업을 한다는 것은..(브랜치 작업 흐름)


```bash
# (1) 작업하기 전에 브랜치를 만든다.

git branch 브랜치이름
git Checkout 브랜치이름

# (2) 열심히 코딩한다.

# (3) 버전을 기록한다. = 커밋
git add .
git commit -m ""

# (4) 작업이 끝나면, 작업한 브랜치를 push한다.

git push origin 브랜치이름

# (5) github에서 pull Request를 생성, 요청한다.

# (6) 코드 리뷰 등,, 협업 룰에 따라서 진행하고 다 완료되면 github에서 merge가 된다.

```
\

# Fork & PullRequest

- 협업관계가 아닐 경우 사용하는 fork
1) 작업하고 싶은 저장소를 fork해서 자신의 로컬저장소로 clone 해온다.
2) 작업 후 commit한다.
    - 이때 자신의 url이 맞는지 확인!
    ```
    git remote -v
    ```
3) 자신의 저장소에 push를 한다.

4) 원래의 원격저장소(github)에 가서 PullRequest를 요청한다.

5) 원본 저장소의 사용자가 승인할 경우 merge된다.

---
## 기타 명령어
```bash
git restore --staged <file> #git add 취소하기
git commit --amend # 커밋 메시지 변경하기
git push origin <브랜치이름> --force #이미 원격 저장소에 푸시했을 경우 
git reset HEAD~1 # 커밋 취소하기
git reset HEAD^ # 가장 최근 커밋 취소하기
git reset HEAD~1 --hard # 커밋 취소하기(워킹디렉토리에서도 제거)
git revert HEAD # 히스토리가 수정되지 않고 새로운 커밋으로 저장
```
---
#### 커밋메시지 편하게 작성하기 위한 설치코드(?)
```bash
git config --global core.editor "code --wait"
```



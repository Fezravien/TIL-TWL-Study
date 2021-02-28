# Git



## VCS(Version Control System)



### 구체적 이점

- 변경 이력을 기록을 통해서 변경된 내용 공유 가능
- 타인이 작업한 내용을 쉽게 병합
- 과거 상태로 쉽게 복구 가능
- 여러 분기(Branch)를 통해 병렬 관리 가능



- 복잡한 Branch 관리에 적합
- 심플하지만 핵심적인 기능이 강력
- 로컬 저장소와 원격저장소의 분리
- 빠른 속도
- 다양한 서비스 업체
- 다양한 보조 툴



### Git 다루기

- $ git init (초기화)

- $ git status (상태)

- $ git add README.md (추적)

- $ git config --global user.name (환경설정)

  $ git config --global user.email

- $ git commit -m "" (a.txt, b.txt 각각 가능)

- $ git log

  ---

  

  <img src="/Users/yjaewoongnaver.com/Library/Application Support/typora-user-images/스크린샷 2021-02-23 오전 10.22.35.png" alt="스크린샷 2021-02-23 오전 10.22.35" style="zoom: 33%;" />

  

### Working Directory (작업 공간)

실제 작업하고 있는 공간



---

### Stage Area (준비 공간 - add)

- Git이 변경이력을 관리하는 부분
- Working Directory에서 git 명령어를 통해서 추가 가능
- 이 곳에 올라와 있는 파일만 저장소에 추가 및 수정 가능
- 일종의 준비구역



----

 ### Repository

변경이력이 저장되는 공간 (log에 기록이 남음)



#### Local Repository

- 외부에 위치하지 않고 작업하고 있는 컴퓨터에 존재
- 인터넷을 이용하지 않기 때문에 매우 빠른 속도
- 인터넷이 연결되지 않아도 작업이 가능
- 잦은 저장소 처리요소에도 부담이 없음
- 외부 저장소에 손실이 발생하더라도 빠르게 복구 가능



#### Remote Repository

- 전통적인 관점에서의 저장소 개념

- 외부 서버에 위치하여 변경 이력을 기록하는 부분

- 인터넷을 이용하여 접근 가능

- **다중 사용자로부터 관리되는 각 로컬 저장소의 접점**

  

---

### .gitignore

무시하는 파일 목록

<img src="/Users/yjaewoongnaver.com/Library/Application Support/typora-user-images/스크린샷 2021-02-23 오전 10.38.35.png" alt="스크린샷 2021-02-23 오전 10.38.35" style="zoom: 50%;" />

<img src="/Users/yjaewoongnaver.com/Library/Application Support/typora-user-images/스크린샷 2021-02-23 오전 10.38.54.png" alt="스크린샷 2021-02-23 오전 10.38.54" style="zoom:50%;" />



---

### Git의 구조



<img src="/Users/yjaewoongnaver.com/Library/Application Support/typora-user-images/스크린샷 2021-02-23 오전 10.41.34.png" alt="스크린샷 2021-02-23 오전 10.41.34" style="zoom:50%;" />

<img src="/Users/yjaewoongnaver.com/Library/Application Support/typora-user-images/스크린샷 2021-02-23 오전 10.52.25.png" alt="스크린샷 2021-02-23 오전 10.52.25" style="zoom:50%;" />



---

### 되돌리기

#### revert

하나의 커밋을 돌려놓기

#### reset

~ 커밋까지 돌아가기

---

### branch 

- $ git branch (브랜치 상태)
- $ git branch test1 (test1 브랜치 생성)
- $ git checkout test1 (test1 브랜치로 바꿈)
- $ git checkout -b test2 (한번에 생성과 교체 가능)

---



## 로컬에서 원격으로 연결하고 싶다 

###  github에서 미리 저장소를 만들었을 경우 

-  Local

  - \$ git init
  - \$ git add *
  - $ git commit -m "init"

  

  - 원격과 연결하기 

  - \$ git branch -M Master

  - \$ git remote add origin "https://github.com/Fezravien/test.git"

  - \$ git push -u origin master 

    - **로컬 레포지토리를 리모트 레포지토리로 처음 push할때는 --set-upstream 옵션을 줘야 한다.** 

      **그래야 tracking 정보 설정이 되어 git push만 사용해도 push가 된다.** 



---



## 브랜치 병합하기 !

 두개의 브랜치가 존재하는 상황에서 하나의 브랜치에서 다른 브랜치로 합치게 되는 경우 Git에서는 일반적으로 두 가지 방법이 있습니다.

1. Merge
2. Rebase

자주 사용하는 Merge에 비해 Rebase는 생소할 수 있습니다.

### Merge

Merge 브랜치의 전략은 `마지막 커밋 두개`와 `공통된 부모 커밋 `의 총 `3개의 커밋`을 이용하는 `3-way merge`를 수행하여 새로운 커밋을 만들어내는 것입니다.

<img src="/Users/yjaewoongnaver.com/Desktop/git-branches.png" alt="git-branches" style="zoom:30%;" />

여기서 `f2, m2, b` 이렇게 3개의 커밋을 이용하여 새로운 커밋을 만드는 것을 말합니다.



#### 왜 `3-way merge` 일까? 

비교를 위해 필요한 3개의 커밋을 보면 

1. 내 브랜치 커밋
2. 다른 브랜치 커밋
3. 두 브랜치의 공통된 부모 커밋

Git은 Merge를 할 때 각 브랜치의 마지막 커밋 두 개, 브랜치의 공통 조상 커밋 총 3개의 커밋을 비교하여 새로운 커밋을 만들어 병합을 수행합니다.

> 즉, 비교 대상이 있어야 무엇이 기준점인지 알 수 있기 때문입니다. 



###Rebase

두 브랜치를 합치는 두 번째 방법인 Rebase는 Merge와는 다르게 이름 그대로 브랜치의 `공통 부모`가 되는 base를 다른 브랜치의 커밋 지점으로 바꾸는 것 입니다. 

 <img src="/Users/yjaewoongnaver.com/Desktop/git-rebase.png" alt="git-rebase" style="zoom:33%;" />

rebase를 수행하고 얻고자 하는 목적은 master 브랜치의 마지막 커밋인 `m2`이후 feature의 변경사항인 `f1`, `f2` 가 일어난 것 처럼 보이게 하는 것 입니다. 즉, feature의 base를 b가 아니라 m2로 `재설정(Rebase)`하는 것입니다.

> feature를 master에 rebase한다 == feature의 master에 대한 공통 부모 base를 master로 변경한다



#### Rebase의 기본 전략 

Rebase 하려는 브랜치 커밋들의 변경사항을 Patch라는 것으로 만든 다음에 어딘가에 저장해 둡니다. 그리고 이를 master 브랜치에 하나씩 적용하여 새로운 커밋을 만드는 것입니다.

feature를 master 브랜치로 Rebase하는 명령어를 살펴보면 일련의 단계를 거쳐 두 브랜치의 병합이 완료됩니다.

1. feature 브랜치로 checkout
2. master 브랜치로 rebase
3. feature 브랜치를 master로 fast-forward merge



### Merge vs Rebase

Merge의 경우 히스토리에 작업한 내용의 사실을 기록합니다. Merge로 브랜치를 병합하게되면 커밋 내역에 Merge commit이 추가로 남게 됩니다.

하지만 Rebase의 경우 브랜치를 병합할 때 Merge commit을 남기지 않으므로, 마치 다른 브랜치는 없었던 것처럼 프로젝트의 작업 내용이 하나의 흐름으로 유지됩니다.

> 브랜치를 합칠 때 Merge를 써야 하는지 Rebase를 써야 하는지에 대해서는 정답이 없습니다. 프로젝트나 팀의 상황에 따라 다른 전략을 사용할 수 있습니다. 다만, 로컬에서는 히스토리 정리를 위해 Rebase를 할 수도 있지만 이미 원격 저장소에 Push된 커밋은 Rebase를 하지 않는 것이 일반적입니다.



> 출처 : https://velog.io/@godori/Git-Rebase

---

## 원격저장소로 부터 내용가지고 오기 !

### Pull vs Fetch

Git에서 원격저장소에 있는 내용을 로컬저장소로 가져올 떄 두가지 방법이 있습니다.

1. pull 
2. fetch 

두 가지 모두 원격 저장소로부터 내용을 가지고 온다는 점에서 기능은 유사하지만 차이점이 존재합니다.

- 원격저장소로 부터 내용을 가지고 온 후 `병합의 유무`

`pull`을 사용하게 되면 바로 병합을 같이 진행하게 되지만, `fetch`를 사용하면 병합을 수동으로 해줘야합니다. 이렇게 함으로 병합 전, 원격 저장소와 로컬 저장소의 코드이 차이점을 비교한 후 문제가 있는지 없는지 체크 해 볼 수 있습니다. 즉, **조심스럽게** 라고 말할 수 있습니다.

> 출처 : https://lsh424.tistory.com/22

---

## GIt 되돌리기 !

### Reset vs Revert

#### Reset

reset은 특정 사건으로 되돌아가게 되는데 과거로 되돌아 갔으니 해당 사건 이후의 사건들은 모두 사라지게 됩니다. 

```sh
$ git reset <옵션> <돌아가고 싶은 커밋 ID>

$ git reset --soft abcdef
$ git reset --mixed abcdef  # (옵션 작성안할 시 기본값)
$ git reset --hard abcdef 
$ git reset HEAD~10 # (현재부터 10개 이전으로 복원)
```

- soft : index 보존(add한 상태, staged 상태), 워킹 디렉터리의 파일 보존. 즉 모두 보존.
- mixed : index 취소(add하기 전 상태, unstaged 상태), 워킹 디렉터리의 파일 보존 (기본 옵션)
- hard : index 취소(add하기 전 상태, unstaged 상태), 워킹 디렉터리의 파일 삭제. 즉 모두 취소.

hard는 가장 깔끔하지만 해당 커밋 이후의 작업들이 모두 사라지므로 확신이 있을때만 신중하게 사용해야합니다.

mixed의 경우 soft와 달리 워킹 디렉토리는 유지되지만, index가 취소되므로 취소된 파일들을 다시 add 해줘야합니다.



#### Revert

특정 사건을 골라서 없던일로 만듭니다. 또한 과거 특정 사건을 없애주지만 revert를 했다는 이력이 남게됩니다.

그리고 없앨려 하는 특정 사건의 과거와 미래가 얽혀 충돌이 나는 경우가 잦습니다.

```sh
$ git rever <돌아가고 싶은 커밋 ID> 
```



> 출처 : https://git-scm.com/book/ko/v2/Git-


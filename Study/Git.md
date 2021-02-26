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
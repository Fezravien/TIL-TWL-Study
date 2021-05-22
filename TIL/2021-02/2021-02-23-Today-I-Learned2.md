---
layout: post
title: Today I Learned 📚
tags:
  - til
  - yagom-ios-camp-2nd
hero: https://source.unsplash.com/collection/14233285/
overlay: orange
published: true

---

{: .lead}
<!–-break-–>


# Today I Learned 🔥

---

## 2021.02.23 (화) 

---

### WITH 👥

[@inwoodev](https://github.com/inwoodev) (James)

---

### 학습내용 📖

#### Git - VCS(Version Control System)



##### 장점

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



##### Git 다루기

```sh
$ git init # 초기화
$ git status # 상태

$ git tag # 태그 조회
$ git tag [tag-name] # 현재 커밋에 태그 
$ git show [tag-name] # 태그에 해당하는 정보

$ git revert [commit] # 해당 커밋으로 돌아가기 - 원격
$ git reset # 커밋 되돌리기 - 로컬

$ git branch # 로컬 브랜치 보기
$ git branch -v # 로컬 브랜치 자세히 보기
$ git branch -r # 원격 저장소 브랜치 보기
$ git barnch -a # 로컬 && 원격
$ git branch [name] # 브랜치 생성
$ git branch -D [name] # 브랜치 삭제

$ git remote update # 원격 저장소에서 새로운 branch를 생성을 받아야한다. (git pull로 못함)

$ git checkout [name] # 브랜치 변경
$ git checkout -b [name] # 새로운 브랜치를 생성하고 새 브랜치로 이동
$ git checkout -u [remote/name] # 기존 원격 브랜치 추적하기
$ git checkout -t [remote/branch] # 기존 원격 브랜치를 추적하는 새로운 브랜치 만들기

$ git add a.txt # 추적 (stage)
$ git commit -m "add commit"

$ git push # 원격 저장소로
$ git log # 로그 확인

$ git merge [name] # 현재 브랜치에 병합

```



이 외에도 git에는 많은 명령어가 존재함을 알게되었습니다. 다른 부분은 프로젝트를 진행하면서 경험하면서 공부해야겠습니다!



##### Git 구조

<img src="/Users/yjaewoongnaver.com/Desktop/스크린샷 2021-02-23 오후 9.48.54.png" alt="스크린샷 2021-02-23 오후 9.48.54" style="zoom:50%;" />



- **Working Directory**

  실제 작업하고 있는 공간

- **Stage Area (add)**

  일종의 준비구역으로 Git의 변경이력을 관리하는 공간으로 이 곳에 올라와 있는 파일만 저장소에 추가 및 수정이 가능

- **Repository (push)**

  변경이력이 저장되는 공간으로 log에 기록이 남음

  - Local

  - Remote



##### . gitignore 

무시하는 파일 

<img src="/Users/yjaewoongnaver.com/Desktop/스크린샷 2021-02-23 오후 9.50.32.png" alt="스크린샷 2021-02-23 오후 9.50.32" style="zoom:50%;" />

<img src="/Users/yjaewoongnaver.com/Desktop/스크린샷 2021-02-23 오후 9.50.39.png" alt="스크린샷 2021-02-23 오후 9.50.39" style="zoom:50%;" />



---

### 문제점 / 고민한 점 ⁉️

 구구단 게임을 리펙토링 해볼때 고민했었던 동작단위로 구분하는 것을 이번 프로젝트에서도 고민하고 있습니다 !! 



---

### 해결방법

아직 해결을 하지 못했습니다 ㅠ

`James`와 머리를 싸매고 만들어 보겠습니다 ! 

****

**화이팅 🔥**
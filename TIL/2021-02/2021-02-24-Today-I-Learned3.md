---
layout: post
title: Today I Learned 📚
tags:
  - til
  - yagom-ios-camp-2nd
hero: https://source.unsplash.com/collection/2243327/
overlay: orange
published: true

---

{: .lead}
<!–-break-–>

# Today I Learned 🔥

---

## 2021.02.24 (월)

---

### 학습내용

#### 숫자 야구 [STEP 1] ⚾️

- **Git**

  - **stash**

    하던 작업 임시 저장하기 !

    git stash 나 git stash save 를 실행하면 스택에 새로운 stash가 만들어진다. 이 과정을 통해 working directory는 깨끗해진다.

    ```sh
    $ git stash
    $ git stash save
    ```

    


  - **add 취소(Unstage)**

    ```sh
    $ git reset HEAD [file] # 뒤에 파일명이 없으면 모두 취소
    ```

  - **commit 취소**

    ```sh
    # [방법 1] commit을 취소하고 해당 파일들은 staged 상태로 워킹 디렉터리에 보존
    $ git reset --soft HEAD^
    
    # [방법 2] commit을 취소하고 해당 파일들은 unstaged 상태로 워킹 디렉터리에 보존
    $ git reset --mixed HEAD^ // 기본 옵션
    $ git reset HEAD^ // 위와 동일
    $ git reset HEAD~2 // 마지막 2개의 commit을 취소
    
    # [방법 3] commit을 취소하고 해당 파일들은 unstaged 상태로 워킹 디렉터리에서 삭제
    $ git reset --hard HEAD^
    
    ```

  - **commit 수정**

    ```sh
    $ git commit --amend
    ```

  - **reset**

    *`git reset` 명령은 아래의 옵션과 관련해서 주의하여 사용해야 합니다.*

    

    - reset 옵션
      – `soft` : index 보존(add한 상태, staged 상태), 워킹 디렉터리의 파일 보존. 즉 모두 보존.
      – `mixed` : index 취소(add하기 전 상태, unstaged 상태), 워킹 디렉터리의 파일 보존 (기본 옵션)
      – `hard` : index 취소(add하기 전 상태, unstaged 상태), 워킹 디렉터리의 파일 삭제. 즉 모두 취소.

      

      **TIP** *만약 워킹 디렉터리를 원격 저장소의 마지막 commit 상태로 되돌리고 싶으면, 아래의 명령어를 사용한다.*

    - 단, 이 명령을 사용하면 원격 저장소에 있는 마지막 commit 이후의 워킹 디렉터리와 add했던 파일들이 모두 사라지므로 주의해야 합니다.

    ```sh
    # 워킹 디렉터리를 원격 저장소의 마지막 commit 상태로 되돌린다.
    $ git reset --hard HEAD
    ```

  -  **push 취소**

    + 이 명령을 사용하면 자신의 local의 내용을 remote에 강제로 덮어쓰기를 하는 것이기 때문에 주의해야 합니다.
    + 되돌아간 commit 이후의 모든 commit 정보가 사라지기 때문에 주의해야 합니다.
    + 특히, 협업 프로젝트에서는 동기화 문제가 발생할 수 있으므로 팀원과 상의 후 진행하는 것이 좋습니다.

    

    1. 워킹 디렉터리에서 commit 되돌린다.
       가장 최근의 commit을 취소하고 워킹 디렉터리를 되돌린다.

       ```sh
       # 가장 최근의 commit을 취소 (기본 옵션: --mixed)
       $ git reset HEAD^
       원하는 시점으로 워킹 디렉터리를 되돌린다.
       
       # Reflog(브랜치와 HEAD가 지난 몇 달 동안에 가리켰었던 커밋) 목록 확인
       $ git reflog 또는 $ git log -g
       
       # 원하는 시점으로 워킹 디렉터리를 되돌린다.
       $ git reset HEAD@{number} 또는 $ git reset [commit id]
       ```

       

    2. 되돌려진 상태에서 다시 commit을 한다.

       ```sh
       $ git commit -m "Write commit messages"
       ```

       

    3. 원격 저장소에 강제로 push 한다.

       ```sh
       $ git push origin [branch name] -f
       또는
       $ git push origin +[branch name]
       
       # Ex) master branch를 원격 저장소(origin)에 강제로 push
       $ git push origin +master
       ```

    

    **TIP** 경고를 무시하고 강제로 push 하기

    - [방법 1] -f 옵션
      –force 옵션과 동일하다.
    - [방법 2] +[branch name]
      해당 branch를 강제로 push한다.

    

    > 출처 : https://gmlwjd9405.github.io/2018/05/25/git-add-cancle.html

    

    

  

- **Naming**

  - Lower Camel Case

    fuction, method, variable, constant

    

  - Upper Camel Case

    type(class, struct, enum, extension…)



---

### 문제점 / 고민한 점 🤦🏼

1. git 

   - branch를 안바꾸고 main에 push -> 충돌 발생
   - add, commit 취소시키기
   - merge 충돌 방지를 위한 현재 변경사항 

    

2. naming

   - 코드 변수와 상수 같은 `이름`에는 규칙이 있다 !

   - 이름에도 함축된 의미가 `찰떡`으로 매치되야된다 !

     

3. 코딩테스트 테크 후 고민

   - 코테를 못하면 면접 기회도 없다 .. 

---

### 해결방법 🙋🏼

- branch를 안바꾸고 main에 push -> 충돌 발생

  > 그라운드 룰을 잘 지키면서 자신의 브랜치를 만들어서 작업한다! (변경 전 브랜치 확인 필수)

  

- add, commit 취소시키기

  > ```sh
  > # add cancel
  > $ git reset HEAD [file]
  > # commit cancel
  > $ git reset --hard HEAD^
  > ```

  

- merge 충돌 방지를 위한 현재 변경사항 

  > stash 명령어를 통해 현재 작업중인 변경사항을 저장
  >
  > ```sh
  > $ git stash
  > $ git stash save
  > ```



- 코드 변수와 상수 같은 `이름`에는 규칙이 있다 ! && 이름에도 함축된 의미가 `찰떡`으로 매치되야된다 !

  > `리나`의 리뷰를 받아보고 변수와 상수에 있어서 대문자 소문자 그리고 동작과 관련된 네이밍에 대해 생각해볼 수 있었다.
  >
  > ```swift
  > ex) let STRIKE --> let strike 
  > ```



- 코딩테스트 

  > 틈 날때마다 꾸준하게 해야겠다는 생각을 새삼 느끼게 되었습니다 🤥


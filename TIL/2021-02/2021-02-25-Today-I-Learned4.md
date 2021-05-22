---
layout: post
title: Today I Learned 📚
tags:
  - til
  - yagom-ios-camp-2nd
hero: https://source.unsplash.com/collection/4828371/
overlay: orange
published: true

---

{: .lead}
<!–-break-–>

# Today I Learned

---

## 2021.02.26 (목)

---

### 학습내용

- 땅따먹기 (CS - Game)

  + CPU (폰노이만, 하버드)

- rom (read only momery) / ram 

  - 주기억 장치

    - rom

      - `Read Only Memory`
      - `비교적 느림`
      - `항구적 기억장치`
      - `비 휘발성 메모리`

    - ram

      - `Random Access Memory`

      - `비교적 빠름`

      - `비교적 빠른 속도`

      -  `휘발성 메모리`

        

  - 보조기억 장치

    - 중앙처리장치와 직접 자료 교환이 **불가**

    -  접근시간이 비교적 오래 걸림

    - 일반적으로 주기억장치에 데이터를 저장할 때는 **DMA** 방식을 사용

    - CPU가 직접 접근 불가

      

      **보조기억장치 종류**

    - 하드디스크 ( 읽기 쓰기를 하는 컴퓨터 외부 기억장치)

    - CD (디지털 기억 매체)

    - 자기 테이프 (플라스틱 자기 테이프를 사용한 대용량 디지털 기억 장치)

    - 광디스크: 대용량 기억장치 & 빛 반사를 이용해서 자료 읽어내는 저장매체

      

- 숫자야구게임 (STEP 1 수정 및 STEP 완성)

  - naming

    - num -> number
    - com -> computer

    **딱 봤을때 영어문장처럼 의미를 이해할 수 있게 코드를 작성해야 된다.**

  - 개행 

    - 개인의 가독성 보다는 보편적인 가독성을 배우자 (참고 : https://awesomeopensource.com/project/StyleShare/swift-style-guide#들여쓰기-및-띄어쓰기)

      

- git !!!!!!!!!!!!!!!!!!!!!!!!!!!!!

  - branch (local, remote)

    ```sh
    $ git branch [브랜치명] # 브랜치 생성
    $ git checkout -b [브랜치명] # 브랜치 생성 후 이동
    $ git push origin [브랜치명] # git remote 브랜치 생성
    $ git branch --set-upstream-to origin/[브랜치명] # 로컬 브랜치와 리모트 브랜치 연동
    $ git branch -D [브랜치명]
    ```

    

  - main으로 PR을 진행중 일때 push만 해도 PR이 날라간다 !!!!!!!!!!!!!!

    + 그러므로 브랜치 관리를 잘해야 불상사를 막을 수 있다.

---

### 문제점 / 고민한 점 / 해결방법

- 숫자야구게임 

  - 재귀함수로 인한 문제

    while로 반복을 수행하면서 오류처리로 밖에 메소드를 재귀형식으로 호출하다보니 while의 조건을 무시하는 상황이 발생했다.

    ```swift
    func A() {
      while a < 10 {
        if a > 5 {
          
        } else {
          func A()
        }
      }
    }
    ```

    예시 코드와 같이 메소드 A에서 while 반복문이 돌때 예외처리 식으로 메소드 A를 재호출하면서 오류가 발생한것 같다 

    > dump 를 통해 문제점을 파악했다,




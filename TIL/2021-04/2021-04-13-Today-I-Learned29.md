---

layout: post
title: Today I Learned 📚
tags:
  - TIL
  - yagom-ios-camp-2nd
hero: https://source.unsplash.com/collection/4409024/
overlay: orange
published: true


---

{: .lead}
<!–-break-–>


# Today I Learned 🔥

## 2021.04.13 (월)

### 학습내용 📝

활동학습의 주제는 고차함수로, 클로저를 다시한번 보고 고차함수를 살펴보는 시간을 가졌다.

#### 클로져

- 이름이 있으면서 어떤 값도 획득하지 않는 전역함수의 형태
- 이름이 있으면서 다른 함수 내부의 값을 획득할 수 있는 중첩된 함수의 형태
- 이름이 없고 주변 문맥에 따라 값을 획득할 수 있는 축약 문법으로 작성한 형태

<img width="700" alt="스크린샷 2021-04-12 오전 10 11 46" src="https://user-images.githubusercontent.com/44525561/114413485-fdefc800-9be8-11eb-9a59-1609f5a74f1d.png">

<img width="700" alt="스크린샷 2021-04-12 오전 10 14 03" src="https://user-images.githubusercontent.com/44525561/114413492-ff20f500-9be8-11eb-8fce-cfdba50e6107.png">

<img width="700" alt="스크린샷 2021-04-12 오전 10 15 31" src="https://user-images.githubusercontent.com/44525561/114413497-ffb98b80-9be8-11eb-8d0c-1d682932415a.png">





<br/>

#### 고차함수

- 스위프트는 함수를 일급 객체로 취급한다. 따라서 함수를 다른 함수의 전달인자로 사용할 수 있다. 
- 매개변수로 함수를 갖는 함수를 고차함수라고 부른다.

##### MAP

- 자신을 호출할 때 매개변수로 전달된 함수를 실행하여 그 결과를 다시 반환해주는 함수이다.
- 맵을 사용하면 컨테이너가 담고 있던 각각의 값을 매개변수를 통해 받은 함수에 적용한 후 다시 컨테이너에 포장하여 반환한다.
- 기존 컨테이너의 값은 변경되지 않고 새로운 컨테이너가 생성되어 반환된다.
- 맵은 기존 데이터를 변형하는데 많이 사용된다.

<img width="700" alt="스크린샷 2021-04-12 오전 10 25 48" src="https://user-images.githubusercontent.com/44525561/114413498-00522200-9be9-11eb-8911-d5ffe4bcf729.png">

<img width="700" alt="스크린샷 2021-04-12 오전 10 26 45" src="https://user-images.githubusercontent.com/44525561/114413502-00522200-9be9-11eb-93e1-e23035a6d708.png">

<img width="700" alt="스크린샷 2021-04-12 오전 10 27 28" src="https://user-images.githubusercontent.com/44525561/114413510-021be580-9be9-11eb-90be-78fbd6990f56.png">

<img width="700" alt="스크린샷 2021-04-12 오전 10 28 15" src="https://user-images.githubusercontent.com/44525561/114413513-034d1280-9be9-11eb-9574-514a12d640ff.png">

<br/>

##### Filter

- 컨테이너 내부의 값을 걸러서 추출하는 역할을 하는 고차함수이다.
- 맵과 마찬가지로 새로운 컨테이너에 값을 담아 반환해준다.
- 맵처럼 기존 콘텐츠를 변형하는 것이 아니라, 특정 조건에 맞게 걸러내는 역할을 할 수 있다는 점이 다르다.

<img width="700" alt="스크린샷 2021-04-12 오전 10 28 36" src="https://user-images.githubusercontent.com/44525561/114413517-03e5a900-9be9-11eb-8f00-3aac0531f632.png">



<img width="700" alt="스크린샷 2021-04-12 오전 10 28 50" src="https://user-images.githubusercontent.com/44525561/114414151-89695900-9be9-11eb-82a5-b9deb2d231e8.png">

<img width="700" alt="스크린샷 2021-04-12 오전 10 29 04" src="https://user-images.githubusercontent.com/44525561/114414160-8b331c80-9be9-11eb-9473-0c68b1c63cbd.png">

<img width="700" alt="스크린샷 2021-04-12 오전 10 29 23" src="https://user-images.githubusercontent.com/44525561/114414162-8bcbb300-9be9-11eb-8b5e-0c04d8d336cc.png">



<br/>

##### Reduce

- 사실 결합이라고 불러야 마땅한 기능이다.
- 리듀스는 컨테이너 내부의 콘텐츠를 하나로 합하는 기능을 실행하는 고차함수이다.
- 배열이라면 배열의 모든 값을 전달인자로 전달받은 클로저의 연산 결과로 합해준다.

<img width="700" alt="스크린샷 2021-04-12 오전 10 31 34" src="https://user-images.githubusercontent.com/44525561/114414168-8cfce000-9be9-11eb-9e8f-a3fc1bdfb84b.png">



<br/>

#### 반복문과 고차함수의 성능차이?

- 컴파일 시간

  - 고차함수의 타입 유추에 의해 조금 차이가 날 수 있다.

- 런타임 시간

  - 거의 차이가 없다 

  

---

### 문제점 / 고민한 점 🤦🏼 / 해결방법 🙋🏼

스텝 1에서 했어야 되는 테스트를 안해서 테스트를 해보려고 했다 !

- 캠프를 하면서 습관아닌 습관?

  - `class` 가 보이면 `final` 생각하기

  - 모든 부분에 접근제어 생각하기 (`private`)

    

- 유닛 테스트를 만들고 습관처럼 `final`과 `private`를 메소드에 붙였다.

  - 틀린 케이스를 넣어도 성공했다고 알림만 뜨고 왼쪽에 테스트 색상은 변하지 않았다.
  - 여기서 final은 문제가 되지 않았지만 테스트 메소드에 private를 쓰는것은 잘못됨을 깨달았다!!

  



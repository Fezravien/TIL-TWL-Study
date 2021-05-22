---
layout: post
title: Today I Learned 📚
tags:
  - til
  - yagom-ios-camp-2nd
hero: https://source.unsplash.com/collection/2229334/
overlay: orange
published: true

---

{: .lead}
<!–-break-–>

# Today I Learned

---

## 2021.02.22 (월)

---



### 학습내용

- **자신의 코드 설명하기**

 캠프에 참가하기 위해 사전과제인 구구단 코드를 캠퍼들에게 설명해주고 질문을 받으며 그에 대해서 대화하는 시간을 가졌습니다. 코드는 짧았지만 어디서 부터 어디까지 설명해야 될지 생각보다 난감한(?) 느낌이 들었었고, 앞으로는 나만의 규칙을 정하여 설명을 해야겠다는 생각할 수 있었습니다.

- **캠퍼의 코드 리뷰하기**

 캠퍼의 코드를 리뷰하며 나와 다르게 설계한 부분에 의문을 가지고 대화를 했고, 이를 통해 나의 코드가 어떻게 개선될 수 있을지 생각해볼 수 있는 계기가 되었습니다. 역시 하나의 문제에도 여러가지 접근법과 그에 따른 코드가 나올 수 있음을 새삼 느낄 수 있었습니다.

- **캠퍼들과 코드 리펙토링**	

 구름 IDE를 통해 3명의 캠퍼와 페어 프로그래밍을 드라이버, 내비게이터, 타이머로 나눠 시간을 분활하여 진행했습니다. 생각과는 다르게  쉽게 완성되지 않았지만, 여러번 역할을 바꿔가며 만들었고 그 후 캠퍼들과 코드에 대한 생각을 얘기했습니다. 그리고 새롭게 코드를 만들어보며 구조에 대해서 생각해보았습니다.



---

### 문제점 / 고민한 점 

- **돌아가만 가는 코드가 아닌 좋은 코드란?** 

```swift
class gugudan {
  func startGame() {
    switch num
    case: error
    case: exit
    case: success
  }
}

let gugu = gugudan()
gugu.startGame()
```

 세부적인 로직이 아닌 구구단이라는 코드 설계에 대해서 생각을 해봤습니다. 위의 설계 처럼 gugudan 클레스를 통해 인스턴스를 만들어 startGame() 메소드를 호출하고 메소드 안에서 모든 동작이 이뤄지는 코드를 기존에 작성했었습니다.

아무래도 하나의 메소드에 모든 동작이 있으면 가독성과 유지보수가 조금 떨어진다고 생각했고 설계에 대해서 캠퍼들과 고민을 했습니다. 



---

### 해결방법

- **하나의 동작은 하나의 메소드에서...**

```swift
class Gugudan {
  func startGame() {
    error()
    exit()
    success()
  }
}

extension Gugudan {
  func error()
  func exit()
  func success()
}

let gugu = gugudan()
gugu.startGame()
```

 하나의 메소드에서 모든 행위를 구현하는 것이 아닌 동작(error, exit, success)라는 3가지 작업에 대해 메소드를 extenstion을 활용해 분리함으로써 좀더 가독성 높은 방법에 대해 생각해볼 수 있었습니다.

****

**화이팅 🔥**
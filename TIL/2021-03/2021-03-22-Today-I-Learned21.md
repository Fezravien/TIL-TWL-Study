---
layout: post
title: Today I Learned 📚
tags:
  - TIL
  - yagom-ios-camp-2nd
hero: https://source.unsplash.com/collection/14233285/
overlay: orange
published: true

---

{: .lead}
<!–-break-–>

# Today I Learned 🔥

## 2021.03.22 (월)

### 학습내용 📝

#### Stack

- 후입선출 자료구조 (Last In First Out)이다.

- 배열과 비슷하지만! 접근이 더 많은 제한과 컨트롤이 있다.

  - 스택은 요소에 접근하는 방법을 제어하는 컨트롤이 있다.

- 구현해보자면 

  - `push`

    - 스택의 마지막에 요소 추가한다.

  - `pop`

    - 스택의 가장 위에 있는 요소를 제거하고 반환한다.

  - `top` 

    - 스택의 가장 위에 있는 요소를 반환하지만, 제거하지는 않는다.

  - `count`

    - 스택이 가지고 있는 요소의 개수를 반환한다.

  - `isEmpty`

    - 스택이 비어있는지 아닌지를 반환한다.

    

  ```swift
  public struct Stack<T> {
      private var array = [T]()
      
      public var isEmpty: Bool {
          return array.isEmpty
      }
      
      public var count: Int {
          return array.count
      }
      
      public mutating func push(_ element: T) {
          array.append(element)
      }
      
      public mutating func pop() -> T? {
          return array.popLast()
      }
      
      public mutating func reset() {
          array.removeAll()
      }
      
      public var top: T? {
          return array.last
      }
  }
  ```



#### 제네릭 이란?

- `제네릭`을 이용해 코드를 구현하면 어떤 타입에도 유연하게 대응할 수 있다.
- `제네릭`으로 구현한 기능과 타입은 재사용하기도 쉽고, 코드의 중복을 줄일 수 있다.
- `제네릭`을 사용하고자 할 때는 제네릭이 필요한 타입 또는 메서드의 이름 뒤의 `<>` 기호 사이에 제네릭을 위한 타입 매개변수를 써주어 제네릭을 사용할 것임을 표시한다.

##### 제네릭 함수

- 제네릭 함수는 실제 타입 이름을 써주는 대신에 `placeholder`를 사용한다. [ eg: T, V, U ]
- placeholder는 타입의 종류를 알려주지 않지만 어떤 타입이라는 것은 알려준다.
- placeholder의 실제 타입은 함수가 호출되는 순간 결정된다.
- placeholder는 타입 매개변수로 쓰일 수도 있는데, 이 타입 매개변수는 함수를 호출할 때마다 실제 타입으로 치환된다.
- 하나의 타입 매개변수를 갖지 않고 여러 개의 타입 매개변수를 갖고 싶다면 홀화살괄호 기호 안쪽에 쉼표로 분리한 여러 개의 타입 매개변수를 지정해줄 수 있다. [ eg: <T, U> ]
- 의미 있는 이름으로 타입 매개변수의 이름을 지정해주면 제네릭 타입 및 제네릭 함수와 타입 매개변수와의 관계를 더 명확하게 표현해줄 수 있다. [ eg: Dictionary<Key, Value>, Array[Element], .. ]

##### 제네릭 타입

- 제네릭 타입을 구현하면 `구조체`, `클래스`, `열거형` 등이 어떤 타입과도 연관되어 동작할 수 있다.

- 제네릭 타입을 정해주면 그 타입에만 동작하도록 제한할 수 있어 안전하고 의도한 대로 기능을 사용하도록 유도할 수 있다.

  > 위 스택 예제를 참고해보자 ! 



> 출처 : [제네릭](https://velog.io/@zooneon/Swift-제네릭에-대해-알아보자)

---

### 문제점 / 고민한 점 🤦🏼

- 아이폰의 기본 어플인 계산기가... 생각보다 만들기 어렵다 !!
- 스택을 이용해서 어떻게 우선순위 계산을 해줄 수 있을까? 
- 우선 10진수 계산만 해보자!

---

### 해결방법 🙋🏼

- 스택을 적극적으로 이용해보기로 했다!
  - top 으로 요소 존재여부 확인
  - 입력된 연산자 말고 정수 스트링을 지속적으로 받는 것의 count 
  - 이번 값으로 연산자가 오는지 정수가 오는지 ! 

<img width="1000" alt="image" src="https://user-images.githubusercontent.com/44525561/112021669-dfac2480-8b74-11eb-9462-d926e267c148.png">


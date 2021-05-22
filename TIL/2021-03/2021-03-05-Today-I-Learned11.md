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

# Today I Learned 🔥



## 2021.03.05 (금)



### 학습내용

#### 열거형 (enum) 고급 !!

##### 프로토콜 

- 스위프트 열거형은 하나의 데이터 타입으로 정의 된다.

- 구조체와 유사한 점들이 많이 있다.

  - 메서드나 프로퍼티(열거형은 연산 프로퍼티만 가능)를 정의할 수 있다.

  - 둘 다 Call by Value로 메모리 주소를 복사하지 않고 값이 복사되는 형태이다.

  - **스위프트에서 가장 많이 활용 되는 프로토콜을 적용할 수 있다**

    

  - 프로토콜 선언

    - 키보드를 만들어 보자 !

      - 모든 키보드에는 여러가지 공통점이 존재한다. 그중 `스위치` 로 살펴보자
      - 그리고 키보드는 스위칭을 통해 스위치를 바꿀 수 있는 기능이 있다.

      ```swift
      protocol 키보드프로토콜 {
        	var 스위치: String { get }
        	mutating func 타이핑() -> Self
      }
      ```

      > 변수에 `get`(읽기) 만 들어있는 것은 열거형에서는 연상 프로퍼티만 사용할 수 있기 때문이다. (`set` - 쓰기) 

      

  - 열거형 프로토콜 채택
    - 키보드프로토콜을 각 변수에 채택해서 `스위치`, `스위칭`을 구현하도록 한다.

    ```swift
    enum 체리스위치: 키보드프로토콜 {
    		case 적축
      	case 흑축
      	case 청축
      	
      	var 스위치: String {
          	switch self {
              case .적축:
              	return "적축"
              case .흑축:
              	return "흑축"
              case .청축:
              	return "청축"
            }
        }
      
      	func 스위칭() -> 체리스위치 {
          	switch self {
              case .적축:
              	return .흑축
              case .흑축:
              	return .청축
              case .청축:
              	return .적축  
            }
        }
    }
    ```

    ```swift
    enum 게이트론스위치: 키보드프로토콜 {
    		case 갈축
      	case 백축
      	case 황축
      	
      	var 스위치: String {
          	switch self {
              case .갈축:
              	return "갈축"
              case .백축:
              	return "백축"
              case .황축:
              	return "황축"
            }
        }
      
      	func 스위칭() -> 게이트론스위치 {
          	switch self {
              case .갈축:
              	return .백축
              case .백축:
              	return .황축
              case .황축:
              	return .갈축 
            }
        }
    }
    ```

  - 사용하기
    - 프로토콜을 채택하여 만든 프로퍼티와 메서드 사용하는 방법은 기존에 직접 정의 했을때 처럼 사용

    ```swift
    var 체리 = 체리스위치.적축
    print(체리.스위치) // "적축"
    
    체리 = 체리.스위칭() // 적축 -> 흑축
    print(체리.스위치) // "흑축"
    
    체리 = 체리.스위칭() // 흑축 -> 청축
    print(체리.스위치) // "청축"
    ```

  ##### 

##### 익스텐션 (extension)

- `열거형`도 `익스텐션`을 사용하여 케이스와 메서드, 프로퍼티를 분리하여 가독성을 높일 수 있다.

  

- 익스텐션 사용하기

  - 케이스와 메서드, 프로퍼티를 `익스텐션`을 사용해서 분리할 수 있다.
  - 여러 `프로토콜`을 채택한 `열거형`이라면 각 `프로토콜` 별로 `익스텐션`을 만들어서 관리할 수도 있다.

  ```swift
  enum 체리스위치 {
    	case 적축
    	case 흑축
    	case 청축
  }
  
  extension 체리스위치: 키보드프로토콜 {
    	var 스위치: String {
        	switch self {
            case .적축:
            	return "적축"
            case .흑축:
            	return "흑축"
            case .청축:
            	return "청축"
          }
      }
    
    	func 스위칭() -> 체리스위치 {
        	switch self {
            case .적축:
            	return .흑축
            case .흑축:
            	return .청축
            case .청축:
            	return .적축 
          }
      }
  }
  ```

  

- 프로토콜 익스텐션 만들기

  - `프로토콜` 자체를 `익스텐션`하여 `프로토콜`이 요구하는 사항을 모두 한꺼번에 구현할 수 있는 방법이 `프로토콜 익스텐션`이다.
    - 프로토콜 익스텐션을 활용하면 중복되는 코드를 피할 수 있다. 
    - 프로토콜을 채택한 곳에서 프로토콜이 요구하는 사항을 모두 구현해 줄 필요가 없다.

  ```swift
  protocol 키보드프로토콜 {
    	var 스위치: String { get }
    	mutating func 타이핑() -> Self
  }
  
  extension 키보드프로토콜 {
    	var 스위치: String {
        	return String(describing: self)
      }
  }
  
  enum 체리스위치: 키보드프로토콜 {
  		case 적축
    	case 흑축
    	case 청축
    	
    	func 스위칭() -> 체리스위치 {
        	switch self {
            case .적축:
            	return .흑축
            case .흑축:
            	return .청축
            case .청축:
            	return .적축 
          }
      }
  }
  
  var 체리 = 체리스위치.적축
  print(체리.스위치) // "적축"
  체리 = 체리.스위칭()
  print(체리.스위치)	// "흑축"
  체리 = 체리.스위칭()
  print(체리.스위치) // "청축"
  ```

  > 스위치프로토콜을 채택 한 후 스위치를 구현하지 않았지만 오류가 나지 않는다.

  

-  프로토콜 익스텐션 재정의

  - 만약 스위치를 각 항목의 이름이 아닌 좀 더 멋진 스위치로 바꾸고 싶다면 열거형 안에서 재정의 해주면 된다.

  ```swift
  enum 체리스위치: 키보드프로토콜 {
  		case 적축
    	case 흑축
    	case 청축
    
    	var 스위치: String {
        	switch self {
            case .적축:
            	return "조용한 리니어 타입의 스위치"
            case .흑축:
            	return "조용하지만 키앞이 높은 리니어 타입의 스위치"
            case .청축:
            	return "전형적인 클릭 타입의 스위치"
          }
      }
    	
    	func 스위칭() -> 체리스위치 {
        	switch self {
            case .적축:
            	return .흑축
            case .흑축:
            	return .청축
            case .청축:
            	return .적축 
          }
      }
  }
  
  var 체리 = 체리스위치.적축
  print(체리.스위치) // "조용한 리니어 타입의 스위치"
  체리 = 체리.스위칭()
  print(체리.스위치)	// "조용하지만 키앞이 높은 리니어 타입의 스위치"
  체리 = 체리.스위칭()
  print(체리.스위치) // "전형적인 클릭 타입의 스위치"
  ```





---

### 문제점 / 고민한 점 🤦🏼

  프로젝트의 상태값을 명시하는 것을 구조체로 하는 것이 좋을까? 열거형으로 하는게 좋을까?

- 원래 `enum`을 사용했었는데, 값(정수)을 반환하는 메소드를 사용하기 위해 `rawValue`를 지속적으로 사용했다.
  그래서 값으로 쓰는 방법은 `enum` 보다 `struct`에 하드코딩을 해서 `static`을 이용해 범용 상수로 사용하고 싶어서 `struct` 로 사용했다.

```swift
struct Hand {
    static let rock = 1
    static let scissors = 2
    static let paper = 3
}
struct GameResult {
    static let win = "이겼습니다!"
    static let lose = "졌습니다!"
    static let draw = "비겼습니다!"
}
struct GameConditions {
    static let endGame = 0
    static let initValue = -1
    static let userTurn = "User"
    static let computerTurn = "Computer"
    static let endGamePresent = "게임 종료"
}
struct WinLoseDrawOfUserAtRockScissorsPaper {
    static let userSelectWinRockScissors = 1
    static let userSelectWinScissors = -2
    static let userSelectLoseScissorsRock = -1
    static let userSelectLosePaper = 2
    static let userSelectDraw = 0
}
```



---

### 해결방법 🙋🏼

 이번 프로젝트에서는 `정형화 된 데이터(캡슐화)`를 저장하는 구조체가 아니라 상태 값을 저장한 `enum`이 적합하다고 생각했다
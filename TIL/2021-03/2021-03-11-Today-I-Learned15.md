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

## 2021.03.11 (목) 🗓

### 학습내용 📝

### 문제점 / 고민한 점 🤦🏼

#### Singleton Pattern 

**특정 용도로 객체를 하나만 생성하여, 공용으로 사용하고 싶을 때 사용하는 디자인 유형**

``` swift
class UserInfo {
  	var id: String?
  	var password: String?
  	var name: String?
}
```



- A : ViewController - `id` 
- B : ViewController - `password`
- C : ViewController - `name`

```swift
// A
let userInfo = UserInfo()
userInfo.id = "Sodeul"

// B
let userInfo = UserInfo()
userInfo.password = "123"

// C 
let userInfo = UserInfo()
userInfo.name = "Fezz"
```



<img src="https://blog.kakaocdn.net/dn/b7DLbv/btqOYtTGZ4t/2HuCG2pgmg1TcJMkxhIne1/img.png" alt="img" style="zoom:50%;" />

- 이렇게 각 instance의 프로터티에만 저장된다. (즉, 다르다!!)
  - instance는 참조 타입이기 때문에, User Info instance를 한번 생성한 후, 이를 instance A->B->C로 필요할 때마다 참조로 넘겨줄 수 있다.
  - But! App 어디 클래스든 UserInfo 인스턴스가 참조되어야 할 때마다 매번 instance를 넘겨줘야한다 (귀찬쓰..)



##### 이 클래스에 대한 Instance는 최초 생성될 때 딱 한번만 생성해서 전역에 두고, 그 이후로는 이 Instance만 접근 가능하게 하자

- 이게 **싱. 글. 톤. 패. 턴.** 이다!!

<img src="https://blog.kakaocdn.net/dn/VmsQc/btqOYt0xgaU/k4fR7SVzSexrukeToKNAKk/img.png" alt="img" style="zoom:50%;" />



##### Singleton Class 만드는 방법 

- static 프로퍼티로 Instance 생성하기 (**쥬스 메이커 step1 에서 싱글톤 사용하기 !!!!**)

  ```swift
  class FruitStock {
      public private(set) var fruits: Storage
      
      static let shared = FruitStock()
  }
  ```



- init 함수 접근제어자를 private로 지정하기 

  ```swift
  class FruitStock {
      public private(set) var fruits: Storage
      
      static let shared = FruitStock()
    
      private init() {
        	self.fruits = [:]
          initStorage(amount: 10)
      }
    
    	private func initStorage(amount: Int) {
          for kindFruit in Fruits.allCases {
              fruits.updateValue(amount, forKey: kindFruit)
          }
      }
  }
  ```

  - **포인트 !!!!** 

    - 가만히 보면 `FuritStock` 클래스 안에서 `static let shared = FruitStock()`으로 Instance를 생성하고 있으니까 결국 `init`은 클래스 속안에서 초기화 되는것을 알 수 있다. 그러므로 초기화를 위해서 초기화 메모드를 새로만들고 private init() 에서 다시 호출해 주는 것으로 나는 해결했다 !!!

      

-  Singgleton Class 접근하는 방법 

  ```swift
  
  class JuiceMaker {
      
      var fruitStorage = FruitStock.shared // 싱글톤 생성
      
      func make(order: Juices) {
  
      }
      
      func consumeFruit(fruit kind: Fruits, amount: Int) {
  
      }
      
      func addFruitStock(fruit kind: Fruits, amount addFruits: Int = 1) {
    
      }
      
      func hasFruitStock(fruit kind: Fruits, amount: Int) throws {
        
      }
      
      func currentFruitStock() -> Storage {
  
      }
  }
  
  ```

  - 저희 팀은 이런식으로 구조를 작성하고 `var fruitStorage = FruitStock.shared` 으로 과일 저장소 싱글톤으로 사용 !!

  

- Singleton 장단점

| **장점** | - 한 번의 Instance만 생성하므로 메모리 낭비를 방지할 수 있음 - Singleton Instance는 전역 Instance로 다른 클래스들과 자원 공유가 쉬움 - DBCP(DataBase Connection Pool)처럼 공통된 객체를 여러개 생성해서 사용해야하는 상황에서 많이 사용 (쓰레드풀, 캐시, 대화상자, 사용자 설정, 레지스트리 설정, 로그 기록 객체등) |
| -------- | ------------------------------------------------------------ |
| **단점** | - Singleton Instance가 너무 많은 일을 하거나, 많은 데이터를 공유시킬 경우 다른 클래스의 Instance들 간 결합도가 높아져 "개방=폐쇄" 원칙을 위배함 (객체 지향 설계 원칙 어긋남) - 따라서 수정과 테스트가 어려워짐 |

- **포인트 !!!!**
  - 전역변수를 사용해 인스턴스를 생성하면, `사용 시점에 초기화(lazy)` 되어 `최초 Singleton Instance가 최초 생성되기 전까진` **메모리에 올라가지 않다.**
  - 따라서 Instance가 여러 개 생성되지 않는, `Thread-Safe한 방법`이다!!



##### iOS 에선 Singletion을 언제 쓸까?

```swift
let screen = UIScreen.main
let userDefault = UserDefaults.standard
let application = UIApplication.shared
let fileManager = FileManager.default
let notification = NotificationCenter.default
```



- 꼭 한번만 `Instance`를 생성하고 프로그램이 끝날때 까지 사용하는 거야 !!



> https://babbab2.tistory.com/66



### 문제점 / 고민한 점 🤦🏼

- 딸기, 바나나, 파인애플, 키위, 망고 
  - 범용적으로 활용할 방법이 있지 않을까?

---

### 해결방법 🙋🏼

- 싱글톤으로 하면 전체를 프로그램 끝날때 까지 유지할 수있지 않을까?

  - 이번 PR에서 적용을 해봤다 !!! 

    ```swift
    class FruitStock {
        public private(set) var fruits: Storage
        
        static let shared = FruitStock() // 싱글톤
        
        private init() {
    
        }
        
        func manageStorage(fruit kind: Fruits, amount: Int) throws {
    
        }
        
        private func initStorage(amount: Int) {
    
        }
    }
    class JuiceMaker {
        
        var fruitStorage = FruitStock.shared // 싱글톤 생성 
        
        func make(order: Juices) {
    
        }
        
        func consumeFruit(fruit kind: Fruits, amount: Int) {
    
        }
        
        func addFruitStock(fruit kind: Fruits, amount addFruits: Int = 1) {
    
        }
        
        func hasFruitStock(fruit kind: Fruits, amount: Int) throws {
        }
        
        func currentFruitStock() -> Storage {
        }
      
    }
    
    
    ```

    
  
  
  
  
  
  - 저희 조는 이렇게 과일 저장소를 싱글톤으로 생성하고 쥬스 메이커에서 사용하는 방식으로 했습니다 !! 
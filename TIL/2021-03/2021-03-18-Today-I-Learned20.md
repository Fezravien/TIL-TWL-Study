---
layout: post
title: Today I Learned 📚
tags:
  - TIL
  - yagom-ios-camp-2nd
hero: https://source.unsplash.com/collection/2243327/
overlay: orange
published: true

---

{: .lead}
<!–-break-–>



# Today I Learned 🔥

## 2021.03.18 (목) 🗓

### 학습내용 📝

### 초기화 (Initializer) 

**스위프트에서 옵셔널 타입으로 선언되지 않은 모든 저장 프로퍼티는 인스턴스가 생성되기 전에 반드시 초기값이 설정되어야 한다.**



### 상속 관계에 있을 때에는 초기화 메소드를 주의해서 사용해야한다. 

- 부모의 초기화 메소드는 자식 클래스에 추가된 새로운 저장 프로퍼티를 `초기화`하지 못하므로, 이를 그래도 상속받아 사용할 경우 `초기화`되지 않는 저장 프로퍼티가 생길 수 있다.

- 방지하기 위해 일반적으로 부모의 초기화 메소드는 자식 클래스에 `상속`되지 않는다.

  - 단, 자식 클래스에서 새로 정의된 모든 저장 프로퍼티가 선언과 동시에 `초기화`된다면 초기화 메소드에서 이를 굳이 다시 `초기화`할 필요는 없기 때문에, 특별한 케이스로 간주하여 부모의 `초기화 메소드`를 `상속`받을 수 있다.

    

### 자식 클래스에서 초기화 메소드를 구현할 때에도 주의해야한다. 

- `초기화 메소드`가 상속되지 않는 까닭에 자식의 초기화 메소드는 부모 클래스의 `저장 프로퍼티`까지 모두 `초기화`해 줘야한다.

- 하지만 부모의 `저장 프로퍼티`를 하나하나 초기화하는 것은 번거로울 뿐만 아니라, 어떤 값으로 `초기화`해야 하는지도 일일이 확인하여 구현해야 하므로 상당히 복잡해질 수 있다. (이래서는 `상속`받는 의미가 없다 !)

  - 부모의 `저장 프로퍼티`를 직접 `초기화`하기보다는 부모 클래스의 `초기화 메소드`를 호출하여 간접적으로 `초기화`하는 방법을 사용한다. (어차피 부모의 초기화 메소드라면 부모에 정의된 저장 프로퍼티를 모두 초기화하고 있을 테니까 !)

    ```swift
    class Boo {
       	var v: Int = 0
      	var c: String = ""
    }
    
    class BooEx: Boo {
      	var d: Int
      
      	override init() {
          	self.d = 0
          	super.init()
        }
    }
    ```

    > 초기화 메소드의 델리게이션(Delegation) - 초기화 메소드의 연쇄 호출
    >
    > 자식부터 부모의 부모의 부모의 부모의 ... 부모 까지 타고 올라가면서 초기화 

    **"모든 맴버(저장 프로퍼티)는 적절한 초기값을 가지고, 누락 없이 완전히 초기화되어야 한다."**



## 지정 초기화 메소드와 편의 초기화 메소드

 `클래스`가 여러 개의 `초기화 메소드`를 가지고 있을 때 각각의 `초기화 메소드`가 처리하는 내용은 모두 조금씩 다를 것이다. 하지만 동시에, 서로 다른 초기화 메소드일지라도 일관되게 처리해야 하는 부분이 있을 수 있다. 이를 위해서는 초기화 메소드들이 모두 일부 동일한 코드를 포함하고 있어야 한다. (`비효율`)

### 초기화 체인 (Initializer Chain)

#### 지정 초기화 메소드 (Designated Initializer)

##### 클래스의 메인 초기화 메소드 

- 모든 맴버,  즉 저장 프로퍼티를 초기화해야 하는 의무가 있다.
- `지정 초기화`  메소드의 수를 최소화하려는 경향이 있기 때문에 여러 개의 초기화 메소드가 있더라도 지정 초기화 메소드는 보통 하나인 경우가 많다.
  - 코드의 중복을 줄이기 위해 다른 초기화 메소드들은 모두 내부적으로 지정 초기화 메소드를 호출하는 깔대기 모양의 호출 구조를 만듬
  - **자동 초기화 메소드 상속**

#### 편의 초기화 메소드 (Convenience Initializer)

##### 사용에 편의를 주기 위해 정의하는 보조적인 초기화 메소드이다.

- 일부 혹은 전체 맴버에 대해서 별도의 초기값을 설정하는 동시에, 내부적으로 다른 초기화 메소드를 다시 호출합니다.

- 반드시 정의해야 하는 것은 아니다.

- `지정 초기화` 메소드와의 구분을 위해 `convenience` 기워드를 붙여준다.

  ```swift
  convenience init() { }
  ```



##### 지정 초기화 메소드와 편의 초기화 메소드 사이에는 다음과 같은 호출 규칙이 존재한다. 이는 상속 관계에 있는 클래스의 모든 저장 프로퍼티를 효율적으로 초기화하기 위한 목적이다.

1. `지정 초기화` 메소드는 자신의 모든 `저장 프로퍼티`를 초기화한 후, 이어서 부모의 `지정 초기화` 메소드를 호출해야 한다.

2. `편의 초기화` 메소드는 같은 클래스 내에 정의된 다른 초기화 메소드를 반드시 호출해야 한다.

3. `편의 초기화` 메소드의 연쇄 호출은 최종적으로 지정 초기화 메소드를 호출하는 것으로 끝나야 한다.

    

<img src="http://minsone.github.io/image/2014/09/initializersExample02_2x.png" alt="Swift-Initialization 정리" style="zoom:67%;" />

- 정리 !!
  1. `지정 초기화` 메소드는 항상 `상위 방향`으로 호출한다.
  2. `편의 초기화` 메소드는 항상 `수평 방향`으로 호출한다.

---



## 2단계 초기화와 안전 점검

스위프트에서 클래스 초기화는 2단계에 걸쳐 이루어진다.

## 1단계 초기화 

- 부모 방향으로 거슬러 올라가면서 모든 프로퍼티의 초기값을 만들어준다.

## 2단계 초기화

### 다시 자식 방향으로 내려오면서 초기화된 프로퍼티 중 일부를 필요에 맞게 커스터마이징한다.

- 이때 컴파일러는 2단계 초기화를 오류 없이 완료할 수 있도록 다음의 안전 점검을 수행한다.

  1. `지정 초기화` 메소드는 부모의 초기화 메소드를 호출하기 전에, 현 클래스에서 정의된 모든 `저장 프로퍼티`를 초기화해야 한다. 이미 초기화되어 있는 프로퍼티는 다시 초기화하지 않아도 된다.

  2. `상속`받은 `저장 프로퍼티`를 직접 초기화하려면, 그전에 먼저 부모의 초기화 메소드를 호출해야한다. 순서가 바뀌면 자신이 초기화한 값을 부모 클래스가 다시 다른 값으로 초기화해버릴 위험이 있다.

  3. `편의 초기화` 메소드에서 저장 프로퍼티를 직접 초기화하려면  그전에 먼저 다른 초기화 메소드를 호출해 줘야한다. 순서가 바뀌면 자신이 초기화한 값을 지정 초기화 메소드가 다시 초기화해버릴 위험이 있다.

  4. 1단계 초기화가 끝나기 전에는 `인스턴스 메소드`를 사용할 수 없으며, `인스턴스 프로퍼티`를 읽을 수도 없으며, `self`를 참조해서도 안 된다.

      

## 초기화 세부적 과정 

### 1 단계 세부적 과정 (초기화)

1. `클래스`에서 `지정 초기화` 메소드 또는 `편의 초기화` 메소드가 호출된다.
2. `클래스` 인스턴스에 대한 메모리가 할당된다. 아직 메모리는 초기화 되지 않은 상태이다.
3. `지정 초기화` 메소드가 호출되면서 현 클래스의 모든 프로퍼티를 초기화한다. 아직 `상속`받은 프로퍼티들은 초기화되지 않은 상태이다.
4. `지정 초기화` 메소드는 부모의 `지정 초기화` 메소드를 호출한다. 이제 부모 클래스에서 정의한 프로퍼티가 초기화된다.
5. 이 과정은 계층의 `최상위 클래스`에 이를 때까지 계속된다.
6. 계층의 끝에 도달하여 마지막 클래스의 모든 저장 프로퍼티까지 초기화되면 인스턴스 메모리는 클래스가 충분히 초기화된 것으로 간주한다. 이것으로 **1단계가 끝**난다.

### 2 단계 세부적 과정 (초기값 커스터마이징)

1. 계층의 `최상위 클래스`에서 다시 아래로 한 단계식 내려간다.
2. 바로 다음 단계의 `지정 초기화` 메소드 뒷부분에서 필요한 `커스터마이징`이 실행된다.
3. 이 과정이 계속해서 반복되어 현 단계의 클래스까지 이어져 내려오게 된다.
4. 이제 현 단계의 `편의 초기화` 메소드까지 흐름이 오고 나면 `인스턴스 메소드`나 `self`를 모두 안전하게 참조할 수 있다



---

### 문제점 / 고민한 점 🤦🏼

- 커스텀 라벨 클래스로 각각의 라벨을 관리할 수 있을까?

  - Delegate Pattern 사용해보기 

  ```swift
  // JuiceData
  protocol StockDelegate {
    	func currentStock(fruit: Fruits)
  }
  
  // FruitStorage
  var delegate: FruitStockLabel?
  
  func manageStorage(fruit kind: Fruits, amount: Int) {
      guard let stock = fruits[kind] else {
          return NSLog(JuiceMakerError.invalidStock.localizedDescription)
      }
      fruits.updateValue(stock + amount, forKey: kind)
      delegate.currentStock(fruit: kind)
  }
  
  // FruitStockLabel
  func currentStock(fruit: Fruits) {
      self.text = "\(juiceMaker.fruitStorage.fruits[fruit]!)"
  }
  ```

  > 분명,, 뭔가 놓치고 있다... 



### 해결방법 🙋🏼

- 커스텀 라벨에 `노티피케이션 센터`로 라벨 별로 수량 관리

```swift
final class FruitStockLabel: UILabel {
    private var juiceMaker = JuiceMaker.shared
    private(set) var kindFruit: Fruits?
    
    required init?(coder: NSCoder) {
        super.init(coder: coder)
        NotificationCenter.default.addObserver(self,
                                               selector: #selector(updateLabel(_ :)),
                                               name: Notification.Name(rawValue: "changeFruitAmount"),
                                               object: nil)
        self.layer.backgroundColor = .init(gray: 0.8, alpha: 0.6)
        self.layer.cornerRadius = 10
        self.layer.borderWidth = 1
        self.adjustsFontSizeToFitWidth = true
    }
    
    func initValue(fruit: Fruits) {
        guard let amount = juiceMaker.fruitStorage.fruits[fruit] else {
            return
        }
        self.kindFruit = fruit
        self.text = String(amount)
    }
    
    @objc private func updateLabel(_ notification: Notification) {
        guard let fruit = kindFruit, let amount = juiceMaker.fruitStorage.fruits[fruit] else {
            return
        }
        self.text = String(amount)
    }
}
```
---
layout: post
title: Today I Learned 📚
tags:
  - TIL
  - yagom-ios-camp-2nd
hero: https://source.unsplash.com/collection/3728885/
overlay: orange
published: true

---

{: .lead}
<!–-break-–>

# Today I Learned 🔥

## 2021.03.15 (월) 🗓

### 학습내용 📝

#### NotificationCenter 란?

- `NotificationCenter` 에 등록된 `event` 가 발생하면 해당 `event`에 대한 행동을 한다.

- 앱 내에서 메세지를 던지면 아무데서나 이 메세지를 받을 수 있게 하는 역할을 한다.

- 보통 `백그라운드 작업`의 결과, `비동기 작업`의 결과 등 현재 작업의 흐름과 다른 흐름의 작업으로부터 이벤트를 받을 때 사용한다.

  

  <img src="https://blog.kakaocdn.net/dn/bha9T2/btqI082BBfE/s3vLeZzvH3XhK4Vk6saXk1/img.png" alt="img" style="zoom:40%;" />

  

##### Notification

- `NotificationCenter` 를 통해 정보를 저장하기 위한 구조체이다.

  ```swift
  var name: Notification.Name // 알림을 식별하는 태그
  var object: Any? // 발송자가 옵저버에게 보내려고 하는 객체. 주로 발송자 객체를 전달하는 데 쓰임
  var userInfo: [AnyHashable : Any]? // Notification과 관련된 값 또는 객체의 저장소
  ```



##### NotificationCenter

- 등록된 `observer` 에게 동시에 `notification` 을 전달하는 클래스이다.

- `NotificationCenter` 는 `notification` 을 발송하면 `NotificationCenter`에서 메세지를 전달한 `observer`를 처리할 때까지 대기한다. 즉, 흐름이 `동기적`으로 흘러간다.

  ```swift
  // 노티피케이션 발송
   NotificationCenter.default.post(name: NSNotification.Name("TestNotification"), object: nil, userInfo: nil)
  ```

  - `.post` 가 핵심 !!
    - Name의 해당자들에게(`옵저버`) 일을 수행하라고 시킨다.

  ```swift
  // 옵저버 등록
   NotificationCenter.default.addObserver(self, selector: #selector(didRecieveTestNotification(_:)), name: NSNotification.Name("TestNotification"), object: nil)
  
   @objc func didRecieveTestNotification(_ notification: Notification) {
           print("Test Notification")
   }
  ```

  - **addObserver** 
    - 관찰자를 대기시킴

  - **selector** 
    - 관찰자가 수행해야 할 업무를 의미

   

##### Name 등록 방식

1. `addObserver` 할 때 한 번에 하기

```swift
// Post
NotificationCenter.default.post(name: Notification.Name("doItSomeThing"), object: nil)
// Add Observer
NotificationCenter.default.addObserver(self, selector: #selector(printSomeThing(_:)), name: Notification.Name("doItSomeThing"), object: nil)
```

2. Extension 으로 property 추가

```swift
extension Notification.Name {
    static let doItSomeThing = Notification.Name("doItSomeThing")
}
```



##### Post 값 전달하기

Post메소드 파라미터에 `object`가 있습니다. 위 예시에서는 nil을 넣었지만, 이 부분을 통해 값을 보낼 수도 있습니다.

```swift
NotificationCenter.default.post(name: .testnoti, object: "testobject")
```

object 부분에 "testobject" 라는 string 값을 넣어 post 해줍니다.

```swift
@objc func getValue(_ notification: Notification){
	let getValue = notification.object as! String
	print(getValue)
}
```

- notification.object 로 값을 받아옵니다.

> 출처 : https://silver-g-0114.tistory.com/106



### 문제점 / 고민한 점 🤦🏼

- 과일 저장소를 전체적으로 업데이트하는 것은 낭비다!

  - 어떻게 딸기, 바나나, 파인애플, 키위, 망고 각각에 변화에 대처해서 UILabel에 업데이트 시킬 수 있을까?

  

### 해결방법 🙋🏼

- `NotificationCenter` 활용하기

```swift
 // ViewController
override func viewDidLoad() {
        NotificationCenter.default.addObserver(self,
                                               selector: #selector(updateLabel(_ :)),
                                               name: Notification.Name(rawValue: "changeFruitAmount"),
                                               object: nil)
    }

@objc private func updateLabel(_ notification: Notification) throws {
        
    }
```



```swift
// FruitStorage 
func manageStorage(fruit kind: Fruits, amount: Int) {
  		// 변경되는 부분
      fruits.updateValue(fruits[kind]! + amount, forKey: kind) 
  		// 변경이 발생되었다고 호출 + Fruits타입의 kind 변수를 object로 넘겨줌
      NotificationCenter.default.post(name: Notification.Name(rawValue: "changeFruitAmount"), object: kind) 
    }
```


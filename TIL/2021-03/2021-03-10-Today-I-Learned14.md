---
layout: post
title: Today I Learned 📚
tags:
  - TIL
  - yagom-ios-camp-2nd
hero: https://source.unsplash.com/collection/11663747/
overlay: orange
published: true

---

{: .lead}
<!–-break-–>

11663747
# Today I Learned 🔥

## 2021.03.10 (수) 🗓

### 학습내용 📝

#### Design Patterns

##### MVVM (Model, View, ViewModel)

- `MVC` 패턴은 다양한 로직을 `Controller`에서 처리하다보니 `Controller`에 비지니스 로직이 몰려서 복잡해져 커지는 문제가 있다.
  - `MVVM` 패턴은 `View`에 업데이트할 데이터를 `ViewModel`에서 처리함으로써 `Controller`가 복잡해지는 것을 줄여준다. (기존 `MVC` 패턴에서는 `ViewController`에서 처리 
- MVVM 구조
  - `Model`
    - 데이터 보유
  - `View`
    - 시각적 요소, 컨트롤 표시 (UI에 반영되는 코드 && 생명주기 관리 코드 등..)
  - `ViewModel` 
    - Model에서 가져온 데이터를 View에 맞게 가공 및 처리

<img src="https://blog.kakaocdn.net/dn/lA3JT/btqNDn8KdRB/Chj1vpTATGE0xFt99aNFNk/img.png" alt="img" style="zoom:70%;" />



- **간단한 예제코드로 MVVM 알아보기**

  - MVVM 파일의 구성 

    <img src="https://blog.kakaocdn.net/dn/b8jsCA/btqNBe5TGKJ/k68kf26zWIyuqantPuaNfK/img.png" alt="img" style="zoom:50%;" /> 

    

    > Controller, Views, Models, ViewModels로 파일을 분류 (Controller - 스토리보드, 코드 두 가지 형식)
    >
    > 여기 예시는 강아지지만 저는 키보드를 가지고 한번 만들어 보겠습니다 !!!

  - Model

    ```swift
    // Model
    class Keyboard {
        
        // 키보드 스위치
        enum Switchs {
            case red
            case black
            case blue
            case brown
        }
        
        let name: String
        let type: String
        let switchs: Switchs
        let image: UIImage
        
        init(name: String, type: String, switchs: Switchs, image: UIImage) {
            self.name = name
            self.type = type
            self.switchs = switchs
            self.image = image
        }
    }
    ```

    

  - `Model`을 사용해 받아온 데이터를 가공하기 위한 `ViewModel`을 만든다.

  - ViewModel

    ```swift
    import Foundation
    import UIKit
    
    // MARK: - ViewModel
    class DogViewModel {
        let keyboard: Keyboard
        
        init(keyboard: Keyboard){
            self.keyboard = keyboard
        }
        
        var name: String {
            return keyboard.name
        }
      
      	var type: String {
            return keyboard.type
        }
        
        var image: UIImage {
            return keyboard.image
        }
        
        var priceText: String {
            switch keyboard.type {
                case .red:
                    return "₩15000"
                case .black:
                    return "₩21000"
                case .blue:
                    return "₩12000"
                case .brown:
                    return "₩18000"
            }
        }
    }
    
    extension DogViewModel {
        func configure(_ view: KeyboardView) {
            view.nameLabel.text = name
            view.imageView.image = image
            view.typeLabel.text = typeText
            view.priceLabel.text = priceText
        }
    }
    ```

  - 데이터를 띄워줄 KeyboardView의 경우 UI와 Layout관련 코드들이 있다. (스토리보드를 사용하지 않을시 View 따로.. 아닌경우 Controll와 같은 구역에 있다.)

  - View + Controller

    ```swift
    import UIKit
    
    // 스토리보드를 사용하여 뷰 구성할 경우 
    class ViewController: UIViewController {
        
        // MARK: - View
        @IBOutlet weak var imageView: UIImageView!
        @IBOutlet weak var nameLabel: UILabel!
        @IBOutlet weak var typeLabel: UILabel!
        @IBOutlet weak var priceFeeLabel: UILabel!
        
        
        override func viewDidLoad() {
            super.viewDidLoad()
            
            // data
            guard let image = UIImage(named: "keyboardRED.jpeg") else {
              return
            }
        
            let pomeranian = Dog(name: "keyboardRED", 
                                 type: type, 
                                 switchs: .red, 
                                 image: image)
            
            let viewModel = keyboardViewModel(keyboard: red)
            
            imageView.image = viewModel.image
            nameLabel.text = viewModel.name
            typeLabel.text = viewModel.typeText
            priceLabel.text = viewModel.priceText
        }
    }
    
    ```

    

- 정리 !

  - `MVVM` 장점 
    - 테스트 용이성 ( ViewModel에는 UIKit 관련된 코드가 없으므로 UI에 독립적인 테스트 가능)
    - Controller 부담감을 경감
  - `MVVM` 단점
    - 바인딜을 도와주는 라이브러리를 함께 사용하지 않으면 많은 코드를 작성해야 함
  - 1개의 View = 1개의 ViewModel 존재



출처의 예시를 기반으로 작성했습니다. 코드에 세부적인 내용은 틀릴 수 있으니 전체적인 MVVM 구조를 봐주세요! 

> 출처 : https://lsh424.tistory.com/68?category=948937



---

### 문제점 / 고민한 점 🤦🏼

- 다음 `step 2 ~ 3`에서 앱을 만들기 위해 `step 1` 에서 데이터와 그것을 가공하는 로직을 작성할 때 어떻게 파일을 기능별로 분류하고 어디에 어떤 로직을 넣을까?
- 과일 저장소는 앱 전체에서 범용적으로 사용되지 않나?

---

### 해결방법 🙋🏼

- MVC와 MVVM을 공부해보면서 동작하는 부분과 상태를 나타내는 부분은 다른 파일에 존재하면 좋다고 생각했다.
  - JuiceMaker, JuiceMakerModel로 나눔
    - JuiceMaker 에서는 데이터를 가공(음료 만들기, 재고 추가하기, 재고 보여주기 )
    - JuiceMakerModel 에서는 (과일 저장소 🍓🍌🥭🥝🍍)
- 범용적으로 사용하는 과일 저장소를 `싱글톤 패턴`으로 구현해봤다.

![아침으로 간편하게 딸바 한잔!? 콜? 딸기바나나쥬스 [만개의레시피] - YouTube](https://i.ytimg.com/vi/YFWrsPqQqpM/hqdefault.jpg)

> 너어어어어어는 .... 정말 !!!!!!
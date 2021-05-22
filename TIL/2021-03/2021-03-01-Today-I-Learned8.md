---
layout: post
title: Today I Learned 📚
tags:
  - til
  - yagom-ios-camp-2nd

hero: https://source.unsplash.com/collection/4409024/
overlay: orange
published: true

---
{: .lead}
<!–-break-–>


# Today I Learned 🔥



## 2021.03.01 (월)



### 학습내용

#### 타입의 일반화/추상화

- 일반화란?
  - 연관성 있는 두 개 이상의 개체 집합을 묶어 좀 더 상위의 개체 집합을 만드는 것 

- 추상화란?
  - 중요한 특징을 추출해서 간단하게 표현하는 것 

> 일반화랑 추상화랑 상반된 관계라는 생각을 가지고 있어서 더 힘들었던거 같다. -> 연관은 있지만 반대 관계는 아니다!!

##### 추상화를 하려면 일반화를 먼저 해야봐야된다? 

추상화를 할때 일반화를 거쳐야된다. 그리고 일반화에서 모든 특성 중 중요한 것만 추려낸것(우리가 필요한 것)이 `추상화` 🖼

----



#### Class

- 같은 종류의 집단에 속하는 속성과 행위를 정의한 것

  

#### Instance

- Class의 실체화된 인스턴스(객체)는 자신만의 고유한 속성(변수, 함수)을 가질 수 있으며, 클래스에서 정한 행위(함수, 메소드)를 수행할 수 있다.
- 클래스를 실체화(Instance) 하면 객체(Object)를 만들수 있다.

```swift
// Subject 클래스 생성
Class Subject {
	var name: String = ""
	var score: Int = 0
}

// instance 생성
var newSubject: Subject = Subject()
```



#### Method

- 클래스로부터 생성된 객체를 사용하는 방법으로서 객체에 명령을 내리는 메시지라 할 수 있다.
- Method는 Class(enum, struct 등..)내에 선언된 함수를 말한다.

```swift
// Student Class의 인스턴스 name: "Amy", id: 2011111050으로 생성
var s1 = Student(name: "Amy", id: 2011111050)
s1.setSubjects(subjects: [math, english, computer])
```



#### 객체의 속성

##### **추상화(Abstraciton)**

- 클래스를 정의하는 것 : **공통의 속성이나 기능을 묶어 이름을 붙이는 것**

```swift
class Subject {
var name: String
var score: Int = 0
var grade: String = "F"
var gradePoint: Double = 0.0
var credit: Int = 1

// instance를 생성할 때, 무조건 name이 초기화 됨
init(name: String) {
    self.name = name
}

 // score 값을 저장할 수 있는 메소드 -> 추상화 
func setScore(score: Int) {
    self.score = score
}
}
```



##### **캡슐화(Encapsulation)**

- class안에 관련된 변수와 메소드를 묶어 넣는 것
- 코드의 수정 없는 재활용을 위한 작업



##### **은닉화**

- 메소드의 로직이나 멤버 변수들에 대해 외부로 보이지 않게 하는 것
- `접근지정자`: 클래스의 멤버에 접근할 수 있는 권한을 통제 
- 데이터에 대한 `읽기` or `쓰기`권한 구분 가능
- 입력데이터의 유효성 검증 부분을 로직에 포함 시킬 수 있음 

```swift
class Subject {
  
    private var name: String
    private var score: Int = 0
    
	// 직접적으로 score 변수에 값을 변경 시킬 수 없다. 
  // setScore 메소드를 통해서만 score 값을 변경시킬 수 있다 -> 은닉화 
    func setScore(score: Int) {
        self.score = score
    } 
  
  // instance를 생성할 때, 무조건 name이 초기화 되고, 추후에 바꿀 수도 없음
    init(name: String) {
        self.name = name
    } 
}
```



##### **상속성(Inheritance)**

- 상위 개념의 특징을 하위 개념이 물려받는 것
- 부모 클래스(super, parent)와 자식 클래스(sub, child)
- 자식 클래스가 부모 클래스의 속성을 이용할 수 있게 하는 기능
- [참고] Class는 상속하는 것이고, **Struct에서 Protocol은 선택하는 것**

```swift
class ViewController: UIViewController { }
```



##### **다형성(Polymorphism)**

- 기존에 구현되어있는 클래스를 확장, 변형
- **재정의(Override)** : 부모 클래스에게서 물려받은 성질을 그대로 사용하지 않고 자식 클래스에게 맞는 형태 또는 행위로 변경하여 사용할 수 있는 기능
- **상속을 받은 클래스에 한해서** 부모 클래스의 속성(메소드)을 재정의 가능하다.

```swift
class ViewController: UIViewController {
    override func viewDidLoad() {
    // func viewdDidLoad는 원래 부모의 것(UIViewController)이나, 이를 재정의하겠다는 의미
    super.viewDidLoad()
    // 부모(super)의 method(viewDidLoad)를 먼저 호출해주고 아래에  viewDidLoad() 재정의 코드 작성
}
```



> 출처 : [객체 지향 프로그래밍](https://amywork.github.io/2017-09-13/Object)



### Rock Scissors Paper Game

- STEP 1 - 구조도 그림

  [![image](https://user-images.githubusercontent.com/44525561/109505114-9cafe180-7adf-11eb-8d12-e1f548ce02ef.png)](https://user-images.githubusercontent.com/44525561/109505114-9cafe180-7adf-11eb-8d12-e1f548ce02ef.png)

---

### 문제점 / 고민한 점 🤦🏼

- [STEP1] 이라고 커밋을 남겨야 하는 상황에 오타로 인해 [STEP2] 라는 커밋 실수를 했다.
  1. `git commit --amend`
  2. `git rebase -i`

---

### 해결방법 🙋🏼

첫 번째 방식인 `git commit --amend`는 마지막 커밋 메시지만 바꿀 수 있었다.. (pass)

두 번째 방법은 중간의 커밋 메시지도 바꿀 수 있는 방법으로 `git rebase -i HEAD~3` 최근 커밋으로 부터 3 번째까지 ~ 나는 뜻이다.

그러면 `vi` 에디터가 나오게 되고 맨위에 커밋이 순서대로 id와 함께 보인다. 

<img src="/Users/yjaewoongnaver.com/Desktop/스크린샷 2021-03-02 오전 12.26.11.png" alt="스크린샷 2021-03-02 오전 12.26.11" style="zoom:25%;" />

이 부분에서 `pick -> edit` 으로 바꾸고 `vi` 에디터를 저장하고, `git commit --amend ` 을 입력하게 되면 다시 `vi` 에디터가 뜨게 되는데 이 부분에 수정하고자 한 커밋 메세지를 작성하면 수정할 수 있다. 

마지막 !! `push`를 하지 않았을 시 `git rebase --continue` 만 하면 마무리 된다. 만약 `push`를 했다면 `git push -f`도 해줘야 한다.




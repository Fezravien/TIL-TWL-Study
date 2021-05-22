---
layout: post
title: Today I Learned 📚
tags:
  - TIL
  - yagom-ios-camp-2nd
hero: https://source.unsplash.com/collection/4585827/
overlay: orange
published: true

---

{: .lead}
<!–-break-–>

# Today I Learned 🔥



## 2021.03.08 (월)



### 학습내용 📝

#### 디자인 패턴

- Design Patterns (1994) - The "Gang of Four"

##### 디자인 패턴의 의미

- OOP의 다양한 문제 상황에 대한 예방
- 프로그래머 사이의 협업효율 향상 
- 프로그래머 사이의 의사소통 증진
- 코드의 안정화 및 최적화
- 코드의 재사용성 증가

**단, 적절히 잘! 사용했을 때!** 

> 과유불급 - 주객전도가 되는 상황이 올 수 있다 

##### Design Patterns vs Architectures

- 혼용이 되기도 하고 비슷한 개념이기도 하다
- Architectures
  - 큰 그림 
  - 건축 양식
- Design Patterns 
  - Architectures 에서 세세한 해결방식을 제시

##### Model-View-Controller (MVC)

- 모두 다 객체 



####  Dictionary 

- 딕셔너리는 요소들이 순서 없이 키와 값의 쌍으로 구성되는 컬렉션 타입이다.
- 딕셔너리에 저장되는 값은 항상 키와 쌍을 이룬다
  - 딕셔너리 안에는 키가 하나이거나 여러 개일 수 있다.
  - 하나의 딕셔너리 안의 키는 같은 이름을 중복해서 사용할 수 없다.
- 딕셔너리는 배열과 다르게 딕셔너리 내부에 없는 키로 접근해도 오류가 발생하지 않는다.
  
  - 하지만 `nil`을 반환
  
  <br/>

#####  Dictionary 초기화

```swift
var dictionary : [Int : String] = [:]
var dictionary2 = [Int : String]()
var dictionary3 : Dictionary = [Int:String]()
var dictionary4 : Dictionary<Int, String> = Dictionary<Int, String>()
```

<br/>

##### Dictionary 값 수정

```swift
var dictionary : [Int : String] = [1:"Fezz", 2:"iOS", 3:"Swift"]
dictionary.updateValue("Fezz", forKey: 3)
print(dictionary) //[1:"Fezz", 2:"iOS", 3:"Fezz"]
dictionary[3] = "iOS"
print(dictionary) //[1:"Fezz", 2:"iOS", 3:"iOS"]
```

<br/>

#####  Dictionary 값 추가

```swift
var dictionary : [Int : String] = [1:"Fezz", 2:"swift", 3:"iOS"]
dictionary.updateValue("Fezz", forKey: 4 ) //주의 : updateValue는 Optional값을 반환함
print(dictionary) //[1:"Fezz", 2:"swift", 3:"iOS", 4:"Fezz"]
dictionary[5] = "Hello"
print(dictionary) //[1:"Fezz", 2:"swift", 3:"iOS", 4:"Fezz", 5:"Hello"]
```

<br/>

#####  Dictionary 값 접근

```swift
var dictionary : [Int : String] = [1:"Fezz", 2:"swift", 3:"iOS"]
print(dictionary[1]!) //Fezz
print(dictionary[2]!) //swift
print(dictionary[3]!) //iOS
var dictionary2 : [String : Int] = ["Fezz":30, "swift":40,"iOS":50]
print(dictionary2["Fezz"]!) //30
print(dictionary2["swift"]!) //40
print(dictionary2["iOS"]!) //50
//key의 값으로 접근이 가능

var dictionary3 : [String : String] = ["Fezz":"30", "swift":"40","iOS":"50"]
print(dictionary3["30"]) //nil. "30"을 Value로 가지는 쌍은 있지만, "30"을 Key로 가지는 쌍이 없기때문. 
//무조건 Key값으로 접근해야 Value를 얻어올 수 있음.
```

<br/>

#####  Dictionary 값 삭제

```swift
dictionary = [1:"Fezz", 2:"swift", 3:"iOS", 4:"fun", 5:"Hello"]
dictionary.removeValue(forKey: 5)
print(dictionary) //[1:"Fezz", 2:"swift", 3:"iOS", 4:"fun"]
dictionary.removeAll() //Dictionary의 모든 Key와 Value를 삭제
print(dictionary) //[:]
dictionary = ["Fezz": 1] //error! [Int:String]타입의 Dictionary였으므로. 타입을 바꿔줄 수 없다.
```

<br/>

> 출처 : [딕셔너리](https://zeddios.tistory.com/129)

---

### 문제점 / 고민한 점 🤦🏼

- `쥬스메이커` 프로젝트를 하면서 `switch` 가 너무 많아서 점점 코드가 길어지는 문제가 있었다. 
- class ? struct ? enum ? 

---

### 해결방법 🙋🏼

- `switch` 를 지양하고 다시 로직을 짜면서 딕셔너리를 이용하면서 상당히 짧아짐을 느낄 수 있었다.
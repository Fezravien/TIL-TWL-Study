---
layout: post
title: Today I Learned 📚
tags:
  - til
  - yagom-ios-camp-2nd

hero: https://source.unsplash.com/collection/14233285/
overlay: orange
published: true

---
{: .lead}
<!–-break-–>


# Today I Learned 🔥

## 2021.05.14 (금)

### 학습내용

#### CustomStringConvertible

<img src="/Users/yjaewoongnaver.com/Library/Application Support/typora-user-images/스크린샷 2021-05-14 오후 2.26.30.png" alt="스크린샷 2021-05-14 오후 2.26.30" style="zoom: 45%;" />



우선 공식문서를 살펴보기로 했다.

우선 `CustomStringConvertible`은 프로토콜이고,  "커스텀한 타입을 표현하다".. 라고 써있는데 무슨말인지 와닿지 않는다

<br/>

##### 설명

<img src="https://raw.githubusercontent.com/Fezravien/UploadForMarkdown/forUpload/img/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-05-14%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%202.30.56.png" alt="스크린샷 2021-05-14 오후 2.30.56" style="zoom:45%;" />

이해가 잘 안되니까 설명을 한번 읽어봐야지 ..

`CustomStringConvertible` 프로토콜을 채택한 타입에 인스턴스를 문자열로 변환할때 사용할 표현을 할 수있게 해준다.

`String(describing:)` initializer는 모든 type의 instance를 문자열로 변환해주는 방법이다.

만약 전달된 instance가 `CustomStringConvertible`을 채택하고 있는 경우에는 `String(describing:)` initializer와 `print(_:)` 함수는 instance의 custom된 description 프로퍼티를 사용하게 된다. 

type의 description 프로퍼티에 직접적으로 접근하거나, `CustomStringConvertible`을 일반 제약 조건으로 사용하는 것은 권장하지는 않는다고 한다. 

<br/>

----

##### 예시

역시 이해가 가지 않죠 ?

```swift
struct Point {
    let x: Int, y: Int
}

let p = Point(x: 2, y: 3)
print(p.x, p.y)
// "2 3"
print(p)
// "Point(x: 2, y: 3)"
```

- 직접 프로퍼티에 접근해 출력
- 인스턴스를 출력

<br/>

```swift
extension Point: CustomStringConvertible {
    var description: String {
        return "(\(x), \(y))"
    }

let p = Point(x: 2, y: 3)
print(p)
// "(2, 3)"
```



##### rawValue vs description

프로젝트를 진행하면서 `String` 을 받고 싶어서 사용하다보니 `rawValue ` 과 `CustomStringConvertible` 의 `description` 무슨 차이가 있을지에 대해 질문을 받았다.

```swift
// CustomStringConvertible
enum MarketAPIPath: CustomStringConvertible {
    case items
    case registrate
    case item
    case edit
    case delete
    
    var description: String {
        switch self {
        case .items:
            return "/items/"
        case .registrate:
            return "/item"
        case .item:
            return "/item/"
        case .edit:
            return "/item/"
        case .delete:
            return "/item/"
        }
    }
}

// rawValue
enum MarketAPIPath: String {
    case items = "/items/"
    case registrate = "/item"
    case item = "/item/"
    case edit = "/item/"
    case delete = "/item/"
}
```

문자열을 반환 받아서 사용하기 위해서 `CustomStringConvertible` 프로토콜을 채택해서 사용했는데 ... 사실 `rawValue` 와 뭐가 다르지? 생각을 하게 되었다. 사실 `CustomStringConvertible` 프로토콜을 채택하는게 불필요 해보였다. 그래서 사용하면 좋을 수  있는 상황을 생각해보기로 했다.

```swift
enum MarketAPIPath: String, CustomStringConvertible {
    case items = "GET"
    case registrate = "POST"
    case item = "GET"
    case edit = "PATCH"
    case delete = "POST"
    
    var description: String {
        switch self {
        case .items:
            return "/items/"
        case .registrate:
            return "/item"
        case .item:
            return "/item/"
        case .edit:
            return "/item/"
        case .delete:
            return "/item/"
        }
    }
}
```

예시와 같이 기본적으로 `rawValue`를 사용하는 상황에서 다른 문자열을 반환하는 경우에 `CustomStringConvertible` 프로토콜을 사용하면 좋지 않을까 생각이 들었다. 

그리고 

```swift
struct Point2: CustomStringConvertible {
    let x: Int, y: Int

    var description: String {
        return "TAK"
    }
}

let p = Point2(x: 2, y: 3)
print(p) // TAK 

```

`CustomStringConvertible` 을 채택하면 객체자체를 프린트 하게되면 `description` 의 리턴값이 출력된다 



<br/>

<br/>

---

#### 

<br/>




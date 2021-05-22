---
layout: post
title: Today I Learned 📚
tags:
  - TIL
  - yagom-ios-camp-2nd
hero: https://source.unsplash.com/collection/4828371/
overlay: orange
published: true

---

{: .lead}
<!–-break-–>

# Today I Learned 🔥

## 2021.04.01 (목)

### 학습내용 📝

#### Associated Type

> An associated type gives a placeholder name to a type that is used as part of the protocol. The actual type to use for that associated type isn’t specified until the protocol is adopted.

- associated type 은 protocol 에서 사용될 임의의 타입이름을 주는 것

```swift
protocol FezzProtocol {
  	associatedtype MyType
  	var name: MyType { get }
}
```

- name 은 String 이지만, Int나 여러가지 타입형으로 될 수 있다면??? 이럴때 `Associated Type`을 사용한다.
- `Associated Type`은 원래 `typealias` 였지만, Swift 2.2 부터 `Associated Type` 키워드로 변경되었다.
- `Associated Type`은 `Type` 이다... name은 `MyType` 

```swift
struct Fezz: FezzProtocol {
  	var name: Int {
      	return 100
    }
}

struct Kane: FezzProtocol {
  	var name: String {
      	return "Kane"
    }
}
```

> https://zeddios.tistory.com/382


---

### 문제점 / 고민한 점 🤦🏼

- 계산기 .... 아이폰 계산기 앱은,, `명.품` 입니다.

```swift
2 + = = ...	// 2 등차 수열
2 * = = ...	// 2 등비 수열
2 + 2 * = =	...	// 6 부터 2씩 등비 수열
2 + 2 + = =	...	// 8 부터 4씩 등차 수열
2 + 2 * 2 + = =	...	// 12 부터 6씩 등차 수열
2 + 2 * 2 * = =	...	// 18 부터 6씩 등비 수열 
2 * 2 + = = ...	// 4부터 4씩 등차 수열

2 + 2 * 2 *		// 2 * 2 중간 연산 4 출력
2 + 2 * 2 +		// 높음 -> 낮음 6 출력

2 + 3 = + 3 =		// 5 -> 5 + 3 = 8 
```




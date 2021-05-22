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


# Today I Learned 🔥

## 2021.04.08 (목)

### 학습내용 📝

#### Result Type

##### 기존 오류처리 방식 **(do - try - catch - throw)**



```swift
enum MyError: Error {
   case some
   case unknown
}

func doSomething() throws {
   throw MyError.some
}

do {
   try doSomething()
} catch let error as MyError {
   switch error {
   case .some:
      print("someError")
   case .unknown:
      print("criticalError")
   }
} catch {
   print(error.localizedDescription)
}
```



##### 단점

- `throws` 코드 블록에서 에러를 던질 수 있다는 걸 나타내지만 **에러의 형식은 특정할 수 없음**
- `catch`로 올 때 실제 에러가 아닌 에러 프로토콜 형식으로 전달되는데, 이 때 **모호함이 발생함**
- 에러를 처리하기 위해서는 어떤 형식의 에러를 던지는지 파악한 후 해당 형식으로 `타입캐스팅`을 해야함
- 새로운 에러 형식이 추가되어도 컴파일러는 인지할 수 없음 (새로운 에러에 대한 처리가 없으면 경우에 따라 `런타임 에러`의 위험성이 생김)

---



##### Result

- 제네릭 타입으로 선언되어 있다.
  - 제네릭으로 선언되었다는 것은 형식이 명확하다는 것을 의미한다. 형식에 관한 모호함이 사라지게 되는 것 
  - Result는 성공과 실패 2가지가 존재한다. **Success**에는 작업의 결과가 저장되고, **Failure**에는 에러가 저장

```swift
public enum Result<Success, Failure> where Failure : Error
```

- 첫 번째 방법 (throwing function)

```swift
enum NumberError: Error {
   case negativeNumber
   case evenNumber
}

func isOddNumber(number: Int) throws -> Int {
   guard number >= 0 else {
      throw NumberError.negativeNumber
   }

   guard !number.isMultiple(of: 2) else {
      throw NumberError.evenNumber
   }

   return number * 2
}

let result = Result {
   try isOddNumber(number: 1)
}

switch result {
case .success(let data):
   print(data)
case .failure(let error):
   print(error.localizedDescription)    
}
```

- `isOddNumber` 메소드에서 음수, 2의 배수가 아닌 수를 `guard` 로 오류를 던져준다.
- `isOddNumber`는 `result` 상수에서 클로져를 통해 호출한다.
- `result`의 타입은 `Result`으로 success, failure를 가지고 있다 



- 두 번째 방법 (**Result** 반환)

```swift
func isOddNumber(number: Int) -> Result<Int, NumberError> { // 반환 타입을 잘 보자 !
   guard number >= 0 else {
      return Result.failure(NumberError.negativeNumber)
   }

   guard !number.isMultiple(of: 2) else {
      return .failure(.evenNumber) 
   }

   return .success(oddNumber * 2)
}

let result = isOddNumber(number: 1) 

switch result {
case .success(let data):
    print(data)
case .failure(let error):
    print(error.localizedDescription)
}
```

- 작업이 성공하면 `Int`가 리턴되고 실패하면 `NumberError`가 리턴되는 것을 명확히 알 수 있도록 함수의 리턴 형식이 변경되었다. 
  - 에러 형식을 직접 선언하기 때문에 형식 안정성이 보장
- 잘못된 형식으로 인해 발생하는 문제는 `컴파일 단계`에서 확인된다.



에러를 처리하는 시점이 `함수를 호출하는 시점`에서 `작업 결과를 사용하는 시점`으로 이동한 것을 알 수 있다. 이것을 **Delayed Error Handling** 이라고 부른다.



- 작업을 성공한 경우만 고려한다면, **get**을 활용하여 아래와 같이 더욱 간단하게 사용 가능하다.

```swift
if let successResult = try? result.get() {
    print(successResult)
}
```

---

#### 정리

- `throwing function`은 정확히 어떤 에러 형식을 던지는지 파악하기 어렵다
- `컴파일 타임`에 에러 형식을 정확히 인식할 수 있다는 것은 형식 안정성이 보장된다는 뜻 이다.



##### **Result Type을 활용하면,**

- 에러 형식이 명시적으로 선언된다
- 타입 캐스팅 없이 에러 처리가 가능하다.
- 형식 추론을 통해 에러 처리 코드가 단순해진다.
- 작업의 결과를 성공과 실패로 명확히 구분 가능하다.
- get 메소드로 에러 처리 코드를 더욱 단순하게 구현 가능하다.
- 기존 에러 처리 패턴을 완전히 대체하는 것이 아니라 에러를 처리하는 방식이 다양해진 것이다.



> 출처 : https://onelife2live.tistory.com/1



---

### 문제점 / 고민한 점 🤦🏼 / 해결방법 🙋🏼

프로젝트를 진행할 때 반환 타입이 존재하는데 `throw`는 사용하기 애매할 때 오류처리를 어떻게 해줘야 될 지 고민이 많았다.

추후 프로젝트를 진행할때 오류처리는 `Result`로 구현해보면서 익숙해져 보려고 한다!


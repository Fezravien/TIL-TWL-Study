---
layout: post
title: Today I Learned 📚
tags:
  - TIL
  - yagom-ios-camp-2nd
hero: https://source.unsplash.com/collection/4409024/
overlay: orange
published: true

---

{: .lead}
<!–-break-–>

# Today I Learned 🔥

## 2021.03.14 (일) 🗓

### 학습내용 📝

#### private vs final

##### Increasing Performance by Reducing Dynamic Dispatch

- 다른 언어와 마찬가지로 Swift도 SuperClass에 선언된 메소드와 프로퍼티 선언을 override 할 수 있다.

  - 프로그램이 런타임에 어떤 메소드와 프로퍼티를 참조할지 결정하고, `indirect call`(간접 호출), `indirect access`(간접 접근)을 수행해야 한다.

  - 이것을 `dynamic dispatch` 이라 불리며, `indirect call`(간접 호출) / `indirect access`(간접 접근)을 사용할때마다 `런타임 오버헤드` 비용을 증가시킨다.

    - 성능에 민감한 코드에서는 오버헤드는 바람직하지 못하다

       

  *다이나믹함을 제거함으로써 성능을 향상시키는 3가지 방법*

  - `final`
  - `private`
  - `모듈 최적화`

---



```swift
class ParticleModel {
	var point = ( 0.0, 0.0 )
	var velocity = 100.0

	func updatePoint(newPoint: (Double, Double), newVelocity: Double) {
		point = newPoint
		velocity = newVelocity
	}

	func update(newP: (Double, Double), newV: Double) {
		updatePoint(newP, newVelocity: newV)
	}
}

var p = ParticleModel()
for i in stride(from: 0.0, through: 360, by: 1.0) {
	p.update((i * sin(i), i), newV:i*1000)
}
```

위 코드를 보면 컴파일러는 동적으로 호출한다.

1. p의 update 호출
2. p의 updatePoint 호출
3. p의 point 튜플 속성에 접근
4. p의 velocity 속성에 접근

- ParticleModel의 서브 클래스들이 메소드와 프로퍼티를 `오버라이딩`을 할 수 있기 때문에 동적으로 호출된다.
- Swift에서 `동적인 호출`은 메서드 테이블에서 찾고 간접 호출을 수행한다.
  - 직접 호출에 비해서 느리다.
  - 많은 컴파일러의 최적화를 막아 훨씬 더 많은 비용이 든다.



**1. 오버라이딩 할 필요없는 속성은 final을 사용하자!**

- `final`은 클래스의 메서드, 프로퍼티가 `오버라이드` 할 수 없도록 하는 키워드이다.

  - 컴파일러가 `동적`인 `간접 호출`, `간접 접근`을 생략할 수 있게한다.

  ```swift
  // 프로퍼티와 메소드에 final
  class ParticleModel {
  	final var point = ( x: 0.0, y: 0.0 )
  	final var velocity = 100.0
  
  	final func updatePoint(newPoint: (Double, Double), newVelocity: Double) {
  		point = newPoint
  		velocity = newVelocity
  	}
  
  	func update(newP: (Double, Double), newV: Double) {
  		updatePoint(newP, newVelocity: newV)
  	}
  }
  
  // 클래스 자체에 final
  final class ParticleModel {
  	var point = ( x: 0.0, y: 0.0 )
  	var velocity = 100.0
  	// ...
  }
  ```



**2. private 키워드를 사용하면 한 파일에서만 참조되는 final 선언임을 추론할 수 있다!**

- `private` 키워드를 선언부에 작성하면 현재 파일에만 선언이 노출되도록 제한한다.

- 컴파일러가 모든 잠재적인 `오버라이딩 선언`을 찾을 수 있도록 한다.

- 오버라이딩 선언이 없으면 컴파일러는 자동으로 `final` 키워드를 추론하고 메소드와 프로퍼티 접근에 대한 `간접 호출`, `간접 접근`을 제거한다.

  ```swift
  // 프로퍼티와 메소드에 private
  class ParticleModel {
  	private var point = ( x: 0.0, y: 0.0 )
  	private var velocity = 100.0
  
  	private func updatePoint(newPoint: (Double, Double), newVelocity: Double) {
  		point = newPoint
  		velocity = newVelocity
  	}
  
  	func update(newP: (Double, Double), newV: Double) {
  		updatePoint(newP, newVelocity: newV)
  	}
  }
  
  // class에 private
  private class ParticleModel {
  	var point = ( x: 0.0, y: 0.0 )
  	var velocity = 100.0
  	// ...
  }
  ```

  

**3. internal 선언을 final로 추론할 수 있는 전체 모듈 최적화를 사용하자!**

- `internal` 접근자(default)는 선언된 모듈 내에서만 볼 수 있다. 

- Swift는 일반적으로 모듈을 구성하는 파일들을 개별적으로 컴파일하기 때문에 컴파일러는 `internal` 선언이 다른 파일에서 오버라이딩 되었는지 알 수 없다.

  - 전체 `모듈 최적화` 옵션을 활성화하면 모든 모듈이 동시에 컴파일된다. -> 전체 모듈에 대해 컴파일러가 추론이 가능하게 되어 오버라이딩 되지 않은 internal을 final로 `추론`할 수 있게된다.

  ```swift
  public class ParticleModel {
  	var point = ( x: 0.0, y: 0.0 )
  	var velocity = 100.0
  
  	func updatePoint(newPoint: (Double, Double), newVelocity: Double) {
  		point = newPoint
  		velocity = newVelocity
  	}
  
  	public func update(newP: (Double, Double), newV: Double) {
  		updatePoint(newP, newVelocity: newV)
  	}
  }
  
  var p = ParticleModel()
  for i in stride(from: 0.0, through: times, by: 1.0) {
  	p.update((i * sin(i), i), newV:i*1000)
  }
  ```

  모듈 최적화 옵션을 활성화하고 이 코드를 컴파일하면, 컴파일러는 point, velocity, updatePoint를 final로 추론할 수 있다. 반면에 update는 public 접근자를 갖기 때문에 final로 추론이 안된다.



**정리**

- 접근 제어자를 잘써야 성능이 좋아진다 !
  - private, final ....
- 컴파일러가 추론 가능하게 해줘도 된다

> 출처 : https://developer.apple.com/swift/blog/?id=27





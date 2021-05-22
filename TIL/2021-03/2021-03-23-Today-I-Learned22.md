---
layout: post
title: Today I Learned 📚
tags:
  - TIL
  - yagom-ios-camp-2nd
hero: https://source.unsplash.com/collection/5058541/
overlay: orange
published: true

---

{: .lead}
<!–-break-–>


# Today I Learned 🔥

## 2021.03.23 (화)

### 학습내용 📝

계산기를 만들다 보니 연산자에 따른 우선순위 덕분에 복잡해졌다 ..

#### 연산자 우선순위(https://developer.apple.com/documentation/swift/swift_standard_library/operator_declarations)

| Operator               | Description                     | Associativity     | Precedence group               |
| :--------------------- | :------------------------------ | :---------------- | :----------------------------- |
| `<<`                   | Bitwise left shift              | None              | `BitwiseShiftPrecedence`       |
| `>>`                   | Bitwise right shift             | None              | `BitwiseShiftPrecedence`       |
| `*`                    | Multiply                        | Left associative  | `MultiplicationPrecedence`     |
| `/`                    | Divide                          | Left associative  | `MultiplicationPrecedence`     |
| `%`                    | Remainder                       | Left associative  | `MultiplicationPrecedence`     |
| `&*`                   | Multiply, ignoring overflow     | Left associative  | `MultiplicationPrecedence`     |
| `&`                    | Bitwise AND                     | Left associative  | `MultiplicationPrecedence`     |
| `+`                    | Add                             | Left associative  | `AdditionPrecedence`           |
| `-`                    | Subtract                        | Left associative  | `AdditionPrecedence`           |
| `&+`                   | Add with overflow               | Left associative  | `AdditionPrecedence`           |
| `&-`                   | Subtract with overflow          | Left associative  | `AdditionPrecedence`           |
| `|`                    | Bitwise OR                      | Left associative  | `AdditionPrecedence`           |
| `^`                    | Bitwise XOR                     | Left associative  | `AdditionPrecedence`           |
| `..<`                  | Half-open range                 | None              | `RangeFormationPrecedence`     |
| `...`                  | Closed range                    | None              | `RangeFormationPrecedence`     |
| `is`                   | Type check                      | Left associative  | `CastingPrecedence`            |
| `as`, `as?`, and `as!` | Type cast                       | Left associative  | `CastingPrecedence`            |
| `??`                   | Nil coalescing                  | Right associative | `NilCoalescingPrecedence`      |
| `<`                    | Less than                       | None              | `ComparisonPrecedence`         |
| `<=`                   | Less than or equal              | None              | `ComparisonPrecedence`         |
| `>`                    | Greater than                    | None              | `ComparisonPrecedence`         |
| `>=`                   | Greater than or equal           | None              | `ComparisonPrecedence`         |
| `==`                   | Equal                           | None              | `ComparisonPrecedence`         |
| `!=`                   | Not equal                       | None              | `ComparisonPrecedence`         |
| `===`                  | Identical                       | None              | `ComparisonPrecedence`         |
| `!==`                  | Not identical                   | None              | `ComparisonPrecedence`         |
| ~=                     | Pattern match                   | None              | `ComparisonPrecedence`         |
| `.==`                  | Pointwise equal                 | None              | `ComparisonPrecedence`         |
| `.!=`                  | Pointwise not equal             | None              | `ComparisonPrecedence`         |
| `.<`                   | Pointwise less than             | None              | `ComparisonPrecedence`         |
| `.<=`                  | Pointwise less than or equal    | None              | `ComparisonPrecedence`         |
| `.>`                   | Pointwise greater than          | None              | `ComparisonPrecedence`         |
| `.>=`                  | Pointwise greater than or equal | None              | `ComparisonPrecedence`         |
| `&&`                   | Logical AND                     | Left associative  | `LogicalConjunctionPrecedence` |
| `||`                   | Logical OR                      | Left associative  | `LogicalDisjunctionPrecedence` |
| `?``:`                 | Ternary conditional             | Right associative | `TernaryPrecedence`            |
| `=`                    | Assign                          | Right associative | `AssignmentPrecedence`         |
| `*=`                   | Multiply and assign             | Right associative | `AssignmentPrecedence`         |
| `/=`                   | Divide and assign               | Right associative | `AssignmentPrecedence`         |
| `%=`                   | Remainder and assign            | Right associative | `AssignmentPrecedence`         |
| `+=`                   | Add and assign                  | Right associative | `AssignmentPrecedence`         |
| `-=`                   | Subtract and assign             | Right associative | `AssignmentPrecedence`         |
| `<<=`                  | Left bit shift and assign       | Right associative | `AssignmentPrecedence`         |
| `>>=`                  | Right bit shift and assign      | Right associative | `AssignmentPrecedence`         |
| `&=`                   | Bitwise AND and assign          | Right associative | `AssignmentPrecedence`         |
| `|=`                   | Bitwise OR and assign           | Right associative | `AssignmentPrecedence`         |
| `^=`                   | Bitwise XOR and assign          | Right associative | `AssignmentPrecedence`         |

---

### 문제점 / 고민한 점 🤦🏼

- ~ (not) 비트 연산자를 2진수에 어떻게 적용하지?

```swift
let a = "10110"
let b = Int(a, radix: 2)!
let c = ~b
print(c)
let d = String(c, radix: 2)
print(d)

// -23
// -10111
```

- 후위 연산자에서 중간에 어떻게 우선순위에 따라 연산해서 보여줄 수 있을까?

---

### 해결방법 🙋🏼

- 타입을 고쳐보자 !

```swift
let a = "00010110"
let b = UInt8(a, radix: 2)!
let c = ~b
print(c)
let d = String(c, radix: 2)
print(d)

// 233
// 11101001
```



- 음,,, 맞을까?

<img width="1400" alt="image" src="https://user-images.githubusercontent.com/44525561/112180822-3b42e480-8c3f-11eb-96b7-2cd69db6ea1e.png">
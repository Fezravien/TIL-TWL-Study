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

## 2021.04.02 (목)

### 학습내용 📝

- 계산기 로직 다시짜보자 !!!


---

### 문제점 / 고민한 점 🤦🏼/ 해결방법 🙋🏼

- 이게 맞는지는 모르겠지만 ,, 경우의 수를 정말 잘 !!!! 나눠야 겠다 ......

```swift
private func decideCalculatePriority() -> StatusByPriority {
        if equalStack.isEmpty == false { // "=" 입력됨
            if operandStack.count == 1 && lowOperatorStack.count + highOperatorStack.count == 1 {

                if lowOperatorStack.isEmpty == true { // *, / 

                } else { // +, - 
                  
                }

            } else if operandStack.count == 2 && lowOperatorStack.count + highOperatorStack.count == 2 {

            } else if operandStack.count == 2 && lowOperatorStack.count + highOperatorStack.count == 1 {

                if lowOperatorStack.isEmpty == true {

                } else {

                }
            }
            return .calculation
        } else { // 2 + 3 +, 2 + 3 + ...
            if operandStack.count == 3 && lowOperatorStack.count + highOperatorStack.count == 3 { 
                if lowOperatorStack.count > highOperatorStack.count {

                } else {

                }

            } else if operandStack.count == 2 && lowOperatorStack.count == 2 || highOperatorStack.count == 2 { 
  
            } else if operandStack.count == 2 && lowOperatorStack.count + highOperatorStack.count == 2 {

            }
        }
        return .hold
    }
```


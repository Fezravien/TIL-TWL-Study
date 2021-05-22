---
layout: post
title: Today I Learned 📚
tags:
  - til
  - yagom-ios-camp-2nd

hero: https://source.unsplash.com/collection/4828371/
overlay: orange
published: true

---
{: .lead}
<!–-break-–>


# Today I Learned 🔥

## 2021.05.05 (수)

### 학습내용

#### 세마포어

- 은행원이 동시다발적으로 본사에 심사를 요청해서 어떤것이 먼저 본사의 일 처리 순번에 들어가지?

![image-20210505214427004](https://raw.githubusercontent.com/Fezravien/UploadForMarkdown/forUpload/img/image-20210505214427004.png)

세마포어를 통해 한번에 하나만 접근할 수 있도록 `thread-safe` 를 생각해봤다 



#### 실패할 수 있는 이니셜라이저

- 초기화 구문에서 옵셔널을 풀어줘야되는 일이 발생했다.

```swift
init?() {
    guard let credit = CreditRating.allCases.shuffled().first,
          let work = WorkType.allCases.shuffled().first else {
            
        return nil
    }
}

이는 초기화 과정에서도 옵셔널을 푸는 과정에 실패가 있을 수 있으므로 `실패할 수 있는 초기화`를 써줌으로 해결할 수 있었다.


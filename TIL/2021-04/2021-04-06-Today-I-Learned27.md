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

## 2021.04.05 (월)

### 학습내용 📝

#### Managing the View Hierarchy

##### bringSubviewToFront

<img src="https://t1.daumcdn.net/cfile/tistory/999C56475DADA9CF37" alt="img" style="zoom:60%;" /> <img src="https://t1.daumcdn.net/cfile/tistory/99E067405DADAA2106" alt="img" style="zoom:60%;" />

```swift
self.myView.bringSubviewToFront(self.brownView)
```

myView 에서 brownView를 맨 앞으로 가져온다 !



##### sendSubviewToBack

 <img src="https://t1.daumcdn.net/cfile/tistory/999F7F405DADAD6903" alt="img" style="zoom:70%;" /><img src="https://t1.daumcdn.net/cfile/tistory/99958E385DADAC5E36" alt="img" style="zoom:50%;" />

```swift
self.myView.sendSubviewToBack(self.orangeView)
```

myView 에서 orangeView를 맨 뒤로 보낸다 !!



> 출처 : https://zeddios.tistory.com/832

<br/>

---

### 문제점 / 고민한 점 🤦🏼/ 해결방법 🙋🏼

<img width="500" alt="스크린샷 2021-04-07 오전 12 36 18" src="https://user-images.githubusercontent.com/44525561/113742981-1de14080-973e-11eb-98b0-8ed577df36c7.png"><img width="500" alt="스크린샷 2021-04-07 오전 12 36 36" src="https://user-images.githubusercontent.com/44525561/113742951-1752c900-973e-11eb-9129-87b562944d7b.png">

위쪽 이미지를 보면 뷰가 겹쳐보이는 문제가 있었다. 

뷰의 계층이 왼쪽은 전체에 가장 위쪽에 존재해서 이런 문제가 발생했다.

```swift
backgroundImage.alpha = 0.15
self.view.sendSubviewToBack(backgroundImage)
```






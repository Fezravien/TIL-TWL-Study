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

## 2021.04.29 (목)

### 학습내용 📝

#### completionBlock

<img src="https://tva1.sinaimg.cn/large/008i3skNgy1gq11zqmbmmj31h20ggq5q.jpg" alt="스크린샷 2021-04-30 오전 12.54.31" style="zoom:40%;" />

내가 생각한 그림도 하나의 `task`와 `task`가 끝날때 호출되는 `completionBlock`이 묶여서 호출될 것이라 생각했다.

<br/>

<img src="https://tva1.sinaimg.cn/large/008i3skNgy1gq11zrafyaj31h00p07ay.jpg" alt="스크린샷 2021-04-30 오전 12.54.41" style="zoom:40%;" />

 하지만 앨런의 얘기를 들어보니 같은 객체라 보면 안되며 completionBlock는 알려만 줄뿐 순서를 보장하지 못했다.

간헐적으로 비동기라 생각했었지만, 그것 보다 순서자체가 뒤바뀌는 상황이 벌어졌다.

<br/>

<img src="https://tva1.sinaimg.cn/large/008i3skNgy1gq11zsbeptj31gk0tcwmf.jpg" alt="스크린샷 2021-04-30 오전 12.54.51" style="zoom:40%;" />

- waitUntilAllOperationsAreFinished(), waitUtilFinished()

큐를 기다리는 메소드, 오퍼레이션을 기다리는 메소드 어떻게 돌아가길래 ??

아무튼 waitUntilAllOperationsAreFinished 은 메인에서 사용하게 되면 차단이 일어나서 절대로 쓰면 안된다!!!!

 

> 출처 : 앨런
>
> Thank you 앨런 !!



<br/>

---

### 문제점 / 고민한 점 🤦🏼/ 해결방법 🙋🏼

- James 와 고민 

<img src="https://tva1.sinaimg.cn/large/008i3skNgy1gq11ztgrvoj31d90u07da.jpg" alt="스크린샷 2021-04-29 오후 9.04.28" style="zoom:30%;" />

이런 느낌적인 느낌인가???? 

실시간 적으로 고객을 받았을 때 어떻게 우선순위를 부여해야 될지 .... 
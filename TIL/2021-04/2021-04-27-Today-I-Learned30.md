---
layout: post
title: Today I Learned 📚
tags:
  - TIL
  - yagom-ios-camp-2nd
hero: https://source.unsplash.com/collection/3728885/
overlay: orange
published: true

---

{: .lead}
<!–-break-–>


# Today I Learned 🔥

## 2021.04.27 (화)

### 학습내용 📝

#### 성장하는 iOS 개발자 되기 세미나 

![스크린샷 2021-04-27 오후 4.04.09](https://tva1.sinaimg.cn/large/008i3skNgy1gpyr2jsifkj32ci0tkdli.jpg)

![스크린샷 2021-04-27 오후 4.05.48](https://tva1.sinaimg.cn/large/008i3skNgy1gpyr2oc21uj31r60ncdky.jpg)

![스크린샷 2021-04-27 오후 4.06.08](https://tva1.sinaimg.cn/large/008i3skNgy1gpyr2qcdyyj31d20n0wid.jpg)

![스크린샷 2021-04-27 오후 4.06.33](https://tva1.sinaimg.cn/large/008i3skNgy1gpyr2rtme4j31940pijun.jpg)

![스크린샷 2021-04-27 오후 4.08.32](https://tva1.sinaimg.cn/large/008i3skNgy1gpyr2tsqjlj31k40u0qal.jpg)

![스크린샷 2021-04-27 오후 4.09.19](https://tva1.sinaimg.cn/large/008i3skNgy1gpyr3bxs0dj31o10u0tb8.jpg)

![스크린샷 2021-04-27 오후 4.13.49](https://tva1.sinaimg.cn/large/008i3skNgy1gpyr3fob1vj31rg0u0dlq.jpg)

![스크린샷 2021-04-27 오후 4.15.42](https://tva1.sinaimg.cn/large/008i3skNgy1gpyr754w2sj320a0u07co.jpg)

![스크린샷 2021-04-27 오후 4.17.02](https://tva1.sinaimg.cn/large/008i3skNgy1gpyr73gj0sj324p0u0qb1.jpg)

![스크린샷 2021-04-27 오후 4.17.47](https://tva1.sinaimg.cn/large/008i3skNgy1gpyr7ffxk8j31mz0u0dqu.jpg)

![스크린샷 2021-04-27 오후 4.18.21](https://tva1.sinaimg.cn/large/008i3skNgy1gpyr7nx1tvj31pt0u0gzi.jpg)

![스크린샷 2021-04-27 오후 4.18.54](https://tva1.sinaimg.cn/large/008i3skNgy1gpyr7wq55ej31y70u0wma.jpg)

![스크린샷 2021-04-27 오후 4.19.53](https://tva1.sinaimg.cn/large/008i3skNgy1gpyr84fs6pj31ko0u07m9.jpg)

![스크린샷 2021-04-27 오후 4.21.09](https://tva1.sinaimg.cn/large/008i3skNgy1gpyr8ebfxbj31o70u0n65.jpg)



<br/>

---

### 문제점 / 고민한 점 🤦🏼/ 해결방법 🙋🏼

1. n명의 은행원이란?

- 은행원의 수 == 스레드

[![image](https://user-images.githubusercontent.com/44525561/116269226-01727a00-a7b9-11eb-9916-65b2bd122118.png)](https://user-images.githubusercontent.com/44525561/116269226-01727a00-a7b9-11eb-9916-65b2bd122118.png)

- n명의 은행원을 스레드로 보고 `maxConcurrentOperationCount = n` 로 지정하는 방식





- 은행원의 수 == 큐의 갯수

[![image](https://user-images.githubusercontent.com/44525561/116269432-2ebf2800-a7b9-11eb-8351-4c1a67a847fd.png)](https://user-images.githubusercontent.com/44525561/116269432-2ebf2800-a7b9-11eb-8351-4c1a67a847fd.png)

- n명의 은행원을 큐로 보고 각각의 큐마다 라벨링하는 방식

큐 자체를 창구로 보고 각각의 스레드를 1개로 지정해서 동기적으로 수행하는 방법을 생각했어요. 
---
layout: post
title: Today I Learned 📚
tags:
  - til
  - yagom-ios-camp-2nd

hero: https://source.unsplash.com/collection/2229334/
overlay: orange
published: true

---
{: .lead}
<!–-break-–>


# Today I Learned 🔥

## 2021.05.07 (금)

### 학습내용

#### iOS App Life Cycle 

 App은 상태에 변화에 맞춰 대응하도록 해야된다 !

##### foreground

- 사용자에게 보이는 부분으로, CPU를 포함한 시스템 자원에서 높은 우선순위를 가지게 된다.

##### background

- 사용자에게 보이지 않는 부분으로 새로운 작업을 수행하지 않고 유지를 하거나 우선수위에 밀리게 되면 종료하게 될 수 있다.

---



##### Scene

![스크린샷 2021-05-07 오후 4.45.12](https://raw.githubusercontent.com/Fezravien/UploadForMarkdown/forUpload/img/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-05-07%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%204.45.12.png)

공식문서의 정의를 읽어보면 **“App의 UI 인스턴스를 동시에 여러개 다루고, 자원을 UI 인스턴스에 적절하게 적용해준다”** 라고…. 가 맞겟죠?



##### AppDelegate는 뭐하고 있지?

- 중앙 데이터 구조 초기화
- `scene` 구성(설정)
- App 밖에서 발생한 이벤트 처리 (배터리, 다운로드 - 알림)
- App의 `scene`, `view`, `viewController`에 한정되지 않고 App 스스로를 타겟하는 이벤트 처리
- 푸쉬 알림과 같은 App 초기에 요구되는 모든 서비스를 등록



##### `AppDelegate` 클래스

- Xcode에서 프로젝트를 생성할 때 마다 자동으로 생성
- 특별한 경우를 제외하고 App을 초기화하고 App 수준의 이벤트에 대응하기 위해서는 `AppDelegate` 클래스를 사용해야한다.



##### UISceneDelegate는 뭐하고 있지?

`UISceneDelegete`는 `protocol`이며, `scene`에서 발생하는 life-cycle 이벤트에 반응하기 위해서 사용하는 메소드이다.



##### `SceneDelegate` 클래스

- Xcode에서 프로젝트를 생성할 때 마다 자동으로 생성
- 내부에는 `scene`의 상태들에 관한 메소드들을 가지고 있다.

> 자세한 내용은 블로그에 정리했습니다 
>
> https://fezravien.github.io/posts/ios4

---



#### UnitTest

##### Test Doubles

Unit Test를 작성하는 동안 production에 사용될 객체와 동일하게 동작하지만 단순화된 버전이 필요한 경우가 있고,  이런 종류의 객체들을 `Test Double` 이라고 한다. 

외부 의존성은 Test Doubles를 통해 관리되며 다양한 시나리오를 쉽게 시뮬레이션할 수 있다

Test Double은 테스트 목적으로 production 객체를 교체하는 모든 객체를 부르는 모든 용어를 말한다. 

그리고 이러한 Test Double에는 다섯 가지 종류가 있다



- Dummy
- Fake
- Stub
- Mock
- Spy


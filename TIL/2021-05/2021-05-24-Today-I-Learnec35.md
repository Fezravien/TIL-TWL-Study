

# Today I Learned 🔥

### 2021.05.24 (월)

## 학습내용

### 키체인이란 무엇일까?

- 사용자의 앱, 서버 및 웹 사이트 계정과 암호 및 신용 카드 번호 또는 은행 계좌 PIN 번호와 같은 중요 정보를 암호화하여 안전하게 저장
- 웹 사이트, 이메일 계정, 네트워크 서버 또는 기타 암호로 보호된 항목에 접근할 때 해당 암호를 키체인에 저장하면 해당 암호를 기억하거나 다시 입력할 필요가 없습니다.
- 앱을 삭제해도 키체인 정보는 남아있다.

Securely store small chunks of data on behalf of the user.

The keychain services API helps you solve this problem by giving your app a mechanism to store small bits of user data in an encrypted database called a keychain. When you securely remember the password for them, you free the user to choose a complicated one.

https://developer.apple.com/documentation/security/keychain_services

키 체인은 애플 계열의 운영체제에서 동작하는 다양한 응용 프로그램에서 비밀번호나 계정 등 보안이 필요한 요소를 저장하는 데 사용되는 암호화된 저장소이다. iOS뿐만 아니라 macOS, tvOS, watchOS 등에서도 모두 제공된다. 사용하는 곳이 생각보다 많아서, 아이클라우드의 로그인 정보가 키 체인을 통해 관리되고 있고, 와이파이의 패스워드도 키 체인에 저장되며, 사파리에서 웹사이트별 패스워드를 관리할 때에도 키 체인이 사용된다.

<br/>

### 키 체인의 특징

1. 기본적으로 애플리케이션은 자기 자신의 키 체인에만 접근할 수 있다.
2. iOS에서 키 체인의 위치는 샌드박스(외부에서 받은 파일을 바로 실행하지 않고 보호된 영역에서 실행시켜 봄으로써 잘못된 파일과 프로그램이 내부시스템 전체에 악영향을 주는 것을 미연에 방지하기는 기술) 외부이므로, 앱을 삭제해도 키 체인에 저장된 정보는 삭제되지 않는다.
3. 앱의 프로비저닝 파일을 이용해서 앱 간의 사용 경로를 구분하기 때문에, 동일한 앱이라도 프로비저닝 파일을 변경해서 빌드하면 기존 정보를 더 이상 조회할 수 없다.
4. 키 체인 그룹을 사용하여 서로 다른 앱에서도 저장된 데이터를 공유할 수 있다.
5. 비밀번호 또는 개인 키처럼 보호가 필요한 항목은 암호화되어 키 체인으로 보호되며, 인증서처럼 보호과 필요하지 않은 항목은 암화되지 않은 채로 저장된다.
6. 키 체인은 잠글 수 있어서, 일단 잠기면 해제하기 전까지 저장된 데이터에 접근할 수 없지만 iOS에서는 기기의 잠근이 해제되는 순간 키 체인의 잠금도 함께 해제된다.

<br/>

### Keyed Archiver, User Defaults, CoreData와 다른 점은 무엇일까?

#### Keyed Archiver

An encoder that stores an object’s data to an archive referenced by keys.

- https://developer.apple.com/documentation/foundation/nskeyedarchiver/
- 객체같은 사용자 정의 타입을 UserDefaults에 데이터의 형태로 저장
- NSCoding 프로토콜을 채택하고 NSKeyedArchiver, NSKeyedUnarchiver 인코딩/디코딩 하여 사용
- 앱을 삭제하면 함께 삭제됨
- 인스턴스의 정보를 시스템에 저장
- 딕셔너리와 같이 key-value 쌍으로 저장하기 위해 썼던  클래스
- Objective-C에서 사용하기 위해 설계 되었지만 현재도 사용할 수 있음.
- Serialization - 인스턴스를 파일 형태로 저장하기 위한 클래스
- key-value 형태로 아카이빙
- 암호화 지원하지 않음



#### UserDefaults

An interface to the user’s defaults database, where you store key-value pairs persistently across launches of your app.

- https://developer.apple.com/documentation/foundation/userdefaults/
- 앱 이용자의 환경설정 등 키-값 형태로 저장해둘 수 있다.
- 주로 단일 데이터인 값을 저장
- 앱 삭제 전까지 유지
- key-value 쌍으로 저장
- 앱 전역적으로 사용하는 가벼운 저장소
- 암호화 지원하지 않음



#### CoreData

Persist or cache data on a single device, or sync data to multiple devices with CloudKit.

- https://developer.apple.com/documentation/coredata/

- 복잡하고 큰 데이터를 저장

- 앱이 많은 데이터를 필요로 하고 여러 다른 객체 간의 관계를 관리하고 객체에 빠르고 쉽게 접근해야한다면 CoreData 를 사용하는 것이 좋다.

- CoreData의 역할

  - Persistence - 데이터 지속 관리
  - Undo and Redo of individual or Batched Changes - 데이터 변경사항에 대한 실행취소/재실행 기능
    - 코어데이터의 변경 사항을 추적하여 이에 대한 취소작업이 가능
  - Background Data Tasks - 백그라운드 상의 데이터 작업 지원
  - View Synchronization - 뷰 동기화
    - 테이블뷰/ 컬렉션뷰 등의 UI에게 섹션, 행, 열 아이템을 관리해주는 DataSource를 제공하여 뷰와 데이터가 동기화 되도록 함
  - Versioning and Migration - 버전 관리 및 데이터 이전 기능
  - 오프라인 활용
  - undo, redo 이용

  <br/>

### iOS의 키체인과 macOS의 키체인의 차이는?

#### macOS

- 사용자나 애플리케이션은 원하는 만큼 키 체인을 만들 수 있다.
- iOS와 달리 분리해서 사용 가능



#### iOS

- 모든 앱에서 사용할 수 있는 하나의 키 체인만 제공한다.
- 키체인 저장소를 분리해서 쓰기보다 사용자가 공통으로 사용하는 키체인 하나만 사용 가능



#### iCloud

- 사용자가 디바이스에서 아이클라우드 계정에 로그인하면 시스템의 논리적으로 구분되는 아이클라우드용 키 체인을 제공한다.

<br/>

### 키체인 서비스를 사용하기 위해 k- 접두어를 사용하는 여러 타입과 값을 사용합니다

#### k- 접두어의 비밀은?

상수의 의미로 표현되는것 (변하지 않는 값) https://green1229.tistory.com/56

https://developer.apple.com/library/archive/documentation/CoreFoundation/Conceptual/CFDesignConcepts/Articles/NamingConventions.html#//apple_ref/doc/uid/20001110-CJBEJBHH

Core Foundation 등의 Core Framework 헤더파일들을 보면, 헝가리언 네이밍 규칙을 따른 흔적들을 제법 볼 수 있다. 일단 'k' 는 헝가리언 네이밍에 따라 사용된 걸로 보인다. Constants 의 'c' 는 이미 헝가리안에서 'char' 의 'c' 로 예약이 되어 있는 상황이니 중복을 피하기 위해 동일한 발음기호인 'k' 를 사용한 것으로 추측된다. Core Foundation 의 역사를 고려하면 헝가리언 네이밍을 따른것이 어느정도 이해가 된다.

https://metalkin.tistory.com/20



#### 어떤 프레임워크의 값일까?

CoreFoundation

<img src="https://raw.githubusercontent.com/Fezravien/UploadForMarkdown/forUpload/img/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-05-25%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%202.42.50.png" alt="스크린샷 2021-05-25 오전 2.42.50" style="zoom: 67%;" />

#### 그 프레임워크와 Foundation 프레임워크와의 차이는?

##### CoreFoundation

- C로 구현
- Foundation 구현을 위해 일부 사용됨
- Core- 접두어가 붙은 프레임워크 구현에 일부 사용됨

<img src="https://raw.githubusercontent.com/Fezravien/UploadForMarkdown/forUpload/img/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-05-25%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%202.43.21.png" alt="스크린샷 2021-05-25 오전 2.43.21" style="zoom:67%;" />

##### Foundation

- Objective-C, Swift로 구현

<img src="https://raw.githubusercontent.com/Fezravien/UploadForMarkdown/forUpload/img/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-05-25%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%202.44.13.png" alt="스크린샷 2021-05-25 오전 2.44.13" style="zoom: 67%;" />

<br/>

### 키체인은 언제 사용하면 좋을까?

- 로그인 비밀번호
- 결제 데이터
- 암호화를 위한 키
---
layout: post
title: Today I Learned 📚
tags:
  - TIL
  - yagom-ios-camp-2nd
hero: https://source.unsplash.com/collection/14233285/
overlay: orange
published: true

---

{: .lead}
<!–-break-–>


# Today I Learned 🔥

## 2021.04.05 (월)

### 학습내용 📝

#### UITableView

##### 단일 열에 배열된 행을 사용하여 데이터를 표시하는 뷰 !

```swift
class UITableView : UIScrollView
```

##### iOS의 테이블 뷰에는 세로 스크롤 콘텐츠의 단일 열이 행으로 구분되어 표시된다

- 테이블의 각 행에는 하나의 앱 콘텐츠가 포함한다.
- 테이블을 구성하여 행의 긴 단일 목록을 표시하거나, 관련 행을 섹션으로 그룹화하여 콘텐츠를 보다 쉽게 탐색할 수 있다.

<img src="https://docs-assets.developer.apple.com/published/722508d93c/1eb44f8d-1907-4949-9208-f2fb7f3ffd1b.png" alt="Illustration showing the Contacts app and Settings app. The Contacts app uses a table to organize the user's individual contacts in a scrolling list. The Settings app displays different groups of settings in a scrolling list." style="zoom:60%;" />

##### 테이블은 일반적으로 데이터가 고도로 구조화되거나 계층적으로 구성된 앱에서 사용된다.

- 계층 데이터가 포함된 앱은 내비게이션 컨트롤러와 함께 테이블을 사용하는 경우가 많으므로 계층 구조의 여러 수준 간에 쉽게 탐색할 수 있다. 
- UITableView는 테이블의 기본 모양을 관리하지만 앱은 실제 콘텐츠를 표시하는 셀(UITableViewCell 개체)을 제공힌디.
  - 표준 셀 구성은 텍스트와 이미지의 간단한 조합을 표시하지만 원하는 내용을 표시하는 사용자 정의 셀을 정의할 수 있습니다. 

<br/>

##### Adding a Table View to Your Interface

- 인터페이스에 테이블 뷰를 추가하려면 테이블 뷰 컨트롤러(UITableViewController) 개체를 스토리보드로 끌어다 놓는다.
- 테이블 뷰는 일반적으로 제공하는 데이터 개체에서 데이터를 가져와 보여준다.
- 데이터 개체는 앱의 데이터를 관리하고 테이블의 셀을 만들고 구성하는 역할을 합한다. 
  - 테이블의 내용이 변경되지 않는 경우 대신 스토리보드 파일에서 해당 내용을 구성할 수 있다.



https://developer.apple.com/documentation/uikit/uitableview

---

### 문제점 / 고민한 점 🤦🏼

- 만국박람회 [Step 1]을 진행하면서 Codable을 이용해서 데이터 타입을 만들고 파싱이 잘되는지 확인하고 싶었다.

  ```swift
  let expoJson = """ 
  {
    // expo json 
  }
  """
  
  let decoder = JSONDecoder()
  let jsonData = expoJson.data(using: .utf8)!
  let result = try decoder.decode(Expo.self, from: jsonData)
  print(result)
  
  ```

  - decoder.decode() 부분에서 오류가 발생 **"The given data was not valid JSON."**	????????? 

  

---

### 해결방법 🙋🏼

- 문자열 데이터 중 개행( `\n`)을 전부 지우니 오류없지 정상적으로 파싱이 가능했다.
  1. 개행 문자를 `\\n` 로 변환
  2. 개행 부분을 기억하고 강제로 줄바꿈 

다음 스텝에서 직접 해보면서 해결방법을 사용을 해봐야겠다 ! 






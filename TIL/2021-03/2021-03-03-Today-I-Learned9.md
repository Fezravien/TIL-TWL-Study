---
layout: post
title: Today I Learned 📚
tags:
  - til
  - yagom-ios-camp-2nd

hero: https://source.unsplash.com/collection/11663747/
overlay: orange
published: true

---

{: .lead}
<!–-break-–>

# Today I Learned 🔥



## 2021.03.03 (수) 🗓



### 학습내용 📝

#### 글쓰기 강의 (IT 서적 편집자로 일하고 계신 이중민님의 특강)

- 먼저 전체 주제와 관련된 제목을 정하고 무엇을 설명할지 요약글 작성
  - 만약 작성하기가 어렵다면 본문 애용을 먼저 작성한 후 마지막에 정리
  - **코드나 명령어를 먼저 나열해보자**
- 코드를 중심으로 주제를 나눈다
  - 코드에서 설명해야할 클래스, 메소드, 문법, 예제 코드 설명 등을 중심으로 나눈다.
- 해당 부분의 연관성을 전제로 설명하는 글을 쓴다.
  - 부가적인 설명을 진행할 때는 표, 목록, 블록 인용 문자 등을 활용

---

- **블로그 글 쓰기의 포인트 1**

  - 특정 주제를 잡고 연재 형식으로 꾸준히 쓰는 방법
  - 내 공부 기록을 꾸준히 남기는 방식
  - 누군가에게 보여주는 글인가? 내가 참고하는 글인가?를 미리 생각해두면 좋다.

  

- **블로그 글 쓰기의 포인드 2**

  - 가능하면 경어체로 작성하는 것이 좋다.
  - 부연 설명할 다른 사람의 글 혹은 내 글을 미리 챙겨두면 좋다.
  - 특정 주제와 관련해 연재 형식으로 꾸준히 쓰는 방법이 좋다(검색 최적화에 유리).
  - 카테고리 기반으로 정리하면 좋다.

  

- **블로그 글 쓰기의 포인트 3**

  - 어투는 큰 상관없다.
  - 내가 알아볼만한 중요한 포인트를 잡고 쓰는 것이 좋다.
  - 내 공부 기록을 꾸준히 남기는 방식이 좋다.
  - 태그 기반으로 정리하는 것이 좋다.

  ---

#### RockScissorsPaperGame Project

- 구조체

  - static

  ```swift
  struct Hand {
      static let rock = HandShape.rock.rawValue
      static let scissors = HandShape.scissors.rawValue
      static let paper = HandShape.paper.rawValue
  }
  struct GameResult {
      static let win = UserSideGameResult.win.rawValue
      static let lose = UserSideGameResult.lose.rawValue
      static let draw = UserSideGameResult.draw.rawValue
  }
  struct GameConditions {
      static let endGame = GameStatus.endGameValue.rawValue
      static let initValue = GameStatus.initHandValue.rawValue
      static let userSelectWinRockScissors = UserResultSituation.SelectWinRockScissors.rawValue
      static let userSelectWinScissors = UserResultSituation.SelectWinScissors.rawValue
      static let userSelectLoseScissorsRock = UserResultSituation.SelectLoseScissorsRock.rawValue
      static let userSelectLosePaper = UserResultSituation.SelectLosePaper.rawValue
      static let userSelectDraw = UserResultSituation.SelectDraw.rawValue
  }
  ```

  > struct 가 로직에 도움이 되지 않는데 가독성 있게 쓰려고 ... 필요 이상의 짓을 하고 있는게 아닌가 생각이 듭니다 ㅠ
  >
  > 추후에 활용법을 좀더 강구해봐야 될 것 같습니다 🤔

- 열거형

  - Error 

  ```swift
  enum GameRestart: Error {
      case inputValue
      case beginAgain
  }
  ```

  

  - CaseIterable (allCases)

  ```swift
  enum HandShape: Int, CaseIterable {
      case rock = 1, scissors = 2, paper = 3
  }
  
  print(HandShape.allCases)
  print(HandShape.allCases.map { $0.rawValue })
  
  for value in HandShape.allCases {
      print(value.rawValue)
  }
  
  ```

  






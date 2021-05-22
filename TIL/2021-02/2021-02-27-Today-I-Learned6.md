---
layout: post
title: Today I Learned 📚
tags:
  - til
  - yagom-ios-camp-2nd
hero: https://source.unsplash.com/collection/4585827/
overlay: orange
published: true

---

{: .lead}
<!–-break-–>

# Today I Learned 🔥

---

## 2021.02.27 (토)

---

### 학습내용

- 숫자야구게임 [STEP2] 에서 숫자의 중복을 확인하기 위해 contains -> set 

  - `Set`

    집합(Set) 은 같은 타입의 서로다른 값을 중복없이 저장하고자 할 때 사용하는 집단 자료형

    - **선언 및 초기화**

    ```swift
    // Type annotation 을 생략하게되면 Array로 선언되게 됨, 자동추론으로 Set<String>으로 선언 및 초기화됨
    var genres : Set = ["Classic","Rock", "Balad"]
    
    // 저장 타입을 생략하지 않고 초기화 한 경우
    var genres : Set<String> = ["Classic","Rock", "Balad"]
    
    // 빈 배열로 초기화 하는 경우 Type annotation 과 저장 타입을 반드시 명시해야한다.
    var g : Set<String> = []
    
    // Set객체를 통한 직접 정의
    var genres = Set<String>()
    
    ```

    - **출력해보기**

    ```swift
    var genres = Set<String>()
    
    genres.insert("Rock")
    genres.insert("Classic")
    genres.insert("Balad")
    
    for g in genres {
        print("\(g)")
    }
    
    print()
    
    for g in genres.sorted(){
        print("\(g)")
    }
    ```

    - **Set에서 지원하는 함수**

      - insert(_:): Set에 아이템을 추가합니다._

      - _remove(_:) : Set에 인자값에 해당하는 값을 삭제합니다.  

        > Set에 삭제할 값이 없으면 nil을 반환하고, 값이 있으면 삭제한 후 삭제한값을 반환합니다.

      - removeAll() : Set에 있는 모든 값을 제거합니다.

      - contains(_:) : 인자 값이 Set에 포함되어있으면 true, 없으면 false를 반환합니다.

      

      - **연산 함수**
        - intersection(_:) : 교집_
        - _symmetricDifference(_:) : A와 B의 합집합에서 둘의 교집합을 뺸 집합
        - union(_:) : 합집합_
        - _subtract(_:) : 차집합 [a.subtract(b) -> a-b]

      

      - **포함관계 연산 함수**

        - isSubset(of:) : [A.isSubset(of:B) : A가 B의 부분집합인지 -> true/false 반환]

        - isSuperset(of:) : [B.isSuperset(of:A) : B가 A의 상위 집합인지 -> true/false]

        - isStrictSubset(of:) : 같은 집합은 제외, 다음 예제를 통해 확인

        - isStrictSuperset(of:) : 같은 집합은 제외, 다음 예제를 통해 확인

        - isDisjoint(with:) : 두 집합 사이에 어떤 공통 값이 없을 때 true, 하나라도 있으면 false반환

          

        ```swift
        var a : Set = [1,3,5,7,9]
        var b : Set = [3,5]
        var c : Set = [3,5]
        var d : Set = [2,4,6]
        
        let isSubSet = b.isSubset(of: a)
        print("\(isSubSet)")
        
        let isSuperset = a.isSuperset(of: b)
        print("\(isSuperset)")
        
        //c 는 b의 부분집합이긴 하지만 같은 집합으로 판단해 false를 반환
        let cIsStrictSubSetOfb = c.isStrictSubset(of: b)
        print("\(cIsStrictSubSetOfb)")
        
        let cIsStrictSubSetOfa = c.isStrictSubset(of: a)
        print("\(cIsStrictSubSetOfa)")
        
        //c는 b의 상위 집합이긴 하지만 같은 집합으로 판단해 false를 반환
        let cIsStrictSuperSetOfb = c.isStrictSuperset(of: b)
        print("\(cIsStrictSuperSetOfb)")
        
        let aIsStrictSuperSetOfc = a.isStrictSuperset(of: c)
        print("\(aIsStrictSuperSetOfc)")
        ```

---


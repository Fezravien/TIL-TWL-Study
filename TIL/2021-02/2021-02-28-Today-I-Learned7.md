---
layout: post
title: Today I Learned 📚
tags:
  - til
  - yagom-ios-camp-2nd
hero: https://source.unsplash.com/collection/14233285/
overlay: orange
published: true

---

{: .lead}
<!–-break-–>

# Today I Learned 🔥

---

## 2021.02.28 (일)

---

### 학습내용

- 한 주동안 나를 괴롭게 했던 git에 대해 다시한번 복습

  #### 브랜치 병합하기 !

  - **Merge vs Rebase**

    두개의 브랜치가 존재하는 상황에서 하나의 브랜치에서 다른 브랜치로 합치게 되는 경우 Git에서는 일반적으로 두 가지 방법이 있습니다.

    ```markdown
    1. Merge
    2. Rebase
    ```

    자주 사용하는 Merge에 비해 Rebase는 생소할 수 있습니다.

    

    Merge의 경우 히스토리에 작업한 내용의 사실을 기록합니다. Merge로 브랜치를 병합하게되면 커밋 내역에 Merge commit이 추가로 남게 됩니다.

    하지만 Rebase의 경우 브랜치를 병합할 때 Merge commit을 남기지 않으므로, 마치 다른 브랜치는 없었던 것처럼 프로젝트의 작업 내용이 하나의 흐름으로 유지됩니다.

    

    브랜치를 합칠 때 `Merge`를 써야 하는지 `Rebase`를 써야 하는지에 대해서는 정답이 없습니다. 프로젝트나 팀의 상황에 따라 다른 전략을 사용할 수 있습니다. 다만, 로컬에서는 히스토리 정리를 위해 Rebase를 할 수도 있지만 이미 원격 저장소에 `Push`된 커밋은 `Rebase`를 하지 않는 것이 일반적입니다.

    

    #### 원격저장소로 부터 내용가지고 오기 !

  -  **Pull vs Fetch**

    Git에서 원격저장소에 있는 내용을 로컬저장소로 가져올 떄 두가지 방법이 있습니다.

    ```markdown
    1. pull 
    2. fetch 
    ```

    두 가지 모두 원격 저장소로부터 내용을 가지고 온다는 점에서 기능은 유사하지만 차이점이 존재합니다.

    - 원격저장소로 부터 내용을 가지고 온 후 `병합의 유무`

    `pull`을 사용하게 되면 바로 병합을 같이 진행하게 되지만, `fetch`를 사용하면 병합을 수동으로 해줘야합니다. 이렇게 함으로 병합 전, 원격 저장소와 로컬 저장소의 코드이 차이점을 비교한 후 문제가 있는지 없는지 체크 해 볼 수 있습니다. 즉, **조심스럽게** 라고 말할 수 있습니다.

    

  #### GIt 되돌리기 !

  - **Reset vs Revert**
    - Reset

  reset은 특정 사건으로 되돌아가게 되는데 과거로 되돌아 갔으니 해당 사건 이후의 사건들은 모두 사라지게 됩니다. 

  ```bash
  $ git reset <옵션> <돌아가고 싶은 커밋 ID>
  
  $ git reset --soft abcdef
  $ git reset --mixed abcdef  # (옵션 작성안할 시 기본값)
  $ git reset --hard abcdef 
  $ git reset HEAD~10 # (현재부터 10개 이전으로 복원)
  ```

  - soft : index 보존(add한 상태, staged 상태), 워킹 디렉터리의 파일 보존. 즉 모두 보존.
  - mixed : index 취소(add하기 전 상태, unstaged 상태), 워킹 디렉터리의 파일 보존 (기본 옵션)
  - hard : index 취소(add하기 전 상태, unstaged 상태), 워킹 디렉터리의 파일 삭제. 즉 모두 취소.

  hard는 가장 깔끔하지만 해당 커밋 이후의 작업들이 모두 사라지므로 확신이 있을때만 신중하게 사용해야합니다.

  mixed의 경우 soft와 달리 워킹 디렉토리는 유지되지만, index가 취소되므로 취소된 파일들을 다시 add 해줘야합니다.

  

  - Revert

  특정 사건을 골라서 없던일로 만듭니다. 또한 과거 특정 사건을 없애주지만 revert를 했다는 이력이 남게됩니다.

  그리고 없앨려 하는 특정 사건의 과거와 미래가 얽혀 충돌이 나는 경우가 잦습니다.

  ```sh
  $ git rever <돌아가고 싶은 커밋 ID> 
  ```

  



---

> 출처 
>
>  https://velog.io/@godori/Git-Rebase
>
> https://lsh424.tistory.com/22
>
> https://git-scm.com/book/ko/v2/Git-
# Today I Learned 🔥

🗓 21.08.11 



### **오늘** **뭐** **했지** ⁉️

- Stream Chat 프로젝트 진행하기
  - 서버와 연결 (송신, 수신)
  - 메인 페이지 구성 (UI, 키보드)

<br>

### **오늘의** **삽질** ⏳



![Simulator Screen Recording - iPhone 12 Pro Max - 2021-08-11 at 23.25.16](https://raw.githubusercontent.com/Fezravien/UploadForMarkdown/forUpload/img/Simulator%20Screen%20Recording%20-%20iPhone%2012%20Pro%20Max%20-%202021-08-11%20at%2023.25.16.gif)

키보드에서 올라올 때 TextField의 높이에 따라 애니메이션 작업하기 !!

```swift
private var chatUserNameTextFieldConstraint: NSLayoutConstraint!

private func setChatUsernametextField() {
	self.view.addSubview(chatUsernameTextField)
	self.chatUserNameTextFieldConstraint = self.chatUsernameTextField.bottomAnchor.constraint(equalTo: self.view.safeAreaLayoutGuide.bottomAnchor, constant: -220)
    
	NSLayoutConstraint.activate([
		self.chatUserNameTextFieldConstraint,
		self.chatUsernameTextField.centerXAnchor.constraint(equalTo:
                                                         self.chatLogoImageView.centerXAnchor),
		self.chatUsernameTextField.widthAnchor.constraint(equalTo:
                                                      self.chatLogoImageView.widthAnchor, multiplier: 3/7, constant: 15)
        ])
    }

    @objc func keyboardWillShow(notification: NSNotification) {
        guard let userInfo = notification.userInfo,
              let endFrameValue = (userInfo[UIResponder.keyboardFrameEndUserInfoKey] as? NSValue) else {
            
            return
        }
        
        NSLayoutConstraint.deactivate([ self.chatUserNameTextFieldConstraint ])
        
        let endFrame = endFrameValue.cgRectValue
        self.chatUserNameTextFieldConstraint = self.chatUsernameTextField.bottomAnchor.constraint(equalTo: self.view.bottomAnchor,
                                                                                          constant: -(endFrame.size.height + self.chatUsernameTextField.frame.height * 2))
        NSLayoutConstraint.activate([ self.chatUserNameTextFieldConstraint ])
        
        UIView.animate(withDuration: 0.25) {
            self.view.layoutIfNeeded()
        }
    }
    
    @objc func keyboardWillHide(notification: NSNotification) {
        NSLayoutConstraint.deactivate([ self.chatUserNameTextFieldConstraint ])
        self.chatUserNameTextFieldConstraint = self.chatUsernameTextField.bottomAnchor.constraint(equalTo: self.view.bottomAnchor,
                                                                                          constant: -220)
        NSLayoutConstraint.activate([ self.chatUserNameTextFieldConstraint ])

        UIView.animate(withDuration: 0.25) {
            self.view.layoutIfNeeded()
        }
    }
```

뭔가 지금 코드 블럭이 이상한데... 어쩄든 

기존에 Point 를 바꾸는 방식에서 레이아웃을 수정하고 그것을 업데이트하면서 애니메이션을 동작하도록 했음..

참... 스와이프 구현하면서는 결국에는 못했었는데 다시 해보니 어느정도 이해가 가는것 같다 !!

해결 방법은 

레이아웃 변수 (NSLayoutConstraint) 타입으로 유동적인 레이아웃을 만들고 이벤트에 변화에 따라 `deactivate`, `activate` 해주면서 레이아웃을 정리하고! 그 다음이 중요해 `self.view.layoutIfNeeded()` 이것들 통해서 레이아웃을 **즉시!**업데이트 해주는거지 

<br>

**오늘의** **느낀점** 😎

계속 잡고 있는다고 해결될 문제였으면 진즉이 해결했겠지?... 좀 더 여유롭게 문제를 해결해보려고 해보자 !!

그리고... **애니메이션 재밌네 !!** 😃 
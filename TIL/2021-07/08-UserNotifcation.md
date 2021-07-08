# Today I Learned 🔥

### 21.07.08 🗓

<br>

## **오늘** **뭐** **했지** ⁉️

오늘은 목요일 활동학습하는 날!

오늘의 주제는 `User Notification`

### **User Notifications**

> Push user-facing notifications to the user’s device from a server, or generate them locally from your app.

서버에서 사용자를 대상으로 하는 알림을 device로 보내거나, 혹은 앱에서 로컬로 알림을 보낸다

#### **Overview**

> User-facing notifications communicate important information to users of your app, regardless of whether your app is running on the user’s device. For example, a sports app can let the user know when their favorite team scores. Notifications can also tell your app to download information and update its interface. Notifications can display an alert, play a sound, or badge the app’s icon.

사용자 대면 notifications은 앱이 사용자의 기기에서 실행중인지 여부에 관계없이 앱 사용자에게 중요한 정보를 전달합니다. 예를 들어, 스포츠 앱은 그들이 가장 좋아하는 팀이 득점을 할 때 사용자에게 알려줄 수 있습니다. Notifications은 또한 앱에 정보를 다운로드 하고 인터페이스를 업데이트하도록 지시할 수 있습니다. Notifications은 alert를 표시하거나, 소리를 재생하거나, 앱 아이콘에 배지를 표시할 수 있습니다.

<img src="https://raw.githubusercontent.com/Fezravien/UploadForMarkdown/forUpload/img/_2021-07-07__11.59.56.png" alt="_2021-07-07__11.59.56" style="zoom:70%;" />

> You can generate notifications locally from your app or remotely from a server that you manage. For *local notifications*, the app creates the notification content and specifies a condition, like a time or location, that triggers the delivery of the notification. For *remote notifications*, your company’s server generates push notifications, and **`Apple Push Notification service (APNs)`** handles the delivery of those notifications to the user’s devices.

우리는 notifications를 앱으로부터 로컬로 생성할 수도 있으며, 서버에서 원격으로 생성하게도 할 수 있습니다. 로컬 notification의 경우, 앱은 notification 내용을 생성하고 notification 발송의 트리거가 될 만한 시간, 지역, 조건 등을 지정합니다. 원격 Notifications의 경우에는, 회사 서버에서 notification을 보냅니다. 그러고 나면 `Apple Push Notifications Service`가 사용자의 기기에서 해당 notification의 전송에 대해서 다룹니다.

<br>

Use this framework to do the following:

- Define the types of notifications that your app supports.
- Define any custom actions associated with your notification types.
- Schedule local notifications for delivery.
- Process already delivered notifications.
- Respond to user-selected actions.

아래를 따르기 위해서는 다음 프레임워크를 사용하십쇼

- 앱에서 지원하는 알림 유형을 정의합니다
- notification의 유형과 관련된 사용자 지정 작업을 정의한다
- 전송할 로컬 notification를 예약한다
- 이미 전달된 notification을 처리한다
- 유저가 선택한 행위에 대해서 응답한다

> The system makes every attempt to deliver local and remote notifications in a timely manner, but delivery isn’t guaranteed. The PushKit framework offers a more timely delivery mechanism for specific types of notifications, such as those VoIP and watchOS complications use. For more information, see [PushKit](https://developer.apple.com/documentation/pushkit).

시스템은 모든 로컬 및 원격 notifications를 제 시간에 보내기 위해서 노력한다. 하지만, 항상 notifications를 보장할 수는 없다. `PushKit` framework는 VoIP 및 Watch와 같은 특정 유형의 알림에 대한 보다 시기 적절한 전달 메커니즘을 제공한다.

<br>

### Scheduling a Notification Locally from Your App

>  Create and schedule notifications from your app when you want to get the user’s attention.

유저의 관심, 이목을 끌고 싶을 때, 앱으로부터 notification을 생성하거나 예약한다

<br>

#### **Overview**

> Use local notifications to get the user’s attention. You can display an alert, play a sound, or badge your app’s icon. For example, a background app could ask the system to display an alert when your app finishes a particular task. Always use local notifications to convey important information that the user wants.

로컬 notification을 사용하여 사용자의 주의를 끌 수 있다. Alert를 화면에 띄우거나, 소리를 재생시키거나, 혹은 app 아이콘에 뱃지를 띄운다. 예를들어, 백그라운드 앱의 경우 특정 작업이 끝날 때 alert를 화면에 띄우는 것을 시스템에 요청할 수 있습니다. 로컬 Notification의 경우 항상 사용자가 원하는 중요한 정보를 전달하도록 한다.

> The system handles delivery of notifications based on a time or location that you specify. If the delivery of the notification occurs when your app isn’t running or in the background, the system interacts with the user for you. If your app is in the foreground, the system delivers the notification to your app for handling.

시스템은 사용자가 지정한 시간 또는 위치를 기준으로 Notification 전송을 처리한다. 만약에 앱이 실행중이지 않거나 백그라운드에서 작동하고 있을 때 Notification이 전송되면 시스템이 사용자와 상호작용한다. 만약에 app이 전면에서 작동하고 있는 foreground 상태이면, system은 앱에 알림을 전송하여 처리한다.

<br>

#### **Create the Notification's Content**

> Fill in the properties of a `NSMutableNotificationContent` object with the details of your notification. The fields you fill in define how the system delivers your notification. For example, to play a sound, assign a value to the `[sound](<https://developer.apple.com/documentation/usernotifications/unnotificationcontent/1649871-sound>)` property of the object. [Listing 1](https://developer.apple.com/documentation/usernotifications/scheduling_a_notification_locally_from_your_app#2980225) shows a content object that displays an alert containing a title string and body text. You can specify multiple types of interaction in the same request.

notification의 상세 내용을 `NSMutableNotificationContent` 객체에 채우세요. 채우는 fields들은 시스템에서 notification을 전송하는 방법을 정의하게 될 것이다. 예를들어, 소리를 재생시키기 위해서는, 해당 객체의 `sound` 프로퍼티에 값을 할당해주면 된다. 아래를 보면 title, content 텍스트가 포함된 alert를 표시하는 `content` 객체가 있다. 동일한 요청에 대해서 여러 유형의 interaction을 지정할 수 있게 된다.

**Listing 1** Configuring the notification content

```swift
let content = NSMutableNotificationContent()
content.title = "Weekly Staff Meeting"
content.body = "Every Tuesday at 2pm"
```

<br>

#### **Specify the Conditions for Delivery**

> Specify the conditions for delivering your notification using a `UNCalendarNotificaitonTrigger`, `[UNTimeIntervalNotificationTrigger](<https://developer.apple.com/documentation/usernotifications/untimeintervalnotificationtrigger>)`, or `[UNLocationNotificationTrigger](<https://developer.apple.com/documentation/usernotifications/unlocationnotificationtrigger>)` object. Each trigger object requires different parameters. For example, a calendar-based trigger requires you to specify the date and time of delivery.

`UNCalendarNotificaitonTrigger`, `[UNTimeIntervalNotificationTrigger](<https://developer.apple.com/documentation/usernotifications/untimeintervalnotificationtrigger>)` ,  `[UNLocationNotificationTrigger](<https://developer.apple.com/documentation/usernotifications/unlocationnotificationtrigger>)` 와 같은 객체들을 활용해서 notification 전달 조건에 대해서 명시합니다. 각각의 object trigger는 다른 매개변수들을 요구한다. 예를들어, calendar을 기초로 하는 trigger의 경우는 전송 날짜, 시간에 대한 명시를 요구한다.

> [Listing 2](https://developer.apple.com/documentation/usernotifications/scheduling_a_notification_locally_from_your_app#2980231) shows you how to configure a notification for the system to deliver every Tuesday at 2pm. The `[DateComponents](<https://developer.apple.com/documentation/foundation/datecomponents>)` structure specifies the timing for the event. Configuring the trigger with the `repeats` parameter set to `true` causes the system to reschedule the event after its delivery.

아래 코드를 보면, 우리는 매주 화요일 오후 두시에 notification이 전송되도록 설정되어 있는 것을 볼 수 있다. `DateComponents` structure는 이벤트의 타이밍을 명시하고 있다. 그리고 `repeats` 매개변수를 통해 해당 전송이 반복될 것인지에 대해서도 설정한다

**Listing 2** Configuring a recurring date-based trigger

```swift
var dateComponents = DateComponents()
dateComponents.calendar = Calendar.current

dateComponents.weekday = 3 //Tuesday
dateComponents.hour = 14 // 14:00

let trigger = UNCalendarNotificationTrigger(dateMatching: dateComponents, repeats: true)
```

<br>

#### **Create and Register a Notification Request**

> Create a `UNNotificationRequest` object that includes your content and trigger conditions, and call the `[add(_:withCompletionHandler:)](<https://developer.apple.com/documentation/usernotifications/unusernotificationcenter/1649508-add>)` method to schedule your request with the system. [Listing 3](https://developer.apple.com/documentation/usernotifications/scheduling_a_notification_locally_from_your_app#2980221) shows an example that uses the content from [Listing 1](https://developer.apple.com/documentation/usernotifications/scheduling_a_notification_locally_from_your_app#2980225) and [Listing 2](https://developer.apple.com/documentation/usernotifications/scheduling_a_notification_locally_from_your_app#2980231) to fill in the request object.

trigger 조건과 content를 포함하고 있는 `UNNotificationRequest` 객체를 생성하고, 요청을 예약하는`[add(_:withCompletionHandler:)](<https://developer.apple.com/documentation/usernotifications/unusernotificationcenter/1649508-add>)` 메서드를 호출한다. 아래의 코드는 위 코드들을 활용해서 `UNNotificationRequest` 를 통해 request를 예약하는 것을 볼 수 있다.

**Listing 3** Registering the notification request

```swift
let uuidString = UUID().uuidString
let request = UNNotificationRequest(identifier: uuidString, content: content, trigger: trigger)

let notificationCenter = UNUserNotificationCenter.current()
notificationCenter.add(request) { (error) in
	if error != nil {
		//Error handling
	}
}
```

- uuid를 통해서 notificaiton에 id를 부여해주는 것 같다

<br>

#### **Cancel a Scheduled Notification Request**

> Once scheduled, a notification request remains active until its trigger condition is met, or you explicitly cancel it. Typically, you cancel a request when conditions change and you no longer need to notify the user. For example, if the user completes a reminder, you’d cancel any active requests associated with that reminder. To cancel an active notification request, call the `removePendingNotificationRequests(withIdentifiers:)` method of `UNUserNotificationCenter`.

예약된 notification 요청은 trigger의 조건을 만날때까지 혹은 취소될 때까지 계속해서 active 상태를 유지하고 있다. 일반적으로는 조건이 변경되거나 더 이상 유저에게 notification을 알리지 않아도될 때 request를 취소한다. 예를들어, 사용자가 미리 Notification의 reminder(?)를 완성(?), 성공(?)한다면, 이 reminder와 연관된 요청을 취소해야한다. 이 active상태의 notification을 취소시키기 위해서는, `UNUserNotificationCenter` 객체의`removePendingNotificationRequests(withIdentifiers:)` 메서드를 호출하면 된다.


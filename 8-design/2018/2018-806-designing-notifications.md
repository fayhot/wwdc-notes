# [2018 806 Designing Notifications](https://developer.apple.com/videos/play/wwdc2018/806/)

806-designing-notifications.md

Heena Ko

iOS|Feature
---|---
3|Pop up
4|.
?|Notification Center
?|Rich Notificaion
iOS 12 | Group


Topic|Speaker|Time
---|---|---
First run|Jon Dascola
Provide value|Jon Dascola
Notification Grouping|Jon Dascola|1910
Richer Rich Notifications|Heena Ko|


## First run

Direct to Notification Center

Social News Game

Route|Conditions
---|---
New|Passive consumption. Noncritical response.
Traditional Route|Timely delivery. Urgent response.

### Asking for Permission

- Do not prompt on first launch
- Explain why notifications are valuable
- Present at a relevant moment


## Provide value

Attention is valuable.

Send great content.

Notifications aren’t reasons to launch into an app.

Considered delivery.

- x / meditation / CNN / Duolingo

Smart customization.

- Settings / ESPN / New York Times


## Notification Grouping


### Create notification threads.

```swift
// Creating groups with thread identifiers
let content = UNMutableNotificationContent()
content.title = "Notifications Team"
content.body = "WWDC After Party!"
content.threadIdentifier = "notifications-team-chat"

// Yes, this is a code slide in a design presentation.
😎
```
- News app / Podcast 

It’s ok to group by app.


## Richer Rich Notifications

---

First Run

- Timely delivery and urgent response
- Passive content and noncritical response
- Make decision based on your app’s needs

Provide Value

- Meaningful content with specific information
- Not a reason to launch the app
- Well designed Settings and configuration UI

Notification Grouping

- By default notifications will group by app
- Threads can be used to create more nuanced grouping
- Use threads only when necessary

Rich Notifications

- Each notification should complete a specific task
- Add images, video, audio, and custom content
- Add interactivity to create a holistic notification experience


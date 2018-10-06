--
title: Notification Center
category: ios
---

```swift
  NotificationCenter.default.addObserver(self, selector: #selector(triggeredNotice(_:)), name: NSNotification.Name("Notificacion"), object: nil)
```

```swift
  NotificationCenter.default.post(name: NSNotification.Name("Notificacion"), object: nil)
```

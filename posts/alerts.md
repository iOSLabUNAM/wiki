---
title: UIAlertController
category: ios
---

# UIAlertController

- **actionSheet** An action sheet displayed in the context of the view controller that presented it.
- **case alert** An alert displayed modally for the app.

```swift
func tapSimpleAlert(_ sender: Any) {
    print("Simple Alert")
    let alert = UIAlertController(title: "Simple Alert", message: "lipsum", preferredStyle: .actionSheet)
    self.present(alert, animated: true, completion: nil)
}

@objc func tapOkAlert(_ sender: Any) {
    print("Ok Alert")
    let alert = UIAlertController(title: "Ok Alert", message: "lipsum", preferredStyle: .alert)
    let okAction = UIAlertAction(title: "Ok", style: .default) { action in
        debugPrint(action)
    }
    alert.addAction(okAction)
    self.present(alert, animated: true, completion: nil)
}

func tapOkCancelAlert(_ sender: Any) {
    print("Ok Cancel Alert")
    let alert = UIAlertController(title: "Ok Cancel Alert", message: "lipsum", preferredStyle: .alert)
    let okAction = UIAlertAction(title: "Ok", style: .default) { action in
        debugPrint(action)
    }
    alert.addAction(okAction)
    let cancelAction = UIAlertAction(title: "Cancel", style: .cancel) { action in
        debugPrint(action)
    }
    alert.addAction(cancelAction)
    self.present(alert, animated: true, completion: nil)
}
```

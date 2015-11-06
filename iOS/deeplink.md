## deeplink

### safari브라우저에서 deeplink를 연결하기

앱이 실행 중인 상태가 아닐 때는 launchOptions에 `UIApplicationLaunchOptionsURLKey` 값으로 전달된다.

```swift
func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

        if let checkedLaunchOptions = launchOptions {
            if let URL = checkedLaunchOptions[UIApplicationLaunchOptionsURLKey] as? NSURL {

            }
        }
        return true
    }
```

전달받은 NSURL값으로 openURL메소드를 실행하면 될 거라 생각했는데 안됨. (수정 개발 진행 중)

```swift
func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

        if let checkedLaunchOptions = launchOptions {
            if let URL = checkedLaunchOptions[UIApplicationLaunchOptionsURLKey] as? NSURL {
				// 처리가 안됨.
                if UIApplication.sharedApplication().canOpenURL(URL) {
                    UIApplication.sharedApplication().openURL(URL)
                }
            }
        }
        return true
    }
```



### push 수신

앱이 실행 중이 아닌 경우 `UIApplicationLaunchOptionsRemoteNotificationKey` 값으로 `application:didReceiveRemoteNotification` method로 전달한다.

```swift
func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

        if let checkedLaunchOptions = launchOptions {
            if let notificationPayload: NSDictionary = checkedLaunchOptions[UIApplicationLaunchOptionsRemoteNotificationKey] as? NSDictionary {

                let mNotificationUserInfo: NSMutableDictionary = NSMutableDictionary(dictionary: notificationPayload)
                mNotificationUserInfo["appLauch"] = "true"
                self.application(application, didReceiveRemoteNotification: mNotificationUserInfo as [NSObject : AnyObject])
            }
        }
        return true
    }
```
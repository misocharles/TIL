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

### freeze 현상

```swift
                    if UIApplication.sharedApplication().canOpenURL(NSURL(string: urlString)!) {
                        dispatch_async(dispatch_get_main_queue()) {
                            UIApplication.sharedApplication().openURL(NSURL(string: urlString)!)
                        }
                    }
```


`openURL:` 실행시 freeze 현상이 발생하여 main_queue 스레드로 비동기처리를 하여 해결하였다. 그런데 새로 배포한 앱에서 다시 freeze 현상이 발생한다. 

#### 해결책

- OS 특성을 타는 것인지 확인해보는 중이다.
- openURL 이 아닌 내부 method 를 새로 분리하는 법



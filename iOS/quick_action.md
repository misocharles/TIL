# Home screen quick action

## 종류

- Static quick action
- Dynamic quick action

## Static quick action

### Property List

Info.plist에 UIApplicationShortcutItems (Array) Key를 추가한다. 아직 Xcode name은 없다.

#### Xcode property list editor:

![Info.plist](https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/InfoPlistKeyReference/Art/UIApplicationShortcutItems_plist_editor_2x.png)

#### XML 

```xml
<key>UIApplicationShortcutItems</key>
    <array>
        <dict>
            <key>UIApplicationShortcutItemIconFile</key>
            <string>open-favorites</string>
            <key>UIApplicationShortcutItemTitle</key>
            <string>Favorites</string>
            <key>UIApplicationShortcutItemType</key>
            <string>com.mycompany.myapp.openfavorites</string>
            <key>UIApplicationShortcutItemUserInfo</key>
            <dict>
                <key>key1</key>
                <string>value1</string>
            </dict>
        </dict>
        <dict>
            <key>UIApplicationShortcutItemIconType</key>
            <string>UIApplicationShortcutIconTypeCompose</string>
            <key>UIApplicationShortcutItemTitle</key>
            <string>New Message</string>
            <key>UIApplicationShortcutItemType</key>
            <string>com.mycompany.myapp.newmessage</string>
            <key>UIApplicationShortcutItemUserInfo</key>
            <dict>
                <key>key2</key>
                <string>value2</string>
            </dict>
        </dict>
    </array>
```

Home screen quick action 을 선택하면, delegate의 [application:performActionForShortcutItem:completionHandler:](https://developer.apple.com/library/prerelease/ios/documentation/UIKit/Reference/UIApplicationDelegate_Protocol/index.html#//apple_ref/occ/intfm/UIApplicationDelegate/application:performActionForShortcutItem:completionHandler:) 를 호출한다.

```swift
    @available(iOS 9.0, *)
    func application(application: UIApplication, performActionForShortcutItem shortcutItem: UIApplicationShortcutItem, completionHandler: (Bool) -> Void) {
        
        println(shortcutItem)
        if shortcutItem.type == "com.mycompany.myapp.openfavorites" {
            println("com.mycompany.myapp.openfavorites")
            
        }
    }

```

## Dynamic quick action


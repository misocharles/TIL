# Home screen quick action

## 종류

- Static quick action
- Dynamic quick action

## Static quick action

### Property List

Info.plist에 UIApplicationShortcutItems (Array) Key를 추가한다. 아직 Xcode name은 없다.

```
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


## google-cast-sdk를 설치하다가 생긴 에러 메시지 해결

```bash
$ pod install

[!] The `Application [Debug]` target overrides the `EMBEDDED_CONTENT_CONTAINS_SWIFT` build setting defined in `Pods/Target Support Files/Pods/Pods.debug.xcconfig'. This can lead to problems with the CocoaPods installation
    - Use the `$(inherited)` flag, or
    - Remove the build settings from the target.

[!] The `Application [Release]` target overrides the `EMBEDDED_CONTENT_CONTAINS_SWIFT` build setting defined in `Pods/Target Support Files/Pods/Pods.release.xcconfig'. This can lead to problems with the CocoaPods installation
    - Use the `$(inherited)` flag, or
    - Remove the build settings from the target.
```

Application의 Target 에 있는 EMBEDDED_CONTENT_CONTAINS_SWIFT 값을 $(inherited) 로 변경하면 해결된다. 

괜히 Pods 의 Target 정보를 수정한다고 고생했다. Project `Pods` 의 Build Settings 값으로 Pods.debug.xcconfig 와 Pods.release.xcconfig 파일들이 생성된다. 실제 Application 의 Build Settings 값들은 이 2개의 파일에서 가져오게 된다. 
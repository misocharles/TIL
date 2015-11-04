# Google Cast (iOS)

## Dependencies

- iOS Sender API library : can be downloaded here at: https://developers.google.com/cast/docs/downloads/

## Documentation

- Google Cast iOS Sender Overview: https://developers.google.com/cast/docs/ios_sender
- Google Cast iOS API Reference: https://developers.google.com/cast/docs/reference/ios/
- Google Cast Design Checklist http://developers.google.com/cast/docs/design_checklist

## Sample App (iOS)

### Reference apps

- [CastVideos-ios](https://github.com/googlecast/CastVideos-ios)	Design Checklist compliant iOS sender to Cast videos.

### Other sample apps

- [HelloText-ios](https://github.com/googlecast/CastHelloText-ios)	iOS sender application to send and receive text messages.
- [hello-cast-video-ios](https://github.com/googlecast/CastHelloVideo-ios)	Basic iOS sender application to cast a Video.
- [CastRemoteDisplay-iOS](https://github.com/googlecast/CastRemoteDisplay-iOS)	iOS sender on how to use the Remote Display API for iOS with Google Cast devices.

## [iOS App Development](https://developers.google.com/cast/docs/ios_sender)

### Library

- API 종류
	- iOS Sender API
	- Remote Display API (beta version)
	- Game Manager API

#### 직접 다운로드
- https://developers.google.com/cast/docs/developers 문서상에 다운로드 링크가 있다. 

#### Cocoapods

- The iOS SDK library is called `google-cast-sdk`.
- The Remote Display API library is called `google-cast-remote-display-sdk`.
- The Game Manager API library is called `google-cast-games-sdk`.

```
pod 'google-cast-sdk'
```

```bash
$ pod install
Installing google-cast-sdk (2.10.0)
```

### Xcode Setup

- In your Xcode project, set the Other Linker Flags to -ObjC.
![xcode_linker](https://developers.google.com/cast/images/xcode_linker.png)

- linked frameworkd libraries (not embedded). 새로 추가한 것만 체크함

    - [x] Accelerate.framework
    - [ ] AudioToolbox.framework
    - [ ] AVFoundation.framework
    - [x] CoreBluetooth.framework
    - [x] CoreText.framework
    - [ ] GoogleCast.framework - wait
    - [ ] libc++.dylib
    - [x] MediaAccessibility.framework
    - [ ] MediaPlayer.framework
    - [ ] SystemConfiguration.framework

	- GoogleCast.framework 는 `Link Binary With Libraries` 에서 추가할 수가 없었다. 일단 추가하지 않고 작업 진행
		- 여기서 추가 정보를 얻을 수 있을까? http://guides.cocoapods.org/using/using-cocoapods.html#what-is-happening-behind-the-scenes

- The Google Cast SDK does not support bitcode. In your Xcode project, go to **Build Settings > All** and set **Enable Bitcode** to **No**.

### Development

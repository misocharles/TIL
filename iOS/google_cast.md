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

- 특이사항: GoogleCast.framework 는 `Link Binary With Libraries` 에서 추가할 수 없었다. 일단 추가하지 않고 작업 진행
	- 여기서 추가 정보를 얻을 수 있을까? http://guides.cocoapods.org/using/using-cocoapods.html#what-is-happening-behind-the-scenes
	- 이 소스에서는 https://github.com/googlecast/CastHelloText-ios CocoaPods 사용에는 Library를 별도로 추가하지 않는데?

- The Google Cast SDK does not support bitcode. In your Xcode project, go to **Build Settings > All** and set **Enable Bitcode** to **No**.

### Development

구글 캐스트 SDK는 이벤트의 응용 프로그램을 통보하고 Cast 앱 생명주기(life cycle)의 다양한 상태 사이를 이동할 Delegate 패턴을 사용합니다.

#### 애플리케이션 흐름

다음 섹션은 Sender 애플리케이션 일반적인 실행 흐름의 세부 사항을 포함한다 :

- 장치 검색 Scan for devices
- 장치 선택 Select device
- 앱 실행 Launch application
- 미디어 채널 Work with media channels
- 미디어 호출 Load the media

#### 장치 검색

이 단계에서는 sender 애플리케이션은 Google Cast receiver 단말기에 대한 WiFi 네트워크를 찾는다. 장치 스캐너와 delegate를 인스턴스화하고 검색을 시작하는 것을 포함한다. (This involves instantiating a device scanner, a delegate, and starting the scan.) 스캐너가 장치를 발견했을 때, delegate를 통해 애플리케이션에 통보한다.




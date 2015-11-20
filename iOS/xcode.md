# Xcode plugin

Xcode plugin 을 편하게 관리하기 위해 package manager를 먼저 설치한다.

## [Alcatraz](http://alcatraz.io)

스크립트가 변경될 수 있으니 홈페이지를 꼭 참고한다.

### 설치

Paste this into your terminal:

`curl -fsSL https://raw.githubusercontent.com/supermarin/Alcatraz/deploy/Scripts/install.sh | sh`

### 삭제

Delete the plugin:

`rm -rf ~/Library/Application\ Support/Developer/Shared/Xcode/Plug-ins/Alcatraz.xcplugin`

Remove all cached data:

`rm -rf ~/Library/Application\ Support/Alcatraz`

### 실행

Window > Package Manager 

## plugin 추천

### RTImageAssets

Xcode 에서 이미지를 자동으로 생성해주는 플러그인. 예) @3x 이미지에서 @2x 이미지를 만들어준다.

https://github.com/rickytan/RTImageAssets

### BBUFullIssueNavigator

이슈 네비게이터(issue navigator) 에서 이슈 전체 내용을 보여준다. Preferences > General > Issue Navigator Detail 에서 줄 수를 선택할 수 있다.

https://github.com/neonichu/BBUFullIssueNavigator




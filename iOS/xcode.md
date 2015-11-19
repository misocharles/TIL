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

### FuzzyAutocompletePlugin

Xcode 자동 완성 기능을 완벽하게 지원해주는 플러그인

https://github.com/FuzzyAutocomplete/FuzzyAutocompletePlugin
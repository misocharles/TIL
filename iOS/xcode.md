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

### FuzzyAutocompletePlugin

Xcode 자동 완성 기능을 완벽하게 지원해주는 플러그인

https://github.com/FuzzyAutocomplete/FuzzyAutocompletePlugin

### GitDiff

Xcode 에서 Git 의 마지막 커밋과 비교해 변경 사항을 표시해준다.

https://github.com/johnno1962/GitDiff

# Xcode

## Build Phases

### 빌드할 때 buildNumber 자동 증가

- Run Script 추가
- Shell : /bin/sh

```
buildNumber=$(/usr/libexec/PlistBuddy -c "Print CFBundleVersion" "$INFOPLIST_FILE")
buildNumber=$(($buildNumber + 1))
/usr/libexec/PlistBuddy -c "Set :CFBundleVersion $buildNumber" "$INFOPLIST_FILE"
```

불필요하게 commit 할 내용이 생겨서 script 제거함. 추적이 필요한 내용이라 .gitignore 에 넣기도 애매했음.

## Simulator

### Uninstall simulator

You can remove them from `/Library/Developer/CoreSimulator/Profiles/Runtimes`

![simruntime 파일 삭제](http://i.stack.imgur.com/fTJvE.png)

> http://stackoverflow.com/a/30940055

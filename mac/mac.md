## Key Remapping

macOS Sierra 로 업데이트하고 Key-mapping 용으로 사용하던 [Karabiner](https://pqrs.org/osx/karabiner/)을 더 이상 사용할 수 없었다.

[Remapping Keys in macOS 10.12 Sierra](https://developer.apple.com/library/content/technotes/tn2450/_index.html)에서 새로운 방법을 소개해 적용하였다.

왼쪽 Alt와 왼쪽 Command 키의 값이 필요하다. 해당 ID를 참조하여 스크립트를 실행한다.

|Usage|Usage ID (hex)|
|---|---|
|Keyboard Left Alt|0xE2|
|Keyboard Left GUI|0xE3|

```
$ hidutil property --set '{"UserKeyMapping":
    [{"HIDKeyboardModifierMappingSrc":0x7000000e2,
      "HIDKeyboardModifierMappingDst":0x7000000e3},
     {"HIDKeyboardModifierMappingSrc":0x7000000e3,
      "HIDKeyboardModifierMappingDst":0x7000000e2}]
}'
```

적용된 Key Remapping 상태는 `--get` 옵션으로 확인한다.

```
$ hidutil property --get "UserKeyMapping"
(
        {
        HIDKeyboardModifierMappingDst = 30064771299;
        HIDKeyboardModifierMappingSrc = 30064771298;
    },
        {
        HIDKeyboardModifierMappingDst = 30064771298;
        HIDKeyboardModifierMappingSrc = 30064771299;
    }
)
```

### 환경설정 > 키보드

환경설정 > 키보드 > 보조키에서 키를 바꿀 수 있다고 한다.

![스크린샷 2017-06-09 오전 10.33.35](http://i.imgur.com/2YT3Cdk.png)

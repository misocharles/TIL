# 앱 실행상태

어느 시점이든 앱은 표 2-3에 나열된 상태 중 하나의 상태입니다. 시스템은 시스템 전체에서 일어나는 작업에 응답하여 앱을 상태에서 다른 상태로 이동합니다. 예를 들어 사용자가 홈 버튼을 누르거나 전화가 오거나 그 외 여러 예외상황이 발생하면 현재 실행 중인 앱은 응답상태로 변경됩니다. 그림 2-3은 상태에서 상태로 이동할 때 앱이 수행하는 경로를 보여줍니다.

## 표 2-3 앱 상태

상태(State)|설명
-|-
`Not running`|앱이 실행되지 않았거나 실행 중이었으나 시스템에 의해 종료되었다.
`Inactive`|앱이 포그라운드에서 실행 중이나 현재 이벤트를 받지 않는다. (다른 코드를 수행하고 있을지도 모른다.) 앱은 보통 다른 상태에서 전환될 때 잠깐동안 이 상태에 머문다.
`Active`|앱이 포그라운드에서 실행 중이고 이벤트도 받고 있다. 포그라운드 앱의 일반적인 모드이다.
`Background`|앱이 백그라운드에서 코드를 실행하고 있다. 대부분의 앱은 일시 중지되는 동안 잠시 이 상태에 들어간다. 그러나 추가 실행 시간을 요청하는 앱은 일정기간 이 상태로 유지될 수 있다. 또한 백그라운드에서 직접 실행되는 앱은 `Inactive` 상태 대신 이 상태로 전환된다. 백그라운드에서 코드를 실행하는 방법은 [Background Execution](https://developer.apple.com/library/content/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/BackgroundExecution/BackgroundExecution.html#//apple_ref/doc/uid/TP40007072-CH4-SW1)을 참조한다.
`Suspended`|앱이 백그라운드에 있지만 코드를 실행 중이 아니다. 시스템은 앱을 자동으로 이 상태로 이동시키고 그렇게 하기 전에 알리지 않는다. 이 상태인 동안 앱은 메모리를에 남아 있지만 코드는 실행하지 않는다. 메모리 부족현상이 발생하면, 시스템은 포그라운드 앱을 위해 더 많은 공간을 확보갛기 위해 예고없이 이 상태(suspended)인 앱을 제거할 수 있다.

## 그림 2-3  State changes in an iOS app

![그림 2-3  State changes in an iOS app](https://developer.apple.com/library/content/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/Art/high_level_flow_2x.png)

대부분의 상태 전환은 app delegate 객체의 메소드 호출이 수반된다. 메소드들은 적절한 방법으로 상태 변화에 대응할 수 있는 기회이다. 메소드와 사용 방법의 요약은 아래에 나와있습니다.

* application:willFinishLaunchingWithOptions: - 이 메소드는 앱이 실행시 코드를 실행할 수 있는 첫 번째 기회입니다.
* application:didFinishLaunchingWithOptions: - 이 메소드을 사용하면 앱이 사용자에게 표시되기 전에 최종 초기화를 수행 할 수 있습니다.
* applicationDidBecomeActive: - 앱에 포그라운드 상태 앱이 될 것임을 알립니다. 마지막 순간의 준비에는 이 방법을 사용하십시오.
* applicationWillResignActive: - 앱이 포그라운드 상태 앱으로 전환하고 있음을 알 수 있습니다. 이 메소드를 사용하여 앱을 정지 상태로 만듭니다.
* applicationDidEnterBackground: - 이제 앱이 백그라운드에서 실행 중이며 언제든지 일시 중지 될 수 있음을 알 수 있습니다.
* applicationWillEnterForeground: - 앱이 백그라운드에서 벗어나 포그라운드로 돌아 왔지만 아직 활성화되지 않았음을 알 수 있습니다.
* applicationWillTerminate: - 앱이 종료 중임을 알 수 있습니다. 앱이 일시 중지된 경우 이 메소드는 호출되지 않습니다.

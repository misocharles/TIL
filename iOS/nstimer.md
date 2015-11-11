## NSTimer에 값 전달하기

`NSTimer` 생성할 때 값을 전달하고 싶은 경우 userInfo 를 사용한다. 

[+ scheduledTimerWithTimeInterval:target:selector:userInfo:repeats:](https://developer.apple.com/library/mac/documentation/Cocoa/Reference/Foundation/Classes/NSTimer_Class/#//apple_ref/occ/clm/NSTimer/scheduledTimerWithTimeInterval:target:selector:userInfo:repeats:)


```swift
let data = "This is new data."
NSTimer.scheduledTimerWithTimeInterval(1, target: self, 
    selector: Selector("callMethod:"), userInfo: data, repeats: false)
```

호출되는 method 에서 Timer user info 를 사용한다.

```swift
func callMethod(timer: NSTimer){
    if let data = timer.userInfo as? String {
        print(data)
    }
}
```

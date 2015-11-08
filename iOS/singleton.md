# SwiftSingleton

An exploration of the Singleton pattern in Swift. All approaches below support lazy initialization and thread safety.

Swift에서 싱글톤 패턴에 대한 탐구. 모든 방법은 뒤늦은 초기화(lazy initialization, 초기화를 뒤늦게 하는 것) 및 안전한 스레드를 지원합니다.

Issues and pull requests welcome.

문제 및 pull requests 를 환영합니다.

### Approach A: Class constant

```swift
class SingletonA {
    
    static let sharedInstance = SingletonA()
    
    init() {
        println("AAA");
    }
    
}
```

This approach supports lazy initialization because Swift lazily initializes class constants (and variables), and is thread safe by the definition of `let`.

이 방법은 Swift 가 뒤늦게 클래스 상수(와 변수)를 초기화하기 때문에 뒤늦은 초기화를 지원한다. `let` 으로 정의하여서 스래드로부터 안전하다.

Class constants were introduced in Swift 1.2. If you need to support an earlier version of Swift, use the nested struct approach below or a global constant.

클래스 상수는 Swift 1.2에서 소개되었다. Swift의 이전 버전을 지원해야하는 경우, 아래의 중첩 된 구조체 방식(nested struct) 또는 전역 상수(global constant)를 사용합니다.

### Approach B: Nested struct

```swift
class SingletonB {
    
    class var sharedInstance: SingletonB {
        struct Static {
            static let instance: SingletonB = SingletonB()
        }
        return Static.instance
    }
    
}
```

Here we are using the static constant of a nested struct as a class constant. This is a workaround for the lack of static class constants in Swift 1.1 and earlier, and still works as a workaround for the lack of static constants and variables in functions.

여기에서 우리는 클래스 상수로 중첩된 구조체의 정적 상수를 사용하고 있습니다. 1.1 이전 Swift 에서 정적 클래스 상수의 부족(lack)에 대한 해결 방법과, 여전히 함수에서 정적 상수와 변수의 부족에 대한 해결 방법으로 작동합니다.

### Approach C: dispatch_once

The traditional Objective-C approach ported to Swift.

```swift
class SingletonC {
    
    class var sharedInstance: SingletonC {
        struct Static {
            static var onceToken: dispatch_once_t = 0
            static var instance: SingletonC? = nil
        }
        dispatch_once(&Static.onceToken) {
            Static.instance = SingletonC()
        }
        return Static.instance!
    }
}
```

I'm fairly certain there's no advantage over the nested struct approach but I'm including it anyway as I find the differences in syntax interesting.

나는 어떤 장점은 중첩 된 구조체의 접근 방식을 통해이 없습니다 꽤 확신하지만 흥미로운 구문의 차이를 찾을 나는 어쨌든을 포함하고있다.

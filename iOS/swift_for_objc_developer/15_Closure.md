# 15장 Closure #

## 1. Capturing Value 값 획득 ##

클로저를 잘 이해하기 위해서는 앞에서 살펴본 함수 형식(Function Type)과 값 획득(Capturing Value)에 대해 알아야 합니다. 값 획득은 클로저가 선언되어 있는 범위(Scope)에 있는 상수나 변수를 클로저 내에서도 사용할 수 있도록 해 주는 기능입니다. 클로저가 획득한 값은 원래의 사용 범위를 벗어나더라도 클로저가 실행되는 동안 계속 존재합니다.

```swift
func outer(outerParam: Int) {
    var tmp = 3

    func inner() {
        tmp = tmp + outerParam
    }

    inner()

    print(tmp)
}

outer(7)
```

inner 함수와 같은 내포된 함수(Nested Function)도 클로저입니다. 값 획득은 다시 두가지 방식으로 구분할 수 있습니다.

- tmp는 inner 함수에 의해서 획득된 후 값이 변경되기 때문에 값이 아닌 참조가 획득됩니다.
- outerParam은 inner 함수 내부에서 값이 변경되지 않기 때문에 동일한 값을 가진 새로운 상수가 복사됩니다.

이러한 동작을 구분하는 기준은 Swift가 판단하고 획득된 값에 대한 메모리 처리 역시 Swift가 모두 처리해주기 때문에 Objective-C의 블록 프로그래밍에 비해 간편합니다. 그리고 블록에서 자주 발생하는 참조 싸이클(Retain Cycle) 문제도 [클로저 획득 목록](https://www.google.co.kr/#q=swift+closure+capture+list)
(Closure Capture List) 이라는 새로운 기능을 통해 손쉽게 해결하고 있습니다.

## 2. 클로저 표현식 ##

### 3가지 형태 ###

앞서 설명한 전역 함수와 내포된 함수도 일종의 클로저 입니다. 두 함수 모두 이름을 가진 클로저이지만 전역 함수의 경우 값 획득이 일어나지 않고 내포된 함수는 자신을 포함하고 있는 범위 내의 값들을 획득할 수 있는 차이점을 가지고 있습니다.  
가장 정확한 의미의 클로저는 `클로저 표현식으로 작성된 익명 함수이고 자신을 포함하고 있는 범위 내의 값들을 획득할 수 있습니다.` 클로저 표현식은 형식 추론(Type Inference)과 이름 축약을 통해 클로저의 정의를 간략하게 표현하며 주로 인라인 클로저(Inline Closure)를 w작성하는데 사용됩니다.

클로저 문법 (기본적인 형태)

```
{ (<파라미터 목록>) -> <리턴형> in <클로저 본문> }
```

파라미터와 리턴형을 선언하는 문법은 함수를 선언하는 것과 동일합니다. 상수, 변수, 입출력, 가변인자 파라미터를 사용할 수 있습니다. 기본값을 지정할 수는 없습니다. 함수의 경우 구현 부분을 {}(Brace)로 감싸주었지만 클로저는 선언과 구현이 포함된 모든 부분을 감싸 주어야 합니다.  
클로저는 주로 함수의 파라미터로 전달됩니다. 그래서 클로저를 작성할 때는 함수의 선언부분을 참고하여 클로저의 파라미터와 리턴형을 올바르게 작성해야 합니다.

```
func sort(@noescape isOrderedBefore: (Self.Generator.Element, Self.Generator.Element) -> Bool) -> [Self.Generator.Element]
```

Swift 2.2 기준 [func sort(_:)](http://swiftdoc.org/v2.2/protocol/MutableCollectionType/#func--sort_)

파라미터로 클로저를 받습니다. 클로저는 배열에 포함된 두 개의 요소를 파라미터로 받아 두 요소의 값을 비교한 결과를 리턴합니다. sort 함수는 리턴된 결과에 따라 배열을 재정렬합니다. 참고로 배열을 직접 정렬하지 않고 정렬된 새로운 배열을 리턴하는 함수가 필요하다면 sorted 함수를 사용합니다.  
sort 함수의 선언에서 보듯이 클로저의 형식(Type)은 함수형(Function Type)과 동일합니다. 그래서 sort 함수는 특정 자료형을 가지는 두 개의 값을 받아 Bool을 리턴하는 함수나 클로저를 모두 파라미터로 받을 수 있습니다. 사실 클로저 자체가 일종의 익명함수이기 때문에 함수 선언에서 이 둘을 구분하는 것은 무의미 합니다.

```swift
let languages = ["Swift", "C#", "Objective-C", "C++", "Java"]

func reverse(lhs: String, rhs: String) -> Bool {
    return lhs > rhs
}

languages.sort(reverse)
// ["Swift", "Objective-C", "Java", "C++", "C#"]
```

languages 배열은 문자열 배열이기 때문에 sort 함수 선언의 Element 는 `String`이 됩니다. 마찬가지로 sort 함수에 전달된 파라미터의 자료형은 `(String, String) -> Bool`이 됩니다. reverse 함수의 함수 형식(FunctionType)과 파라미터의 자료형이 일치하는 것을 확인할 수 있습니다.  
reverse 함수는 이름을 가지고 있기 때문에 sort 함수 뿐만 아니라 다른 함수에 파라미터로 전달하거나 직접 호출할 도 있습니다. 그러나 sort 함수에서만 사용되는 경우에는 별도의 함수로 구현하는 것보다 인라인 클로저로 구현을 하는 것이 좋습니다.

```swift
let languages = ["Swift", "C#", "Objective-C", "C++", "Java"]

languages.sort({ (lhs: String, rhs: String) -> Bool in
    return lhs > rhs
})
// ["Swift", "Objective-C", "Java", "C++", "C#"]
```

전역 함수를 인라인 클로저로 구현할 때는 대부분 다음과 같은 절차를 따릅니다.

1. 클로저 파라미터 부분을 `{}`로 대체합니다.  
`languages.sort({})`
2. func 키워드와 함수의 이름을 제외한 나머지 선언 부분을 복사합니다.  
`languages.sort({(lhs: String, rhs: Stirng) -> Bool })`
3. `in` 키워드를 통해 클로저 선언 부분을 마무리하고 구현 부분을 시작합니다.  
`languages.sort({(lhs: String, rhs: Stirng) -> Bool in })`
4. 클로저의 구현을 완료합니다. 함수와 달리 클로저의 구현 부분은 {}를 가지지 않습니다.  
`languages.sort({(lhs: String, rhs: Stirng) -> Bool in return lhs > rhs})`

swift는 sort 클로저 파라미터의 함수 형식을 추론할 수 있습니다. 그래서 다음과 같이 파라미터의 자료형과 파라미터 목록을 감싸는 괄호와 리턴형을 생략할 수 있습니다.  
`languages.sort({lhs, rhs in return lhs > rhs})`

클로저 표현식으로 작성한 인라인 클로저를 함수의 파라미터로 전달하는 경우에는 항상 형식 추론(Type Inference)이 가능합니다. 자료형과 리턴형을 명시적으로 포함하는 방식은 함수 형식을 직관적으로 인식할 수 있다는 장점이 있지만 swift에서는 생략된 방식을 주로 사용합니다. 이것은 선택사항이므로 프로그래머 선택에 달렸습니다.

앞에서 작성한 클로저는 두 개의 값을 비교한 결과를 리턴하는 **하나의 문장으로 구성되어 있습니다.**  클로저의 함수 형식을 통해 Bool 값을 리턴한다는 것을 추론할 수 있기 때문에 다음과 같이 return 키워드도 생략할 수 있습니다. 이러한 방식을 암시적 리턴(Implicit Return)이라고 합니다. 만약 클로저의 구현이 두 개 이상의 문장으로 구성되어 있다면 사용할 수 없습니다.  
```
languages.sort({lhs, rhs in lhs > rhs})
```

## 3. 이름 축약 ##

swift는 인라인 클로저를 선언할 때 자동으로 각 파라미터에 축약된 이름을 할당합니다. 이 이름은 $0, $1과 같이 $과 인덱스가 합쳐진 형태입니다. 축약된 이름을 통해서 파라미터의 값을 사용할 수 있기 때문에 다음과 같이 in 키워드를 포함한 클로저의 선언 부분을 생략할 수 있습니다. 이 경우 {}에는 클로저의 구현 부분만 포함됩니다.
```
languages.sort({$0 > $1})
```

## 4. 연산자 함수 ##

String은 두 문자열을 비교하는 연산자 함수(Operator Function)을 구현하고 있습니다. 앞서 사용된 > 연산자 역시 포함되어 있기 때문에 클로저를 더욱 간단하게 구현할 수 있습니다. 비교의 대상이 되는 자료형이 Bool을 리턴하는 연산자 함수를 구현하고 있고 파라미터의 자료형을 통해 이러한 내용을 추론할 수 있다면 이러한 방식을 사용할 수 있습니다.  
```
languages.sort(>)
```

## 5. Trailing Closure ##

인라인 클로저는 함수의 호출에 포함되기 때문에 클로저의 구현 부분이 단순한 경우에 적합합니다. 반대로 클로저의 구현이 복잡한 경우에는 트레일링 클로저로 구현하는 것이 적합합니다. 인라인 클로저와 트레일링 클로저의 가장 큰 차이는 클로저가 포함되는 위치입니다. 인라인 클로저는 함수 호출시 사용하는 괄호 내부에 위치하고, 트레일링 클로저는 괄호 이후에 위치합니다.

```
// Inline Closure
sort({ $0 > $1 })

// Trailing Closure
sort() { $0 > $1 }
```

트레일링 클로저는 클로저 표현식이 함수의 마지막 파라미터로 전달되는 경우에만 사용할 수 있습니다. 위의 코드와 같이 함수 호출시 전달되는 파라미터에서 트레일링 클로저에 해당되는 파라미터가 생략되고 괄호 이후에 트레일링 클로저가 옵니다. 이러한 문법이 새로운 함수를 구현하는 것과 유사하고 실제 파라미터 수를 혼동할 수도 있기 때문에 주의해야 합니다.

```
// 하나의 클로저 파라미터를 가진 함수에서 Trailing Closure 사용
func oneParamFunc(Closure: () -> String) {
    // code...
}

// 1
oneParamFunc() { () -> String in
    // code...
    return "I'm closure"
}

// 2
oneParamFunc { () -> String in
    // code...
    return "I'm closure"
}

```

oneParamFunc 함수는 하나의 클로저를 파라미터로 받습니다. 파라미터를 트레일링 클로저로 전달할 때는 파라미터 괄호가 생략되기 때문에 `// 1` 과 같은 방식으로 호출 할 수 있습니다. 그리고 빈 괄호 역시 생략할 수 있기 때문에 `// 2` 와 같은 방식도 가능합니다. 이 방식은 괄호가 생략되어 있기 때문에 전통적인 방식의 함수 호출과는 거리가 있습니다. 함수 이름 다음에 바로 {}가 온다면 이 함수는 하나의 파라미터를 가지고 있고, 이 파라미터는 트레일링 클로저라는 것을 직관적으로 유추할 수 있어야 합니다.

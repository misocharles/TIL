# 14장 Function #

함수는 프로그램을 구성하는 기능을 작은 단위로 구현한 코드 블록입니다.

```
func <함수 이름>(<파라미터 이름>: <파라미터 자료형>) -> <리턴형> {
  // code...
}
```

Swift의 함수는 **func** 키워드를 사용해서 선언합니다. Objective-C에서는 함수와 메소드를 사용하는 문법이 구분되지만 Swift에서는 동일한 문법을 사용합니다. 그래서 여기에서 설명하는 내용들은 클래스에도 동일하게 적용됩니다.  
함수와 파라미터 이름은 camelBack 방식으로 지정하는 것이 좋습니다. 파라미터는 변수나 상수를 선언하는 것과 동일한 문법으로 선언할 수 있고, 두 개 이상의 파라미터를 사용하는 경우네는 콤마(,)로 구분합니다. 파라미터를 사용하지 않는다면 빈 괄호만 적어줍니다.  
위의 함수 문법에서 파라미터 목록과 리턴형 사이에 있는 화살표(`->`)는 리턴 화살표(Return Arrow)입니다. 리턴형이 C 스타일은 함수 선언 앞쪽에 위치하지만 Swift는 마지막에 위치합니다.

```
// 기본적인 형태
func doSomething() {
  // code...
}
```

리턴값과 파라미터가 없는 단순한 형태의 함수입니다. 리턴값이 없는 경우 리턴형을 지정하는 부분을 생략합니다. 리턴형을 void로 지정하는 것과 동일하기 때문에 값을 리턴할 수 없고, 이러한 코드는 오류를 발생시킵니다.  
void는 주로 C와 맥락을 같이 하는 언어에서 "리턴값이 없음", "파라미터가 없음"을 나타내는 키워드입니다. Swift에서도 동일한 역할을 담당하는 **Void** 라는 특별한 자료형을 제공합니다. Swift의 Void는 빈 튜플이고 간단히 ()으로 표기할 수 잇습니다. `doSomething()`는 원칙적으로는 아래와 같지만 Void는 생략하는 것이 관례이기 때문에 거의 사용되지 않습니다.

```
func doSomething(()) {
  // code...
  return ()
}
```

## 1. 함수 호출 ##

```
doSomething()
```

## 2. 리턴 화살표 ##

리턴형을 지정할 때는 리턴 화살표를 사용합니다. 파라미터를 나열하는 괄호와 함수의 본문을 시작하는 `{` 사이에서 리턴형을 지정합니다. 공백을 반드시 포함시켜 줄 필요는 없지만 가독성을 위해서 각각의 *토큰* 을 공백으로 구분해주는 것이 좋습니다.

```
func doSomething() -> String {
  return "Something fun to do on Swift"
}
print(doSomething())
```

토큰 Token
>토큰은 프로그래밍 언어에서 더 이상 분리할 수 없는 가장 작은 단위의 언어적 요소입니다. do, switch, if 등과 같은 키워드와 {, (, +와 같은 요소들이 속합니다.

## 3. 파라미터 ##

```
func square(num: Int) -> Int {
  return num * num  
}
```

파라미터를 가진 함수의 예를 보여줍니다. `square()`는 하나의 정수를 받아 제곱수를 리턴합니다. Swift에서는 파라미터를 상수로 인십합니다. 그래서 함수 내부에서는 파라미터에 새로운 값을 할 수 없고, 이러한 코드가 별견되면 컴파일러가 오류를 발생시킵니다. 만약 함수 내부에서 파라미터의 값을 조작해야 한다면 변수 파라미터(Variable Parameter)로 선언해야 합니다.

```
func square(var num: Int) -> Int {
  return num * num  
}
```

두 개 이상의 파라미터를 상요할 때는 각 파라미터를 콤마로 구분합니다.

```
func add(a: Int, b: Int) -> Int {
  return a + b
}
```

## 4. 튜플 리턴 ##

Swift에서 새로 도입된 튜플(Tuple)을 사용하면 여러 개의 값을 동시에 리턴할 수 있습니다. 아래 `fetchName()`은 리턴형이 튜플로 선언되어 있고, 각 요소의 이름을 지정하고 있습니다. 이름을 지정하지 않고 인덱스로 튜플의 각 요소에 접근할 수 있지만, 가독성을 위해서 지정하는 습관을 갖는 것이 좋습니다.

```swift
// 서버와 연동이 되는 가상 함수
func fetchName(id: Int) -> (statusCode: Int, name: String) {
  // some code...
  let code = 200
  let fetchedName = "James"

  return (code, fetchedName)
}

let result = fetchName(123)
```

`fetchName()` 는 id 값에 따라서 올바른 이름을 가져오지 못할 수도 있습니다. code 값을 통해서 성공여부를 리턴할 수 있지만 리턴되는 튜플을 옵셔널로 선언하고 실패시 nil을 리턴하는 방식이 효율적입니다. 옵셔널 바인딩 패턴을 함께 사용하면 리턴값을 안전하게 처리할 수 있습니다.

```
func fetchName(id: Int) -> (statusCode: Int, name: String)? {
    // some code...
    let code = 200
    let fetchedName = "James"

    return (code, fetchedName)
}

if let result = fetchName(123) {
    print(result)
}
```

`(Int, String)?`와 같이 선언된 옵셔널 튜플(Optional Tuple)은 nil이 될 수 있습니다. 그러나 `(Int?, String?)`와 같이 선언된 튜플은 개별 요소가 nil이 될 수 있지만 튜플 전체가 nil이 될 수는 없습니다.

## 5. Parameter Names ##

모든 파라미터는 이름을 가지고 있습니다. 함수 내부에서 파라미터 값에 접근하는데 사용되며 **Local Parameter Name(내부 파라미터 이름, 지역 파라미터 이름)** 이라고 부릅니다.  
Objective-C는 함수나 메소드의 이름을 지을 때 간결함보다는 의미 전달과 직관성을 중요하게 생각합니다. 그래서 긴 이름을 가진 함수나 메소드를 흔히 볼 수 있습니다. `- (NSString *)stringByReplacingOccurrencesOfString:(NSString *)target withString:(NSString *)replacement` 메소드는 비교적 긴 이름을 가지고 있지만 메소드의 선언을 알지 못하는 경우에도 파라미터의 성격을 직관적으로 파악할 수 있습니다. `NSArray<NSString *> * NSSearchPathForDirectoriesInDomains ( NSSearchPathDirectory directory, NSSearchPathDomainMask domainMask, BOOL expandTilde )`는 이름을 통해서 함수의 역할은 파악이 되자만 마지막 `expandTilde` 파라미터의 역할은 파악하기가 어렵습니다.  
Swift는 함수의 이름을 C 스타일로 간결하게 유지하면서 Objective-C 메소드와 유사한 직관성을 제공하기 위해서 **External Parameter Nmae(외부 파라미터 이름)** 이라는 새로운 개념을 도입하였습니다. 지역 파라미터 이름과 별도로 외부에서 사용할 수 있는 파라미터 이름을 하나 더 선언하는 것입니다.

```swift
func replace(source: String, target: String, replace: String) -> String {
    var ret = ""
    // some code...
    return ret
}

var str = "Lorem ipsum dolor sit amet"
let reuslt = replace(str, target: " ", replace: "#")
```

`replace()`는 전달된 문자열에 포함된 공백 문자를 '#'으로 변경한 새로운 문자열을 리턴합니다. `NSSearchPathForDirectoriesInDomains()`와 마찬가지로 파라미터의 성격을 직관적으로 파악하기 어렵습니다. 이러한 문제는 외부 파라미터 이름으로 해결할 수 있습니다.  
외부 파라미터 이름은 파라미터 선언시 내부 파라미터 이름 앞에 위치합니다. 그리고 두 파라미터 이름은 공백으로 구분됩니다.

```
func <함수 이름>(<외부 파라미터 이름> <내부 파라미터 이름>: <파라미터 자료형>) {
  // code...
}
```

`replace()`의 각 파라미터에 외부 파라미터 이름을 지정하면 처음 사용하는 경우에도 각 파라미터의 역할을 직관적으로 파악할 수 있습니다. 아래의 코드에서 sourceString, targetString, replaceString이 각 파라미터를 나타내는 외부 파라미터 이름입니다. 내부 파라미터 이름은 함수 내부에서만 사용할 수 잇는 것처럼 외부 파라미터 이름은 함수 호출 시에만 사용되며 함수 내부에서 인식할 수 없습니다.

>여기서부터는 Swift 1.1과 2.2 차이가 크기 때문에 다시 알아보고 정리가 필요하다. 위에 내용도 바뀔 예정.

## 후기 ##

기본적인 함수 사용부터 많은 것이 바뀌었다.

* http://hsg2510.tistory.com/30#recentEntries

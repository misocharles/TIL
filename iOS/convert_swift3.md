# Swift 3.0

## Convert to Swift 3.0

현재 개발환경은 Xcode 8.2.1 (8C1002), Swift 2.3 입니다.

Xcode에서 제공하는 Covert 기능으로 시작합니다.

Xcode > Edit > Convert > To Current Swift Syntax...

Xcode 8.2.1 이전에서는 Swift 2.3 와 Swift 3 중 원하는 버전을 선택할 수 있었습니다.

cocoapods 라이브러리들은 제외하고 프로젝트 파일들을 선택해줍니다.

엄청난 에러가 발생해도 놀라지 마세요.

Podfile 을 열어 라이브러리들을 업데이트 해줍니다. `$ pod outdated` 로 업데이트할 버전을 확인합니다. 간혹 Swift 3 를 미처 지원하지 않는 라이브러리들이 있습니다.

제 경우는 Swift 3 에 관련된 업데이트가 필요한 라이브러리가 `Alamofire, JASON, ReachabilitySwift` 였습니다.

Migration 을 진행합니다.

## Migration

### Alamofire

[Alamofire 4.0 Migration Guide](https://github.com/Alamofire/Alamofire/blob/master/Documentation/Alamofire%204.0%20Migration%20Guide.md)

before

`ParameterEncoding.URL.queryComponents(key, value)`

after

`URLEncoding.default.queryComponents(fromKey: key, value: value)`

#### Benefits of Upgrading

The benefits of upgrading can be summarized as follows:

* No more casting a response serializer `error` from an `ErrorType` to an `NSError`.
* Original server data is now ALWAYS returned in all response serializers regardless of whether the result was a `.Success` or `.Failure`.
* Custom response serializers are now ALWAYS called regardless of whether an `error` occurred.
* Custom response serializers are now passed in the `error` allowing you to switch between different parsing schemes if necessary.
* Custom response serializers can now wrap up any Alamofire `NSError` into a `CustomError` type of your choosing.
* `Manager` initialization can now accept custom `NSURLSession` or `SessionDelegate` objects using dependency injection.

## Swift 3

### Empty collection literal requires an explicit type

`var pickerData = []`

`var pickerData: Array<Any> = []`


### @escaping

* http://stackoverflow.com/questions/39063499/updating-closures-to-swift-3-escaping

closure use of non-escaping parameter '#funcName#' may allow it to escape.

### enum

Enums may not contain stored properties

### CoreGraphics

```Swift
CGContextDrawImage(ctx, area, self.cgImage)
```

`CGContextDrawImage is unavailable. use draw(_:in:)`

```
public func draw(_ image: CGImage, in rect: CGRect, byTiling: Bool = default)
```

```Swift
ctx?.draw(self.cgImage!, in: area)
```

#### CGRectDivide

before

`CGRectDivide(CGRect rect, CGRect *  slice, CGRect *  remainder, CGFloat amount, CGRectEdge edge)`

```Swift
fileprivate func isLeftPointContainedWithinBezelRect(_ point: CGPoint) -> Bool {
    var leftBezelRect: CGRect = CGRect.zero
    var tempRect: CGRect = CGRect.zero
    let bezelWidth: CGFloat = self.options.leftBezelWidth

    CGRectDivide(self.view.bounds, &leftBezelRect, &tempRect, bezelWidth, CGRectEdge.minXEdge)
    return leftBezelRect.contains(point)
}
```

after

`public func divided(atDistance: CGFloat, from fromEdge: CGRectEdge) -> (slice: CGRect, remainder: CGRect)`

```Swift
fileprivate func isLeftPointContainedWithinBezelRect(_ point: CGPoint) -> Bool {
    var leftBezelRect: CGRect = CGRect.zero
    var tempRect: CGRect = CGRect.zero
    let bezelWidth: CGFloat = self.options.leftBezelWidth

    (leftBezelRect, tempRect) = self.view.bounds.divided(atDistance: bezelWidth, from: CGRectEdge.minXEdge)
    return leftBezelRect.contains(point)
}
```

https://github.com/apple/swift/blob/master/stdlib/public/SDK/CoreGraphics/CoreGraphics.swift

### dispatch queue

Compiles under Xcode 8 beta 6 Swift 3. This example contains most of the syntax what we need.

qos - new quality of service syntax

weak self - to disrupt retain cycles

async global background queue - for network query

async main queue - for touching the UI.

Of course you need to add some error checking to this...

`dispatch_async(dispatch_get_main_queue()) {}`
`DispatchQueue.global(qos: DispatchQoS.QoSClass.default).async {}`
`DispatchQueue.main.async {}`

```Swift
    DispatchQueue.global(qos: .background).async { [weak self]
        () -> Void in
        self?.flickrPhoto.loadLargeImage
            {
                loadedFlickrPhoto, error in
                if error != nil {
                    print("error:\(error)")
                } else {

        DispatchQueue.main.async {
            () -> Void in
            activityIndicator.removeFromSuperview()
            self?.imageView.image = self?.flickrPhoto.largeImage
                    }
                }
        }

    }
```

### func MD5() -> String

Swift 2.3

```Swift
func MD5() -> String {
    let data = (self as NSString).data(using: String.Encoding.utf8.rawValue)
    let result = NSMutableData(length: Int(CC_MD5_DIGEST_LENGTH))
    let resultBytes = UnsafeMutablePointer<CUnsignedChar>(result!.mutableBytes)
    CC_MD5((data! as NSData).bytes, CC_LONG(data!.count), resultBytes)

    let a = UnsafeBufferPointer<CUnsignedChar>(start: resultBytes, count: result!.length)
    let hash = NSMutableString()

    for i in a {
        hash.appendFormat("%02x", i)
    }

    return hash as String
}
```

Swift 3.0

```Swift
func md5() -> String {
    let str = self.cString(using: String.Encoding.utf8)
    let strLen = CUnsignedInt(self.lengthOfBytes(using: String.Encoding.utf8))
    let digestLen = Int(CC_MD5_DIGEST_LENGTH)
    let result = UnsafeMutablePointer<CUnsignedChar>.allocate(capacity: digestLen)
    CC_MD5(str!, strLen, result)

    let hash = NSMutableString()

    for i in 0 ..< digestLen {
        hash.appendFormat("%02x", result[i])
    }
    result.deinitialize()

    return String(format: hash as String)
}
```

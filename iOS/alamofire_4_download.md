# Alamofire 4.0 downlaod

## Alamofire 3.x 에서 4.0 으로 마이그레이션

`DownloadManager` 클래스를 싱글턴 인스턴스로 생성한다. `DownloadManager` 는 `Alamofire.SessionManager` 값을 가지고 있다. `SessionManager`는 `URLSessionConfiguration.background` 환경값을 설정하여 생성한다.

`Alamofire.Request` 객체들을 배열로 관리하기 위해 `handlerQueue` 변수를 선언한다.

```Swift
open class DownloadManager {

    static let sharedInstance = DownloadManager()

    var handlerQueue: [String: Alamofire.Request] = [:]

    let manager: SessionManager = {
        let identifier = Bundle.main.bundleIdentifier! + ".background"
        let configuration = URLSessionConfiguration.background(withIdentifier: identifier)
        return SessionManager(configuration: configuration)
    }()

    var backgroundCompletionHandler: (() -> Void)? {
        get {
            return manager.backgroundCompletionHandler
        }
        set {
            manager.backgroundCompletionHandler = newValue
        }
    }
}
```

### Alamofire 3.x

`DownloadManager` 에서 생성한 `SessionManager` 를 이용하여 download 를 진행한다.

```
let urlString = "다운로드 url"
let request = DownloadManager.sharedInstance.manager.download(.get, method: urlString,
    parameters: { (temporaryURL, response) in
        let directoryURL = NSFileManager.defaultManager().URLsForDirectory(.CachesDirectory, inDomains: .UserDomainMask)[0]
        let folderPath = directoryURL.URLByAppendingPathComponent("Downloads/")!
        let fileName = response.suggestedFilename
        return folderPath.URLByAppendingPathComponent(fileName)!
    })
    .progress { bytesWrite, totalBytesWrite, totalBytesExpectedToWrite in
        // progress
    }
    .response { request, response, data, error in
        // response
    }
```

### Alamofire 4.0

`DownloadRequest.DownloadFileDestination`에 원하는 경로와 파일명을 설정하여 `Alamofire.DownloadRequest`으로 넘겨준다.

```
let destination: DownloadRequest.DownloadFileDestination = { _, _ in
    let pathComponent = "fileName"
    let directoryURL: URL = FileManager.default.urls(for: .cachesDirectory, in: .userDomainMask)[0]
    let folderPath: URL = directoryURL.appendingPathComponent("Downloads", isDirectory: true)
    let fileURL: URL = folderPath.appendingPathComponent(pathComponent)
    return (fileURL, [.removePreviousFile, .createIntermediateDirectories])
}

let urlString = "다운로드 url"
DownloadManager.sharedInstance.manager.download(urlString, to: destination)
    .downloadProgress(queue: DispatchQueue.global(qos: .background)) { progress in
        println("Progress: \(progress.fractionCompleted)")
    }
    .responseData { response in
        debugPrint(response)
        println(response.temporaryURL)
        println(response.destinationURL)
    }
```

DownloadRequest 에서 제공하는 기본값도 있다.

`let destination = DownloadRequest.suggestedDownloadDestination()`

## download 오류 발생

Wifi와 3G/LTE간 네트워크가 변경되면서 진행 중인 download가 종료되는 현상이 발생하였다. 원인은 CDN 인증 방식이었다. download url에 포함된 key값에 해당 클라이언트 IP가 포함되어 있어서, 네트워크 변경으로 인증 key의 인증이 실패되었다.

Alamofire 3.x 버전에서 `.response` 메소드를 사용했는데, 위 에러가 발생하면 error가 nil로 반환되었다. 그래서 정상적으로 다운로드가 완료되었다고 판단되는 오류가 발생했다. 그래서 `responseData`를 사용하여 오류를 확인하였고, 정상적으로 처리할 수 있었다.

```Swift
    .responseData { response in
        debugPrint(response)

        switch response.result {
        case .Success:
            print("Success")
        case .Failure(let error):
            print(error)
        }
    }
```

네트워크 변경으로 다운로드가 끊기는 경우 에러를 받아내지 못하는 버그가 있어서, `responseData`를 사용했는데 정상적인 상황에서도 `-6004 "Data could not be serialized. Input data was nil."` 오류가 발생하였다.

https://github.com/Alamofire/Alamofire/issues/1306#issuecomment-225460041

You cannot use the `responseData` serializer with the `download` API. You instead need to use the `response` API and check the `error` parameter. Then you need to read the data our of the filePath that you moved the file to in the `Destination` closure. Here's a [link](https://github.com/Alamofire/Alamofire#downloading-a-file-wprogress) to the README that demonstrates how to do this.

`download` API에서는 `responseData`를 사용할 수 없다고 하여, 기존 `response` 로 복구하고 다른 방법을 사용하였다. 네트워크 변경 event 발생시 `Request`의 `cancel()` 메서드를 호출했다. `response` 에 `canceled` 오류가 반환되어 정상적으로 처리할 수 있었다.

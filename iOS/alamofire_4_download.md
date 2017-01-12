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

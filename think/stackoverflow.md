# stackoverflow

stackoverflow에 처음 답변을 달았다. Alamofire 4.0으로 마이그레이션 작업과 관련하여 `Alamofire.DownloadRequest.DownloadFileDestination`에 대해 찾아보았다. 

친절한 설명과 함께 코드를 사용했는데, `appendingPathComponent`함수는 Mutable URL에 사용하기 때문에 컴파일 오류가 났다.  `appendingPathComponent` 함수로 변경하고 기능 확인을 했다. 갑자기 답변을 달아볼까 생각이 들어서 내용을 정리하고 등록했다.

대단한 내용은 아니지만, stackoverflow에 답변을 달았다는 것이 뿌듯하다.

http://stackoverflow.com/questions/41136560/setting-alamofire-custom-destination-file-name-instead-of-using-suggesteddownloa/41561560#41561560

## 남긴 답변 :)

Use `func appendingPathComponent(_ pathComponent: String) -> URL` instead of `appendPathComponent`.

    let destination: DownloadRequest.DownloadFileDestination = { _, _ in
        let pathComponent = "yourfileName"
        let directoryURL: URL = FileManager.default.urls(for: .documentDirectory, in: .userDomainMask)[0]
        let folderPath: URL = directoryURL.appendingPathComponent("Downloads", isDirectory: true)
        let fileURL: URL = folderPath.appendingPathComponent(pathComponent)
        return (fileURL, [.removePreviousFile, .createIntermediateDirectories])
    }

and it is also possible to use `response`.

    let destination: DownloadRequest.DownloadFileDestination = { _, response in
        let pathComponent = response.suggestedFilename!
        let directoryURL: URL = FileManager.default.urls(for: .cachesDirectory, in: .userDomainMask)[0]
        let folderPath: URL = directoryURL.appendingPathComponent("Downloads", isDirectory: true)
        let fileURL: URL = folderPath.appendingPathComponent(pathComponent)
        return (fileURL, [.removePreviousFile, .createIntermediateDirectories])
    }

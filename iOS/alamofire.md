# Alamofire

## POST request with a simple string in body with Alamofire

http://stackoverflow.com/questions/27855319/post-request-with-a-simple-string-in-body-with-alamofire

```swift
extension String: ParameterEncoding {

    public func encode(_ urlRequest: URLRequestConvertible, with parameters: Parameters?) throws -> URLRequest {
        var request = try urlRequest.asURLRequest()
        request.httpBody = data(using: .utf8, allowLossyConversion: false)
        return request
    }

}

Alamofire.request("http://mywebsite.com/post-request", method: .post, parameters: [:], encoding: "myBody", headers: [:])
```

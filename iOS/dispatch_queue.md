# dispatch queue


## How to create dispatch queue in Swift 3

http://stackoverflow.com/a/37806522/4622153

Creating a concurrent queue
```Swift
let concurrentQueue = DispatchQueue(label: "queuename", attributes: .concurrent)
concurrentQueue.sync {

}
```  

Create a serial queue
```Swift
let serialQueue = DispatchQueue(label: "queuename")
serialQueue.sync {

}
```  

Get main queue asynchronously
```Swift
DispatchQueue.main.async {

}
```  

Get main queue synchronously
```Swift
DispatchQueue.main.sync {

}
```  

To get one of the background thread
```Swift
DispatchQueue.global(attributes: .qosDefault).async {

}
```  

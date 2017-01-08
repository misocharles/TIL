# getting-started

http://www.scala-lang.org/documentation/getting-started.html 문서 실습

## 실습

### "Hello, world" Program

```scala
object HelloWorld {
  def main(args: Array[String]): Unit = {
    println("Hello, world!")
  }
}
```

### 바로 실행하기

```scala
> scala
Welcome to Scala 2.12.1 (Java HotSpot(TM) 64-Bit Server VM, Java 1.8.0_111).
Type in expressions for evaluation. Or try :help.

scala> object HelloWorld {
     |     def main(args: Array[String]) {
     |       println("Hello, world!")
     |     }
     |   }
defined object HelloWorld

scala> HelloWorld.main(Array())
Hello, world!
```

### 컴파일

위의 Hello, world 소스를 HelloWorld.scala 에 저장한다. 아래 명령어로 컴파일한다.

```
> scalac HelloWorld.scala
```

HelloWorld.class, HelloWorld$.class 두 개의 파일이 생성되었다.

### 실행

```
> scala HelloWorld
Hello, world!
```

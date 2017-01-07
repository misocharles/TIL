# Scala

## 설치

### Windows

#### 1. JDK 설치

http://www.oracle.com 홈페이지에서 [다운로드](http://www.oracle.com/technetwork/java/javase/downloads/index.html)

#### 2. Scala 설치

http://www.scala-lang.org/download 최신버전 다운로드

#### 3. 환경변수 설정

JAVA

    JAVA_HOME %JDK_설치경로%
    PATH - %JAVA_HOME%\bin

Scala

    SCALA_HOME C:\Program Files (x86)\scala
    PATH - %SCALA_HOME%\bin


저는 PATH 는 위 설치과정에서 자동으로 설정되어 있었습니다.

#### 4. 설치 확인

JAVA

    c:\> java -version
    java version "1.8.0_111"
    Java(TM) SE Runtime Environment (build 1.8.0_111-b14)
    Java HotSpot(TM) 64-Bit Server VM (build 25.111-b14, mixed mode)

Scala

    c:\> scala
    Welcome to Scala 2.12.1 (Java HotSpot(TM) 64-Bit Server VM, Java 1.8.0_111).
    Type in expressions for evaluation. Or try :help.

    scala>

# Swift Compiler

## Swift 3

기존 Swift 2.3 으로 개발된 프로젝트를 Swift 3 로 변환하였다. 기본 로직부터 cocoapod 라이브러리까지 Swift 3 로 수정하였다. 시뮬레이터와 디바이스 테스트를 끝내고 TestFlight로 올리기 위해서 Archive를 했는데 compile이 되질 않았다. indexing files 에서 멈춰 있었다.

최근 Swift Compiler 최적화에 대한 논의가 많이 벌어지고 있으며, 위 증상은 compiler 옵션을 변경하면 된다는 것을 알았다.

도움을 받은 참고글들을 모으고 정리를 해야겠다.

## 참고글

### 국문

* [WMO 알아보기 (컴파일 최적화)](https://brunch.co.kr/@joonwonlee/14)
* [Swift 컴파일 최적화 옵션 ](https://swifter.kr/2015/11/13/swift-%EC%BB%B4%ED%8C%8C%EC%9D%BC-%EC%B5%9C%EC%A0%81%ED%99%94-%EC%98%B5%EC%85%98/)
* [컴파일러 친화적으로 Swift 코딩 하기 싫다](https://code.iamseapy.com/archives/33)
* [Swift는 정말 파이썬보다 빠를까?](http://soooprmx.com/wp/archives/5436#more-5436)
* [[Swift] 서능향상 시키기 - 다이나믹 디스패치를 최소화](http://hiddenviewer.tistory.com/253)
* [Swift에서 보이는 Apple의 컴파일러 기술 ](http://www.devblog.kr/r/8y0gFPAvJ2g8MOY0I3m7vQ93JPqAmT5872Je4n6YT2P)

### 영문

* [Whole-Module Optimization in Swift 3](https://swift.org/blog/whole-module-optimizations/)
* [Speeding Up Slow Swift Build Times](https://medium.com/swift-programming/speeding-up-slow-swift-build-times-922feeba5780#.vw4o52n5i)
* [Regarding Swift build time optimizations](https://medium.com/@RobertGummesson/regarding-swift-build-time-optimizations-fc92cdd91e31#.tzfz8t531)
* [Swift performance: sorting arrays](http://stackoverflow.com/questions/24101718/swift-performance-sorting-arrays)

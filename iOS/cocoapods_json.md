# JSON Library 교체기

SwiftyJSON 의 업데이트가 늦어서 다른 라이브러리로 교체하기로 결심했다.

## Swift > JSON 검색

https://swift.libhunt.com/categories/657-json

## 첫번째 조건은 popularity, activity 가 모두 6.0 이상

(목록은 activity 순. SwiftyJSON 덕분에 activity의 중요성을 새삼느꼈다)

Decodable  
7.5	8.2 https://github.com/Anviking/Decodable
JSON parsing for Swift 2.		
Monthly Downloads: 7,926
License: MIT License

Unbox  
7.8	7.9 https://github.com/JohnSundell/Unbox
The easy to use Swift JSON decoder.		
Monthly Downloads: 14,541
License: MIT License

Gloss  
7.8	7.5 https://github.com/hkellaway/Gloss
shiny JSON parsing library.		
Monthly Downloads: 38,405
License: MIT License

Himotoki  
6	7.5 https://github.com/ikesyo/Himotoki
A type-safe JSON decoding library purely written in Swift.		
Monthly Downloads: 4,601
License: MIT License

ObjectMapper  
9.7	7.2 https://github.com/Hearst-DD/ObjectMapper
JSON object mapper.		
Monthly Downloads: 282,093
License: MIT License

JASON  
7.4	7 https://github.com/delba/JASON
JSON parsing with outstanding performances and convenient operators.		
Monthly Downloads: 5,424
License: MIT License

Argo  
9.3	7 https://github.com/thoughtbot/Argo
Json parsing library.		  
Monthly Downloads: 44,293
License: MIT License

Genome  
7	6.2 https://github.com/LoganWright/Genome
A simple, type safe, failure driven mapping library for serializing JSON to models in Swift 2.0.		
Monthly Downloads: 0 (기록없음)
License: MIT License

### 목록 추가

libhunt에 누락되어 있던 JsonSwiftson 추가

JsonSwiftson  
0.4 7.0
https://github.com/evgenyneu/JsonSwiftson
Monthly Downloads: 41
License: MIT License

## Swift 3 최적화 여부

| Library | Compatible branch |
| --- | --- |
| Decodable |[master](https://github.com/Anviking/Decodable)|
| Unbox |[swift3](https://github.com/JohnSundell/Unbox/tree/swift3)|
| Gloss |[swift_3.0](https://github.com/hkellaway/Gloss/tree/swift_3.0)|
| Himotoki |[swift3](https://github.com/ikesyo/Himotoki/tree/swift3)|
| ObjectMapper |[swift-3](https://github.com/Hearst-DD/ObjectMapper/tree/swift-3)|
| JASON |[swift-3.0](https://github.com/delba/JASON/tree/swift-3.0)|
| Argo |[master](https://github.com/thoughtbot/Argo)|
| Genome |[lw/swift-3](https://github.com/LoganWright/Genome/tree/lw/swift-3)|
| JsonSwiftson |[master](https://github.com/evgenyneu/JsonSwiftson)|

  `Genome`은 마지막 commit이 7개월 전이다. 역시 activity 가 6.0 인 이유가 있었다. out.  
  `Argo`는 Xcode 8 beta 4까지만 업데이트가 되어 있다. 현재 beta 6까지 나옴. out.  
  `Decodable`, `Argo`, `JsonSwiftson`은 Swift 3.0 버전을 master branch로 개발 중이다. good.  
  역시 activity가 낮은 Library는 제거대상 1순위이다.

## 사용성, 마이그레이션 편의성

(작성 중)

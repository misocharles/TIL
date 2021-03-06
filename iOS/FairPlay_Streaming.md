# FairPlay Streaming Overview

## FairPlay Streaming

이 개요에서는 Apple의 FairPlay Streaming (FPS) 사양에 대해 자세히 설명합니다. FPS는 암호화된 비디오 콘텐츠를 재생할 수 있는 키를 Apple 모바일 디바이스, Apple TV 및 OS X의 Safari에 안전하게 전송합니다. 이 콘텐츠는 HTTP Live Streaming (HLS)을 사용하여 웹을 통해 전달됩니다. FPS는 콘텐츠 키와 함께 전송된 만료 정보를 기반으로 재생을 정지하는 모바일 디바이스와 Apple TV를 허용한다. 또한 상수 FPS 장치 식별자(device identifier)는 서버 재생 컨텍스트 (SPC) 메시지로 서버에 전송되어, 서버가 익명의 개별적으로 장치를 식별할 수 있게 합니다. FTP는 iOS와 Apple TV에 대한 기본 지원과 함께 장치 운영 체제에 통합되어 있습니다. OS X의 Safari는 EME 인터페이스를 사용하여 지원 가능합니다.

### Key Delivery Process

FPS를 통해 콘텐츠 공급자는 공급자의 키 서버에서 AES 128-bit 콘텐츠 키를 안전하게 제공할 수 있습니다. 콘텐츠 제공자는 H.264 비디오 콘텐츠를 콘텐츠 키로 암호화합니다. 그리고 FPS는 암호화된 비디오 콘텐츠를 콘텐츠 키로 복호화합니다. 그림 1-1은 키와 콘텐츠 교환을 보여줍니다.

#### Figure 1-1 FPS exchanges

![Figure 1-1 FPS exchanges](이미지링크)

* FPS 프레임워크는 키 콘텐츠 제공자 키 서버와의 세션을 생성하기 위한 키 전송 프로세스를 초기화한다.
* 콘텐츠 제공자 키 서버는 128-bit AES 콘텐츠 키를 세션 키와 반복 재생 방지 메커니즘으로 래핑합니다.
* 키 전송 프로세스는 3중 보호 솔루션 (AES, RSA 및 파생 기능)을 구현합니다.
* 콘텐츠 제공자는 H.264 비디오 콘텐츠를 AES-CBC 모드 콘텐츠 키와 초기화 벡터를 사용하여 프레임 단위로 암호화합니다.
* 콘텐츠 제공자는 오디오 콘텐츠를 AES-CBC 모드 콘텐츠 키와 초기화 벡터를 사용하여 완전히 암호화합니다.
* FPS는 H.264 비디오 코덱과 AAC-LC, HE-AACV1-2, AC-3, and EC-3 오디오 코덱을 지원합니다. 오디오 코덱은 Safari의 FPS에 따라 다를 수 있습니다.
* 키 처리와 콘텐츠 복호화는 iOS 장치의 커널에서 발생합니다. 즉, 콘텐츠 및 콘텐츠 키는 복호화를 위해 장치 커널에 보관됩니다.
* FPS는 항상 보호된 콘텐츠 블록에 대해 HDCP를 시행합니다.
* FPS는 오프라인 재생을 위한 보안 자료의 지속성을 지원합니다.
* 콘텐츠 제공자는 콘텐츠 키, 키 관련 초기화 벡터 데이터베이스 그리고 콘텐츠의 암호화 모드를 관리합니다.
* FPS는 Apple TV을 위한 AirPlay Streaming을 지원합니다.
* FPS는 콘텐츠 키를 요청하는 장치의 익명 식별를 제공합니다.
* 콘텐츠 제공자가 계정당 스트림을 동시에 관리할 수 있도록 하는 보안 리스 메커니즘입니다.
* FPS는 iOS 장치 및 Apple TV에서 영화 대여를 위한 콘텐츠 키 만료를 지원합니다.

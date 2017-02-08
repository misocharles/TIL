# Core Telephony

`CoreTelephony` 프레임워크를 추가한다.

```
import CoreTelephony
```

`CTCarrier` 클래스에서 이동통신사 정보를 얻는다.

```
var carrierName: String {
    let networkInfo = CTTelephonyNetworkInfo()
    if let carrier = networkInfo.subscriberCellularProvider, let carrierName = carrier.carrierName {
        return carrierName
    }
    return ""
}
```

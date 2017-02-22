### WIFI SSID 얻기

```objective-c
#import <SystemConfiguration/CaptiveNetwork.h>

- (NSString *)getSsid {
  // Does not work on the simulator.
  NSString *ssid = nil;
  NSArray *ifs = (__bridge_transfer id)CNCopySupportedInterfaces();
  for (NSString *ifnam in ifs) {
    NSDictionary *info = (__bridge_transfer id)CNCopyCurrentNetworkInfo((__bridge CFStringRef)ifnam);
    if (info[@"SSID"]) {
      ssid = info[@"SSID"];
    }
    NSLog(@"%@", info);
  }
  return ssid;
}
```

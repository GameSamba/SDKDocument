#### 事件调用

除去GoogleAnalytics的事件调用方法为:

```Objective-C
[NGAAppEvents.sharedInstance recordEvent:@"TestEventA"];
[NGAAppEvents.sharedInstance recordEvent:@"TestEventC" values:@{@"level" : @"10"}];
```

GoogleAnalytics的事件调用方法比较特殊, 接口方法为:

```
- (void)gaSendEventWithCategory:(NSString *)category action:(NSString *)action label:(NSString *)label value:(NSNumber *)value;
```

例如:

```Objective-C
[NGAAppEvents.sharedInstance gaSendEventWithCategory:@"Player_Info"
                                              action:@"Level"
                                               label:nil
                                               value:@(888)];
```

注意:![](/.gitbook/assets/图片2.png)

综上, 也就是常规情况下, 一次完整的事件调用需要分别调用

`- (void)recordEvent:(NSString *)key values:(NSDictionary *)values`

和

`- (void)gaSendEventWithCategory:(NSString *)category action:(NSString *)action label:(NSString *)label value:(NSNumber *)value` 两个方法


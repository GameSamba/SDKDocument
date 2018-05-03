#### 事件调用

除去GoogleAnalytics的事件调用方法为:

```Objective-C
[NGAAppEvents.sharedInstance recordEvent:@"TestEventA"];
[NGAAppEvents.sharedInstance recordEvent:@"TestEventC" values:@{@"level" : @"10"}];
```

GoogleAnalytics的事件调用方法比较特殊, 接口方法为:

```
///parameters构造必须依照GAIDictionaryBuilder.h
- (void)gaSend:(NSDictionary *)parameters;
```

例如:

```Objective-C
[NGAAppEvents.sharedInstance gaSend:[[GAIDictionaryBuilder
                createEventWithCategory:@"Player_Info"
                                 action:@"Level"
                                  label:@"888"
                                  value:nil] build]];
```

注意:![](/.gitbook/assets/图片2.png)

综上, 也就是常规情况下, 一次完整的事件调用需要分别调用

`- (void)recordEvent:(NSString *)key values:(NSDictionary *)values`

和

`- (void)gaSend:(NSDictionary *)parameters` 两个方法


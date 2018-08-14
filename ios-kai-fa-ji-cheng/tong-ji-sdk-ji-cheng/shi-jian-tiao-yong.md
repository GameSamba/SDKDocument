# 事件调用

一般情况下事件调用方法为:

```objective-c
[NGAAppEvents.sharedInstance recordEvent:@"TestEventA"];
[NGAAppEvents.sharedInstance recordEvent:@"TestEventC" values:@{@"level" : @"10"}];
```

Google Firebase的事件调用方法接口为:

```objective-c
- (void)gaLogEventWithName:(NSString *)name parameters:(NSDictionary<NSString *, id> *)parameters;
```



根据需求去确认是否调用Google Firebase的事件记录.


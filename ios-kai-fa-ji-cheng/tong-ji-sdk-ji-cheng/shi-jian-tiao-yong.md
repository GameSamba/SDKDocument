# 事件调用

一般情况下事件调用方法为:

```objectivec
[NGAAppEvents.sharedInstance recordEvent:@"TestEventA"];
[NGAAppEvents.sharedInstance recordEvent:@"TestEventC" values:@{@"level" : @"10"}];
```

Google Firebase的事件调用方法接口为:

```objectivec
- (void)gaLogEventWithName:(NSString *)name parameters:(NSDictionary<NSString *, id> *)parameters;
```

根据需求去确认是否调用Google Firebase的事件记录.

## Purchase事件单独调用

```objectivec
/**
 记录购买事件

 @param contentID 物品ID
 @param contentType 物品类型
 @param revenue 金额
 @param currency 货币单位  例如 @"USD", @"HKD", @"CNY", @"TWD" 等等, 更多请参考 https://www.xe.com/iso4217.php
 @param serverID 服务器ID
 */
- (void)recordPurchaseEventWithContentID:(NSString *)contentID contentType:(NSString *)contentType revenue:(double)revenue currency:(NSString *)currency serverID:(NSString *)serverID;
```

Example:

```objectivec
[NGAAppEvents.sharedInstance recordPurchaseEventWithContentID:@"123456"
                                                  contentType:@"category_a"
                                                      revenue:1.99
                                                     currency:@"USD"
                                                     serverID:@"1001"];
```


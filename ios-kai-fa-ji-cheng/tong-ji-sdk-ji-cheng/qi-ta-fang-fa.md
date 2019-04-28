# 其他方法

### 用户UserID追踪

需要在用户 创建 登录 切换账号后调用
```objective-c

[NGAAppEvents.sharedInstance refreshCustomerUser];

```

即可完成用户UserID的追踪统计和刷新(需集成NGALoginSDK).


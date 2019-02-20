# 卸载追踪​

在`AppDelegate.m`的`application:didFinishLaunchingWithOptions:`方法中添加AF通知选项, 代码如下:

```objectivec
//如果游戏本身不需要通知的话, usePushNotification参数请设置为NO
[[NGAAppEvents sharedInstance] afAddUninstallNotificationWithApplication:application withOptions:launchOptions usePushNotification:YES];
```

并添加相关函数注册通知:

```objectivec
//注册af的卸载功能通知
- (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken {
    [[NGAAppEvents sharedInstance] afRegisterUninstall:deviceToken];
}
```


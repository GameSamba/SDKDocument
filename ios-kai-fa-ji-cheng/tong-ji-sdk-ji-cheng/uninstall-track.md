# 卸载追踪​

首先确保证书支持推送.

![Xnip2019-08-12_15-17-39](/Users/n1/Code/Git/SDKDocument/.gitbook/assets/Xnip2019-08-12_15-17-39.png)



其次, 如果是使用静默推送, 还需要在***Background Modes*** 勾选  ***Remote notifications***

![Xnip2019-08-12_15-15-55](/Users/n1/Code/Git/SDKDocument/.gitbook/assets/Xnip2019-08-12_15-15-55.png)





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



测试卸载:

必须在TestFlight环境下测试, 配置 NGAConfig 代码为:

```objectivec
config.useUninstallSandbox = YES;
```





Note:

安装和卸载之间无需等待时间间隔。可以安装应用后并立即卸载。

但是在后台面板上查看实际卸载可能需要最多9天的等待时间。此外，卸载日期是实际卸载日期后的9天。

iOS卸载事件数据取决于Apple推送通知服务（APN）。出于隐私考虑，APN不会在用户立即删除应用时报告。自2019年2月26日起，APN仅在安装后8天内返回卸载结果。从第8天开始，所有卸载数据都可用。
# iOS

## 文件说明:

* Assets
  * Editor
    * SDKStart.cs        //导出至Xcode工程的脚本文件, 包括对info.plist capability framework等工程文件的添加和修改
  * Plugin
    * NGASDK.cs      //SDK函数注册文件,封装了SDK的函数接口在内
    * NGASDKCallbacks.cs   //回调函数文件, 包括SDK的登录分享等方法等函数回调在内, 需要进行进一步的实现处理
    * iOS
      * NGASDKAppController.mm    //导出至Xcode工程时, Unity会使用此AppController. 如果您的项目使用其他自定义的Apptroller, 请注意合并相关代码
      * NGASDKDelegate\*         //OC代码的登录和购买代理注册对象
      * NGASDKWrapper\*          //将 SDK的OC使用代码按照C语言进行编译

## SDK初始化及启动

#### iOS:

SDK通过`NGASDKAppController.mm`中`- (BOOL)application:didFinishLaunchingWithOptions:`内的方法进行SDK的初始化工作, 其中需要注意和配置的config属性包括 `appsFlyerDevKey` `appleAppID` `appKey` 分别为appsflyer的key , Apple App ID, 统计SDK的key\(统计SDK的key格式为"gamesamba-"+游戏ID\)

其次是通过C\#代码完成SDK的代理对象设置及商品初始化的工作.如下:

```text
    void Start()
    {
#if UNITY_IOS
        string[] array = { "shop.item.001", "shop.item.002", "shop.item.003" }; //配置商品ID列表
        NGASDK.shopDelegate(array);          //设置商品代理对象及初始化
        NGASDK.loginDelegate();                    //设置登录代理对象
#elif UNITY_ANDROID


#endif
    }

        //完成登录后需要配置相关参数
    void AfterLoginMethod()
    {
#if UNITY_IOS
        NGASDK.setRoleName("unknown");    //需要配置角色名
        NGASDK.setServerID("1001");            //需要配置服务器ID
        NGASDK.setServerName("Test");        //需要配置服务器名称

      //设置悬浮窗的显示坐标.x,y均为0,则显示在默认位置. 如果设置在其他坐标, 则注意避开iPhone的刘海区域.
      //openShare    显示悬浮窗的分享按钮, 分享等具体功能需要实现NGASDKDelegate.mm中的share方法
      //openFeedback 显示support支援网页
      //openDiscord  显示打悬浮窗的Discord按钮, 更新Discord的URL使用NGASDK.cs中的setDiscordURL方法
        NGASDK.ngaDragViewWithPoint(0, 0, isOpenShare, isOpenFeedback, isOpenDiscord);    
#elif UNITY_ANDROID


#endif
    }
```

### SDKStart.cs配置说明

**iOS部分:**

需要配置`ngaGameID`\(游戏ID\) ,`facebookAppid` \(Facebook提供的App ID\)

以及根据是否使用通知功能设置标志位参数`userNotification`.

**开启通知**: 在`SDKStart.cs`的代码中调配置`userNotification`标志位参数为true, 同时在`NGASDKAppController.mm` 的`application: didFinishLaunchingWithOptions:`方法中

```text
[[NGAAppEvents sharedInstance] afAddUninstallNotificationWithApplication:application 
                                                             withOptions:launchOptions              
                                                     usePushNotification:YES]
```

`usePushNotification`的标志位也设置为YES

否则, 则以上参数分别设置为false和NO.


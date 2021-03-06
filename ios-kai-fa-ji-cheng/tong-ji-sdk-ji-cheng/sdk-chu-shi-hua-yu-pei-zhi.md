# SDK初始化与配置

## 1. 在AppDelegate文件中配置初始化代码

**导入头文件** `#import <NGALoginSDK/NGALoginSDK.h>` , **在项目中添加GoogleService-Info.plist文件**

在`- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions` 方法中配置如下代码:

```objectivec
//启动FB, 在集成登录SDK的情况下, 此行代码跳过
//[[NGAAppEvents sharedInstance] fbApplication:application didFinishLaunchingWithOptions:launchOptions];

//配置Google Firebase, 需要在项目中添加GoogleService-Info.plist文件
[[NGAAppEvents sharedInstance] gaConfigure];

//配置启动配置的相关参数
NGAConfig* config = NGAConfig.new;
config.appsFlyerDevKey = @"bLmWavMFiw4tAwxcewWnfQ8g";    //AppsFlyer的key
config.appleAppID = @"123456789";                     //Apple的Appid
config.appKey = @"gs-99";                               //游戏id
config.enableAddIDFA = YES;                            //开启IDFA追踪
[[NGAAppEvents sharedInstance] startWithConfig:config];
[[NGAAppEvents sharedInstance] registerActiveSDK];
```

### 配置如下代码:

```objectivec
// Report Push Notification attribution data for re-engagements
- (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult))completionHandler {
    [[NGAAppEvents sharedInstance] afHandlePushNotification:userInfo];
}

- (BOOL)application:(UIApplication *)application continueUserActivity:(NSUserActivity *)userActivity restorationHandler:(void (^)(NSArray *_Nullable))restorationHandler{
    [[NGAAppEvents sharedInstance] afContinueUserActivity:userActivity restorationHandler:restorationHandler];
    return YES;
}
```

### 实现openURL方法

```objectivec
// Reports app open from deeplink for iOS 8 or below (DEPRECATED)
- (BOOL)application:(UIApplication *)application openURL:(NSURL *)url sourceApplication:(NSString*)sourceApplication annotation:(id)annotation{
    [[NGAAppEvents sharedInstance] afHandleOpenURL:url sourceApplication:sourceApplication withAnnotation:annotation];
    return YES;
}

// Reports app open from deeplink for iOS 9+
- (BOOL)application:(UIApplication *)application openURL:(NSURL *)url
            options:(NSDictionary *) options{
    [[NGAAppEvents sharedInstance] afHandleOpenURL:url options:options];

    //如果配置了登录SDK的openURL方法, 则此行代码跳过
    //[[NGAAppEvents sharedInstance] fbApplication:application openURL:url options:options];
    return YES;
}
```

## 2. Info.plist文件配置

**配置登录SDK后, 此步骤跳过**

![](../../.gitbook/assets/tu-pian-1.png)SourceCode下为:

```markup
<array>
  <dict>
    <key>CFBundleURLSchemes</key>
    <array>
      <string>fb820076274792945</string>
    </array>
  </dict>
</array>
<key>FacebookAppID</key>
<string>820076274792945</string>
<key>FacebookDisplayName</key>
<string>NGamesDemo</string>
```

**至此, SDK初始化完成.**


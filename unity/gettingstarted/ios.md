# iOS

## 部分文件说明:

* Assets
  * GameSambaSDK
    * SDK
      * Editor
        * GameSambaiOSConfigurator.cs        //导出至Xcode工程的脚本文件, 包括对info.plist capability framework等工程文件的添加修改
    * Plugin
      * iOS
        * NGASDKAppController.mm    //导出至Xcode工程时, Unity会使用此AppController. 如果您的项目使用其他自定义的Apptroller, 请注意合并相关代码
        * NGASDKDelegate\*         //OC代码的登录和购买代理注册对象
        * NGASDKWrapper\*          //将 SDK的OC使用代码按照C语言进行编译

## SDK初始化及启动

Unity相关代码不再赘述, 参考 [例子](https://github.com/GameSamba/SDKDocument/tree/7505a377da49971fcaa1f521d93f240c65a4c496/unity/gettingstarted/li-zi.md)中的说明进行SDK的初始化及后续步骤.

### 部分说明如下:

* 如果集成Apple登录, 在Unity导出Xcode工程后, 请手动在`Capability`中添加`Sign In with Apple`.
* Unity的Player Settings中需配置好`Bundle identifier`, `GameSambaiOSConfigurator.cs`脚本启动时会获取此项值并写入到相关的Xcode工程文件中.
* Firebase相关:脚本会拷贝固定路径的`Assets/Plugins/iOS/GoogleService-Info.plist`至Xcode工程中, 导出时请确保此文件存在
* 悬浮窗相关的`SetPopPosition`方法也可以不调用, 默认位置是显示在左下角, 自定义位置时注意避开iPhone的刘海区域.

### 导出至iOS工程后, 启动Xcode时:

Xcode工程通过`NGASDKAppController.mm`中`- (BOOL)application:didFinishLaunchingWithOptions:`内的方法进行初始化工作, 其他的诸如`OpenURL` `BecomeActive`等方法也包括在内此文件内.

如果自定义AppViewController, 请合并相关代码, 并重新设置宏`IMPL_APP_CONTROLLER_SUBCLASS`


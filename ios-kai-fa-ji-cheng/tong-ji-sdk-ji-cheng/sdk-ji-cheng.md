# SDK集成

如下图所示, 添加相应的库文件

![](../../.gitbook/assets/iShot2020-04-2314.30.14.png)

包括

> NGACountSDK.framework
>
> AdSupport.framework \(系统库\)
>
> iAd.framework \(系统库\)
>
> SystemConfiguration.framework \(系统库\)
>
> Accelerate.framework \(系统库\)
>
> libc++.tbd \(系统库\)
>
> AppsFlyerLib.framework
>
> FBSDKCoreKit.framework \(登录SDK同样也包含\)
>
> FIRAnalyticsConnector.framework
>
> FirebaseAnalytics.framework
>
> FirebaseCore.framework
>
> FirebaseCoreDiagnostics.framework
>
> FirebaseInstallations.framework
>
> GoogleAppMeasurement.framework
>
> GoogleDataTransport.framework
>
> GoogleDataTransportCCTSupport.framework
>
> GoogleUtilities.framework
>
> PromisesObjC.framework
>
> nanopb.framework

## 并在Build Settings设置如下参数:

![](../../.gitbook/assets/snipaste_2018-05-03_11-50-51.png)

注意拼写为: **-ObjC**


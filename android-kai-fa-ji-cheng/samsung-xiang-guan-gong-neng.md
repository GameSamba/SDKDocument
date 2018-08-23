# Samsung 支付

**Note**: SDK中使用三星IAP 5.0版本

## 商品类型

1. 物品（可消耗，不可消耗）
2. 订购（无自动订购（NRS），自动订购）

## 接入要求

* 支持Android API 14及以上版本，在更早版本上无法正常运行
* 需要Galaxy Apps商店 4.2.13.xx 版本或以上

## 购买流程

请按以下步骤测试购买流程： 

1 在主页面上点击Purchase One Item .验证三星账号页面出现。

2 输入三星账号密码并点击确认

3 支付页面出现，可以选择支付方式

4 点击选择需要的支付方式 

5 点击Buy 开始IAP支付流程

## 关于测试

{% hint style="info" %}
 IAP支持封闭beta测试，用户可以从Galaxy Apps下载并购买商品。在BETA测试中，注册阶段的内容可 以被浏览，购买，消耗，真实交易付款或者测试交易。

 更多信息请参考三星开发者网站: \(http://developer.samsung.com/iap/how-to-start\).
{% endhint %}

## 权限和组件

在 `AndroidManifest.xml` 中加入以下配置:

```markup
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
       package="您的应用包名">

    <!-- 权限声明 -->
    <!--三星商店权限-->
    <uses-permission android:name="com.samsung.android.iap.permission.BILLING"/>

    <application
        ...>
        <!-- 三星商店 IAP Activity ↓↓↓-->
        <!--发起支付请求-->
        <activity
            android:name="com.samsung.android.sdk.iap.lib.activity.PaymentActivity"
            android:theme="@style/Theme.Empty"
            android:configChanges="orientation|screenSize"/>
        <!--请求商品列表-->
        <activity
            android:name="com.samsung.android.sdk.iap.lib.activity.ProductActivity"
            android:theme="@style/Theme.Empty"
            android:configChanges="orientation|screenSize"/>
        <!--请求已购物品列表-->
        <activity
            android:name="com.samsung.android.sdk.iap.lib.activity.OwnedProductActivity"
            android:theme="@style/Theme.Empty"
            android:configChanges="orientation|screenSize"/>
        <!--请求已购物品的消耗情况-->
        <activity
            android:name="com.samsung.android.sdk.iap.lib.activity.ConsumePurchasedItemsActivity"
            android:theme="@style/Theme.Empty"
            android:configChanges="orientation|screenSize"/>
        <!-- 三星商店 IAP Activity ↑↑↑-->
    </application>
</manifest>

```

{% hint style="danger" %}
 1.必须要配置权限  `com.samsung.android.iap.permission.BILLING` ，用于链接三星IAP

 2. 四个activities必须为透明背景，需设置 `android:theme="@style/Theme.Empty"`. 否则会覆盖原本的应用。
{% endhint %}

## 初始化 {#chu-shi-hua}

#### 在主Activity\#onCreate初始化 {#zai-zhu-activityoncreate-chu-shi-hua}

```java
private SamsungBillingSupport mSamsungBillingSupport;
...
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    ...
    //初始化三星商店内购
    mSamsungBillingSupport = SamsungBillingSupport.getInstance(this, new BillingCallback() {
        @Override
        public void onPurchased(String productId, String orderId) {
            //购买成功
        }
    
        @Override
        public void onBillingInitialized() {
        
        }
        
        @Override
        public void onError(int errorCode) {
            //购买失败
        }
    });
}
```

> #### API原型 {#api-yuan-xing-1}

```java
/**
 * 初始化三星商店内购实例
 * @param activity        当前Activity
 * @param billingCallback 购买回调
 * @return
 */
public static SamsungBillingSupport getInstance(Activity activity, BillingCallback billingCallback)
```

> #### 参数 {#can-shu-1}

* Activity activity ：当前Activity
* BillingCallback billingCallback : 购买回调

## 设置调试模式 {#ji-lu-tong-ji-shi-jian}

> #### API介绍 {#api-jie-shao}

设置三星商店内购调试模式

> #### API原型 {#api-yuan-xing-2}

```java
/**
 * 设置三星商店调试模式
 * @param isDebug
 */
public void setDebugMode(boolean isDebug)
```

> #### 示例 {#shi-li}

```java
//设置三星商店调试模式
mSamsungBillingSupport.setDebugMode(true);
```

{% hint style="info" %}
调试模式下，内购为测试订单。
{% endhint %}

{% hint style="danger" %}
打包发布前，测试完成，务必将调试模式设置为false 

请注意：下图中的弹窗出现时，说明该应用仍在 **测试模式** 下：

![](blob:https://gamesamba.gitbook.io/226c1cbe-210e-4592-9856-e5ba1c9aa02a)![](blob:https://gamesamba.gitbook.io/953fad3c-8583-45f9-bb59-9925cb7b1891)
{% endhint %}

## 购买商品 {#ji-lu-tong-ji-shi-jian}

> #### API介绍 {#api-jie-shao}

购买三星商店内购商品

> #### API原型 {#api-yuan-xing-2}

```java
/**
 * 购买商品
 * @param itemId 商品ID
 * @param userId 用户ID
 * @param userName 用户角色名称
 * @param serverId 服务器ID
 * @param serverName 服务器名称
 */
public void purchase(String itemId, String userId, String userName, String serverId, String serverName)
```

> #### 示例 {#shi-li}

```java
String itemId = "ipa.tg.na002";//商品ID
String userId = "1";//用户ID
String userName = "test";//用户名称
String serverId = "1";//服务器ID
String serverName = "test";//服务器名称
//购买商品
mSamsungBillingSupport.purchase(itemId, userId, userName, serverId, serverName);
```




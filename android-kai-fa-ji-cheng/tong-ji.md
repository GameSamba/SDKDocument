---
description: 统计功能
---

# 统计

帮助产品上报自定义行为事件。

{% hint style="info" %}
如果游戏需要接入统计功能，需要额外导入GamesabaAnalysis的Sdk，并且按照步骤接入。
{% endhint %}

## 配置FireBase，下载

1.添加、配置应用到Firebase（[控制台](https://console.firebase.google.com/)）（由产品人员进行配置）

2.下载 `google-services.json` 文件， 复制到项目的模块文件夹（通常是 `app/`），请执行此操作。

## Gradle集成

在SDK文件下的 `附件/libs`目录下存以下的文件：

1. gamesamba-analytics-sdk-3.3.5.aar（GameSamba 统计SDK）

将以上这个aar文件导入到主工程`libs` 目录下

### 配置主工程的  build.gradle

在主工程的 build.gradle 文件中 dependencies下，添加依赖即可。

```java
dependencies {
    ...

    // 统计功能SDK (必需)
    compile(name: 'gamesamba-analytics-sdk-3.3.5', ext: 'aar')
    // Appsflyer模块
    compile 'com.appsflyer:af-android-sdk:4.8.14@aar'
    compile 'com.android.installreferrer:installreferrer:1.0'
    // Google FireBase模块
    compile 'com.google.firebase:firebase-core:11.0.4'
    compile 'com.google.firebase:firebase-messaging:11.0.4'
}
```

**Note**: 如果你使用 `Gradle 3.0.0 或者更高版本`, 务必使用 `implementation` 关键字替代 `compile` 如下:

```java
dependencies {
    ...

    // 统计功能SDK (必需)
    implementation(name: 'gamesamba-analytics-sdk-3.3.5', ext: 'aar')
    // Appsflyer模块
    implementation 'com.appsflyer:af-android-sdk:4.8.14@aar'
    implementation 'com.android.installreferrer:installreferrer:1.0'
    // Google FireBase模块
    implementation 'com.google.firebase:firebase-core:11.0.4'
    implementation 'com.google.firebase:firebase-messaging:11.0.4'
}
```

## 

## 权限和组件

在 `AndroidManifest.xml` 中加入以下配置:

```markup
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
       package="您的应用包名">
   ...

    <application
        ...>
        ...
        <!--Appsflyer Key，接入统计SDK需要-->
        <meta-data
            android:name="com.ngames.analytics.AppsflyerKey"
            android:value="@string/appsflyer_key" />

        <!--Google统计,发送者ID，接入统计SDK需要，AF卸载事件也需要-->
        <meta-data
            android:name="com.ngames.analytics.GoogleSenderId"
            android:value="@string/google_sender_id" />

        <!--货币代码，例如： USD（美元），接入统计SDK需要-->
        <meta-data
            android:name="com.ngames.analytics.CurrencyCode"
            android:value="@string/currency_code" />

        <!-- Appsflyer广播接收器 -->
        <receiver 
            android:name="com.appsflyer.MultipleInstallBroadcastReceiver" 
            android:exported="true">
            <intent-filter>
                <action android:name="com.android.vending.INSTALL_REFERRER" />
            </intent-filter>
        </receiver>
        
        <!-- Appsflyer 追踪卸载服务-->
        <service
            android:name="com.appsflyer.FirebaseInstanceIdListener">
            <intent-filter>
                <action android:name="com.google.firebase.INSTANCE_ID_EVENT" />
            </intent-filter>
        </service>
    </application>
</manifest>
```

{% hint style="info" %}
请配置对应节点下面的内容
{% endhint %}

在 `res/values` 中配置`string.xml`， 配置如下 :

```markup
<!--统计模块-->
<!--Appflyer的KEY，请将 appsflyer_key 替换为自己的Appflyer的KEY-->
<string name="appsflyer_key">appsflyer_key</string>
<!--货币代码，例如： USD（美元）-->
<string name="currency_code">USD</string>
<!--统计模块，谷歌卸载，发送者ID-->
<string name="google_sender_id">google_sender_id</string>
```

{% hint style="danger" %}
接入统计必须配置以上配置：

1.Appsflyer配置：

（1）appsflyer\_key

2.货币代码：

（1）currency\_code

3.统计模块，谷歌卸载，发送者ID

（1）google\_sender\_id
{% endhint %}

## 混淆配置

如果你的apk最终会经过代码混淆，请在proguard配置文件中额外再加入以下代码:

```groovy
-dontwarn com.android.installreferrer

-keep class com.appsflyer.** { *; }
-dontwarn com.appsflyer.**
-keep public class com.google.firebase.iid.FirebaseInstanceId {
    public *;
}
```

## 初始化

### （1）Application

#### 在项目中的Application\#onCreate初始化 <a id="src-cnt-0-0"></a>

```java
//是否是调试模式
private boolean isDebug = false;
...
@Override
protected void onCreate() {
    super.onCreate();
    ...
    //初始化统计SDK
    NgamesAnalyticsSdk.init(this, isDebug);
}
```

> #### API原型

```java
/**
 * 初始化
 * @param application
 * @param isDebug      调试模式
 */
public static void init(Application application, boolean isDebug)
```

> #### 参数

* Application application ：应用的 Application
* boolean isDebug ：调试模式

{% hint style="info" %}
如果接入统计功能，第一步必须在 Application 初始化
{% endhint %}

### （2）Activity

#### 在主Activity\#onCreate初始化 <a id="src-cnt-0-0"></a>

```java
private NgamesAnalyticsSdk ngamesAnalyticsSdk;
...
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    ...
    //初始化Ngames统计SDK
    ngamesAnalyticsSdk = NgamesAnalyticsSdk.getInstance(this);
}
```

> #### API原型

```java
/**
 * 初始化SDK
 * @param activity 当前Activity
 * @return NgamesAnalyticsSdk
 */
public static NgamesAnalyticsSdk getInstance(Activity activity)
```

> #### 参数

* Activity activity ：当前Activity

## 记录统计事件

> #### API介绍

记录统计事件

> #### API原型

```java
/**
 * 记录统计事件
 * @param eventName   事件名称，注意：应用内事件名称长度不得超过 45 个字符
 * @param eventValues 记录内容（字典）
 */
public void recordEvent(String eventName, HashMap eventValues)
```

> #### 示例

```java
//记录事件
HashMap<String, Float> map = new HashMap<>();
map.put("goods_id", 1);
map.put("goods_count", 10);
ngamesAnalyticsSdk.recordEvent("purchase", map);
```

## 记录购买事件

> #### API介绍

追踪购买事件

> #### API原型

```java
/**
 * 追踪购买事件
 * @param itemId       商品ID
 * @param itemType     商品类型
 * @param revenue      收入
 * @param currencyCode 货币单位（ISO 4217 代码），例如"USD","HKD","CNY","TWD"等，更多参考https://www.xe.com/iso4217.php
 * @param serverID     服务器ID
*/
public void recordPurchaseEvent(String itemId, String itemType, float revenue, String currencyCode, String serverID)
```

> #### 示例

```java
String itemId = "good1";//商品ID
String itemType = "good";//商品类型
float revenue = 2.99f;//商品价格
String currencyCode = "USD";//货币单位
String serverID = "1";//服务器ID
ngamesAnalyticsSdk.recordPurchaseEvent(itemId, itemType, revenue, currencyCode, serverID);
```

## 记录谷歌统计事件

> #### API介绍

记录谷歌统计事件

> #### API原型

```java
/**
 * 记录GoogleAnalysis事件
 * @param eventName 事件名称
 * @param params    事件统计参数
 */
public void recordGAEvent(String eventName, Map<String, String> params)
```

> #### 示例

```java
//记录事件：Google Analytics
String eventName = "level";
Map<String, String> params = new HashMap<>();
params.put("up", "1");
ngamesAnalyticsSdk.recordGAEvent(eventName, params);
```

## 设置用户ID

> #### API介绍

设置用户ID，便于统计平台统计

> #### API原型

```java
/**
 * 设置客户用户ID
 * 可以帮助您交叉引用自己的独有 ID 以及 AppsFlyer 的独有 ID 和其他设备的 ID。该 ID 与回传 IP 一同出现在 AppsFlyer CSV 报告中，用于与您的内部 ID 交叉引用。
 * @param userId 用户ID
 */
public void setUserId(String userId)
```

> #### 示例

```java
//设置用户ID
ngamesAnalyticsSdk.setUserId("100");
```

{% hint style="info" %}
注意：此方法需要在登录成功的回调中，进行设置
{% endhint %}

## 记录AF卸载事件

需要配置对应的（参考 本页开始的配置）：

1. `AndroidManifest.xml`中`meta-data`的`com.ngames.analytics.GoogleSenderId`
2. `AndroidManifest.xml`中`service`的 `com.appsflyer.FirebaseInstanceIdListener`
3. `res/values` 中配置`string.xml` 的 `google_sender_id`


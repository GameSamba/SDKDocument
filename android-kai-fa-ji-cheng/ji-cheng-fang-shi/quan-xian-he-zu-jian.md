# 权限和组件

## 权限和组件

在 `AndroidManifest.xml` 中加入以下配置:

```markup
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
       package="您的应用包名">

    <!-- 权限声明 -->
    <!-- 访问网络状态-->
    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
    <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
	 <!-- 多媒体相关 -->
	<uses-permission android:name="android.permission.READ_PHONE_STATE" />
    <!-- 在SDCard中创建与删除文件权限 -->
    <uses-permission android:name="android.permission.MOUNT_UNMOUNT_FILESYSTEMS" />
	<!-- 外置存储存取权限 -->
	<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
    <!-- WindowsManager -->
    <uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />
    <uses-permission android:name="android.permission.GET_ACCOUNTS" />
   
    <!-- bugly -->
    <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
    <uses-permission android:name="android.permission.READ_LOGS" />
    <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />

    <uses-permission android:name="com.android.vending.BILLING" />

    <application
        android:networkSecurityConfig="@xml/network_security_config"
        ...>
        <!-- 游戏对应ID：需要配置 -->
		<meta-data
            android:name="com.ngames.sdk.AppId"
            android:value="@string/ngames_app_id" />
        <!--Google 服务器ClientId-->
        <meta-data
            android:name="com.ngames.sdk.GoogleServerClientId"
            android:value="@string/google_server_client_id" />
        <!--悬浮窗：Discord网站-->
        <meta-data
            android:name="com.ngames.sdk.Discord"
            android:value="@string/pop_discord" />
		<!-- Facebook的应用ID：需要配置Facebook控制台获取 -->
        <meta-data
            android:name="com.facebook.sdk.ApplicationId"
            android:value="@string/facebook_app_id" />
		<!-- Facebook的应用名称 -->
        <meta-data
            android:name="com.facebook.sdk.ApplicationName"
            android:value="@string/facebook_app_name" />
		<!-- Google服务的应用ID -->
        <meta-data
            android:name="com.google.android.gms.games.APP_ID"
            android:value="@string/app_id" />
		<!-- Google服务的应用版本 -->
        <meta-data
            android:name="com.google.android.gms.version"
            android:value="@integer/google_play_services_version" />

		<!-- SDK登录模块需要集成的 -->
		<activity
            android:name="com.ngames.game321sdk.AccountManagementActivity"
            android:configChanges="fontScale|orientation|keyboardHidden|locale|navigation|screenSize|uiMode"
            android:screenOrientation="behind"
            android:theme="@style/ToolTipTheme"/>

        <activity
            android:name="com.ngames.game321sdk.ReplaceAccountActivity"
            android:configChanges="fontScale|orientation|keyboardHidden|locale|navigation|screenSize|uiMode"
            android:screenOrientation="behind"
            android:theme="@android:style/Theme.NoTitleBar.Fullscreen" />

        <activity
            android:name="com.ngames.game321sdk.LoginActivity"
            android:configChanges="fontScale|orientation|keyboardHidden|locale|navigation|screenSize|uiMode"
            android:screenOrientation="behind"
            android:theme="@style/ngames_dialog"
            android:windowSoftInputMode="stateAlwaysHidden|adjustPan" />

        <activity
            android:name="com.ngames.game321sdk.SupportActivity"
            android:configChanges="fontScale|orientation|keyboardHidden|locale|navigation|screenSize|uiMode"
            android:screenOrientation="behind"
            android:windowSoftInputMode="stateAlwaysHidden|adjustPan" />
			
        <!-- Facebook相关的 -->
		<!-- Facebook进程间通信provider，请配置string.xml中的facebook_provider_authorities -->
        <provider
            android:name="com.facebook.FacebookContentProvider"
            android:authorities="@string/facebook_provider_authorities"
            android:exported="true" />
        <activity
            android:name="com.facebook.FacebookActivity"
            android:configChanges="keyboard|keyboardHidden|screenLayout|screenSize|orientation"
            android:label="@string/facebook_app_name" />
        <activity
            android:name="com.facebook.CustomTabActivity"
            android:exported="true">
            <intent-filter>
                <action android:name="android.intent.action.VIEW" />
                <category android:name="android.intent.category.DEFAULT" />
                <category android:name="android.intent.category.BROWSABLE" />
                <data android:scheme="@string/fb_login_protocol_scheme" />
            </intent-filter>
        </activity>
    </application>
</manifest>

```

{% hint style="danger" %}
以上`AndroidManifest.xml` 文件中配置的 &lt;activity&gt; 节点内必须配置为android:screenOrientation="behind"
{% endhint %}

### 

### 请配置对应节点下面的内容

在 `res/values` 中配置`string.xml`， 配置如下 :

```markup
<!--游戏的ID，请将 ngames_game_id 替换为自己的游戏ID-->
<string name="ngames_app_id">ngames_game_id</string>
<!--Google 服务器ClientId-->
<string name="google_server_client_id">google_server_client_id</string>
<!--Facebook的应用ID， 请将 facebook_app_id 替换为自己的 Facebook应用ID-->
<string name="facebook_app_id">facebook_app_id</string>
<!--Facebook的应用协议：fb{Facebook应用ID}, 请将 123456 替换为自己的 Facebook应用ID-->
<string name="fb_login_protocol_scheme">fb123456</string>
<!--Facebook的应用名称，请将 app_name 替换为自己的应用名称 -->
<string name="facebook_app_name">app_name</string>
<!--Facebook的进程授权： com.facebook.app.FacebookContentProvider{Facebook应用ID}, 请将 123456 替换为自己的 Facebook应用ID -->
<string name="facebook_provider_authorities">com.facebook.app.FacebookContentProvider123456</string>
<!--Google游戏ID，请将 google_game_id 替换为自己的Google游戏ID-->
<string name="app_id">google_game_id</string>
<!--Google支付对应的PublicKey，请将 google_publickey 替换为自己的Google支付对应的PublicKey-->
<string name="base64EncodedPublicKey">google_publickey</string>
<!--悬浮框：Discord的URL-->
<string name="pop_discord">discord_url</string>
```

{% hint style="info" %}
1.ngames\_app\_id：由项目经理配置

2.google\_server\_client\_id：Google 服务器ClientId，用于谷歌登录（必须）

3.接入Facebook SDK必须配置：

（1）facebook\_app\_id

（2） fb\_login\_protocol\_scheme

（3） facebook\_app\_name

（4） facebook\_provider\_authorities

4.接入Google sdk必须配置：

（1）app\_id（ Google游戏ID）

5.base64EncodedPublicKey，Google支付的KEY非必须，可以通过代码设置

6.pop\_discord：悬浮框中Discord的URL
{% endhint %}

> google\_server\_client\_id

这个值在Google Console 后台查看 服务器客户端ID

### 

### 复制配置文件到指定目录

在SDK文件下的  `附件/res/xml`目录下存在`network_security_config.xml`文件放到接入项目的`/res/xml`目录下。

将以下代码加入到`AndroidManifest.xml` 的`application`节点下面：

```markup
android:networkSecurityConfig="@xml/network_security_config"
```

{% hint style="danger" %}
以上内容务必加上。因为使用targetSdkVersion的版本为28或者以上，Android 9.0的设备添加了网络权限的配置，如果不添加这个，HTTP协议将被拒绝访问，只能访问HTTPS。 
{% endhint %}






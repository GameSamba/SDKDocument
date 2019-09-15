# 例子

根据 [准备开始](gettingstarted.md) 教程后，加载配置GameSamba SDK。下一步可以尝试以下使用SDK的例子。

* [初始化SDK](li-zi.md#chu-shi-hua-sdk)
* [登录](li-zi.md#deng-lu)
* [分享到Facebook](li-zi.md#fen-xiang-dao-facebook)
* [内购](li-zi.md#nei-gou)
* [统计](li-zi.md#tong-ji)



### 初始化SDK

初始化SDK，并且设置相关配置，设置相关监听

```csharp
void Start()
{
    InitGameSambaSDK();
    RegisterEvents();
}

private void OnDestroy()
{
    UnRegisterEvents();
}

#region 初始化

public void InitGameSambaSDK()
{
    string[] array = { "ipa.aot.na003", "ipa.aot.na005", "ipa.aot.na004" };
    GameSambaSDK.InitializeSdk();
    GameSambaSDK.SetLanguage(GameSambaSDKLanguage.LANG_TW);
    GameSambaSDK.SetIAPItems(array);
    GameSambaSDK.SetDebug(true); //设置是否开启DEBUG
    GameSambaSDK.SetSupportAccount(true, true, true); //设置支持的帐号类型
    GameSambaSDK.SetSupportSwitchAccount(true); //设置是否支持帐号切换
    GameSambaSDK.SetPopPosition(PopDirection.Left, 0.3f); //设置悬浮框初始位置, iPhone注意避开刘海范围
    GameSambaSDK.SetPopSupportFunction(false, true, true); //设置悬浮功能开启
}

#endregion

#region 事件监听

//注册监听
private void RegisterEvents()
{
    //登录
    GameSambaEvents.onLoginSuccessEvent += LoginSuccessEvent; //登录成功
    GameSambaEvents.onLoginFailedEvent += LoginFailedEvent; //登录失败
    GameSambaEvents.onLoginCancelEvent += LoginCancelEvent; //登录取消
    //切换账号
    GameSambaEvents.onSwitchAccountEvent += SwitchAccountEvent; //切换账号成功
    //分享
    GameSambaEvents.onFacebookShareSuccessEvent += FacebookShareSuccessEvent; //分享成功
    GameSambaEvents.onFacebookShareFailedEvent += FacebookShareFailedEvent; //分享失败
    GameSambaEvents.onFacebookShareCancelEvent += FacebookShareCancelEvent; //分享取消
    //购买
    GameSambaEvents.onPurchaseSuccessEvent += PurchaseSuccessEvent; //购买成功
    GameSambaEvents.onPurchaseFailedEvent += PurchaseFailedEvent; //购买失败
}

//取消注册监听
private void UnRegisterEvents()
{
    //登录
    GameSambaEvents.onLoginSuccessEvent -= LoginSuccessEvent; //登录成功
    GameSambaEvents.onLoginFailedEvent -= LoginFailedEvent; //登录失败
    GameSambaEvents.onLoginCancelEvent -= LoginCancelEvent; //登录取消
    //切换账号
    GameSambaEvents.onSwitchAccountEvent -= SwitchAccountEvent; //切换账号成功
    //分享
    GameSambaEvents.onFacebookShareSuccessEvent -= FacebookShareSuccessEvent; //分享成功
    GameSambaEvents.onFacebookShareFailedEvent -= FacebookShareFailedEvent; //分享失败
    GameSambaEvents.onFacebookShareCancelEvent -= FacebookShareCancelEvent; //分享取消
    //购买
    GameSambaEvents.onPurchaseSuccessEvent -= PurchaseSuccessEvent; //购买成功
    GameSambaEvents.onPurchaseFailedEvent -= PurchaseFailedEvent; //购买失败
}

//事件回调：登录成功
private void LoginSuccessEvent(UserInfo loginUserInfo)
{
    Debug.Log("GameSamba : 登录成功");
    string showText = "";
    if (loginUserInfo != null)
    {
        showText = string.Format("登录成功 ： Id:{0} ; Name:{1}", loginUserInfo.GetId(), loginUserInfo.GetName());
    }
    else
    {
        showText = string.Format("登录成功 ： loginUserInfo == null");
    }

    consoleInput.text = showText;
    //登录成功后设置
    string roleName = "test"; //角色名称
    string serverId = "1"; //服务器ID
    string serverName = "test"; //服务器名称
    GameSambaSDK.SetRoleInfo(roleName);
    GameSambaSDK.SetServerInfo(serverId, serverName);
    GameSambaSDK.ShowPop();//显示悬浮框
}

//事件回调：登录失败
private void LoginFailedEvent(GameSambaError message)
{
    Debug.Log("GameSamba : 登录失败");
    string showText = string.Format("登录失败 ： Code:{0} ; Message:{1}", message.GetCode(), message.GetMessage());
    consoleInput.text = showText;
}

//事件回调：登录取消
private void LoginCancelEvent()
{
    Debug.Log("GameSamba : 登录取消");
    string showText = string.Format("登录取消");
    consoleInput.text = showText;
}

//事件回调：切换账号成功
private void SwitchAccountEvent(UserInfo userInfo)
{
    Debug.Log("GameSamba : 切换账号成功");
    string showText = "";
    if (userInfo != null)
    {
        showText = string.Format("切换账号成功 ： Id:{0} ; Name:{1}", userInfo.GetId(), userInfo.GetName());
    }
    else
    {
        showText = string.Format("切换账号成功 ： userInfo == null");
    }

    consoleInput.text = showText;
}

//事件回调：分享成功
private void FacebookShareSuccessEvent()
{
    Debug.Log("GameSamba : 分享成功");
    string showText = string.Format("分享成功");
    consoleInput.text = showText;
}

//事件回调：分享失败
private void FacebookShareFailedEvent(GameSambaError gameSambaError)
{
    Debug.Log("GameSamba : 分享失败");
    string showText = string.Format("分享失败 ： {0}", gameSambaError.GetMessage());
    consoleInput.text = showText;
}

//事件回调：分享取消
private void FacebookShareCancelEvent()
{
    Debug.Log("GameSamba : 分享取消");
    string showText = string.Format("分享取消");
    consoleInput.text = showText;
}


//事件回调：购买成功
private void PurchaseSuccessEvent(OrderInfo orderInfo)
{
    Debug.Log("GameSamba : 购买成功");
    string showText = "";
    if (orderInfo != null)
    {
        showText = string.Format("购买成功 . OrderId:{0} ; ItemId:{1}", orderInfo.GetOrderId(),
            orderInfo.GetItemId());
    }
    else
    {
        showText = string.Format("购买成功");
    }

    consoleInput.text = showText;
}

//事件回调：购买失败
private void PurchaseFailedEvent(GameSambaError gameSambaError)
{
    Debug.Log("GameSamba : 购买失败");
    string showText = string.Format("购买失败 : " + gameSambaError.GetMessage());
    consoleInput.text = showText;
}

#endregion
```



### 登录

根据登录类型，调用对应登录方法，通过登录回调处理登录结果。

```csharp
//游客登陆
public void OnBtnGuestLogin()
{
    GameSambaSDK.LoginGuest();
}

//Facebook登陆
public void OnBtnFacebookLogin()
{
    GameSambaSDK.LoginFacebook();
}

//Google登陆
public void OnBtnGoogleLogin()
{
    GameSambaSDK.LoginGoogle();
}

//GameSamba登录
public void OnBtnGameSambaLogin()
{
    GameSambaSDK.LoginGameSamba();
}

//GameCenter登录
public void OnBtnGameCenterLogin()
{
    GameSambaSDK.LoginGameCenter();
}
```



### 分享到Facebook

分享相关内容，通过分享结果回调，处理结果

```csharp
#region 分享

//分享Facebook链接
public void OnBtnShareFacebookLink()
{
    string shareLink = "http://tg.gamesamba.com";
    string quote = "这是一条引文";
    GameSambaSDK.ShareFacebookLink(shareLink, quote);
}

//分享Facebook图片
public void OnBtnShareFacebookImage()
{
    String imagePath = "/storage/emulated/0/game321/image.png";
    GameSambaSDK.ShareFacebookImage(imagePath);
}

#endregion
```



### 内购

内购商品，通过内购回调，获取内购结果

```csharp
//官方购买
public void OnBtnOfficialIAP()
{
#if UNITY_IPHONE
    string itemId = "ipa.aot.na003"; //商品ID
    GameSambaSDK.PurchaseApple(itemId);
#else
    string itemId = "ipa.tg.na002"; //商品ID
    GameSambaSDK.PurchaseGoogle(itemId);
#endif
}

//第三方内购
public void OnBtnThirdIAP()
{
    string itemId = "ipa.tg.na002"; //商品ID
    GameSambaSDK.PurchaseThird(itemId);
}
```



### 统计

统计相关事件

```csharp
#region 统计事件
//统计事件
public void OnBtnRecordEvent()
{
    string eventName = "Test";
    Dictionary<string, string> evetParams = new Dictionary<string, string>();
    evetParams.Add("id", "1");
    evetParams.Add("level", "1");
    GameSambaSDK.RecordEvent(eventName, evetParams);
}

//统计购买事件
public void OnBtnRecordPurchaseEvent()
{
    string itemId = "good1"; //商品ID
    string itemType = "good"; //商品类型
    float revenue = 2.99f; //商品价格
    string currencyCode = "USD"; //货币单位
    GameSambaSDK.RecordPurchaseEvent(itemId, itemType, revenue, currencyCode);
}

//统计谷歌事件
public void OnBtnRecordGAEvent()
{
    string eventName = "Test";
    Dictionary<string, string> evetParams = new Dictionary<string, string>();
    evetParams.Add("id", "1");
    evetParams.Add("level", "1");
    GameSambaSDK.RecordGAEvent(eventName, evetParams);
}

#endregion
```


# 设置监听

快速集成完成后，必须对对应的方法做监听，监控SDK回调状态。

## 登录

### 注册登录监听

在 **`Awake()`** 或者 **`Start()`** 生命周期方法中注册登录监听方法：

```csharp
//登录
GameSambaEvents.onLoginSuccessEvent += LoginSuccessEvent; //登录成功
GameSambaEvents.onLoginFailedEvent += LoginFailedEvent; //登录失败
GameSambaEvents.onLoginCancelEvent += LoginCancelEvent; //登录取消
```

### 取消监听

在 **`OnDestroy()`**  生命周期方法中取消登录监听方法：

```csharp
//登录
GameSambaEvents.onLoginSuccessEvent -= LoginSuccessEvent; //登录成功
GameSambaEvents.onLoginFailedEvent -= LoginFailedEvent; //登录失败
GameSambaEvents.onLoginCancelEvent -= LoginCancelEvent; //登录取消
```

### 监听方法

#### 登录成功

```csharp
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
}
```

#### 

#### 登录失败

```csharp
//事件回调：登录失败
private void LoginFailedEvent(GameSambaError message)
{
    Debug.Log("GameSamba : 登录失败");
    string showText = string.Format("登录失败 ： Code:{0} ; Message:{1}", message.GetCode(), message.GetMessage());
    consoleInput.text = showText;
}
```



#### 登录取消

```csharp
//事件回调：登录取消
private void LoginCancelEvent()
{
    Debug.Log("GameSamba : 登录取消");
    string showText = string.Format("登录取消");
    consoleInput.text = showText;
}
```



## 切换账号

### 注册监听

在 **`Awake()`** 或者 **`Start()`** 生命周期方法中注册监听方法：

```csharp
//切换账号
GameSambaEvents.onSwitchAccountEvent += SwitchAccountEvent; //切换账号成功
```

### 取消监听

在 **`OnDestroy()`**  生命周期方法中取消监听方法：

```csharp
//切换账号
GameSambaEvents.onSwitchAccountEvent -= SwitchAccountEvent; //切换账号成功
```

### 监听方法

#### 切换账号成功

```csharp
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
```



## Facebook分享

### 注册监听

在 **`Awake()`** 或者 **`Start()`** 生命周期方法中注册监听方法：

```csharp
//分享
GameSambaEvents.onFacebookShareSuccessEvent += FacebookShareSuccessEvent; //分享成功
GameSambaEvents.onFacebookShareFailedEvent += FacebookShareFailedEvent; //分享失败
GameSambaEvents.onFacebookShareCancelEvent += FacebookShareCancelEvent; //分享取消
```

### 取消监听

在 **`OnDestroy()`**  生命周期方法中取消监听方法：

```csharp
//分享
GameSambaEvents.onFacebookShareSuccessEvent -= FacebookShareSuccessEvent; //分享成功
GameSambaEvents.onFacebookShareFailedEvent -= FacebookShareFailedEvent; //分享失败
GameSambaEvents.onFacebookShareCancelEvent -= FacebookShareCancelEvent; //分享取消
```

### 监听方法

#### 分享成功

```csharp
//事件回调：分享成功
private void FacebookShareSuccessEvent()
{
    Debug.Log("GameSamba : 分享成功");
}
```



#### 分享失败

```csharp
 //事件回调：分享失败
private void FacebookShareFailedEvent(GameSambaError gameSambaError)
{
    string showText = string.Format("GameSamba : 分享失败 ： {0}", gameSambaError.GetMessage());
    Debug.Log(showText);
}
```



#### 分享取消

```csharp
//事件回调：分享取消
private void FacebookShareCancelEvent()
{
    Debug.Log("GameSamba : 分享取消");
}
```



## 购买

### 注册监听

在 **`Awake()`** 或者 **`Start()`** 生命周期方法中注册监听方法：

```csharp
//购买
GameSambaEvents.onPurchaseSuccessEvent += PurchaseSuccessEvent; //购买成功
GameSambaEvents.onPurchaseFailedEvent += PurchaseFailedEvent; //购买失败
```

### 取消监听

在 **`OnDestroy()`**  生命周期方法中取消监听方法：

```csharp
//购买
GameSambaEvents.onPurchaseSuccessEvent -= PurchaseSuccessEvent; //购买成功
GameSambaEvents.onPurchaseFailedEvent -= PurchaseFailedEvent; //购买失败
```

### 监听方法

#### 购买成功

```csharp
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
```



#### 购买失败

```csharp
//事件回调：购买失败
private void PurchaseFailedEvent(GameSambaError gameSambaError)
{
    Debug.Log("GameSamba : 购买失败");
    string showText = string.Format("购买失败 : " + gameSambaError.GetMessage());
    consoleInput.text = showText;
}
```




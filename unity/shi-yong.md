# 快速集成

完成Unity SDK的接入工作后，调用以下方法。

## 初始化

### 初始化SDK

```csharp
GameSambaSDK.InitializeSdk();
```



## 设置

### 设置语言

> #### API

```csharp
GameSambaSDK.SetLanguage(string language);
```

> #### 参数

| 参数 | 类型 | 必须 | 描述 |
| :--- | :--- | :--- | :--- |
| language | **string** | 是 | 语言 |

> #### language 参数说明

相关类 `GameSambaSDKLanguage` ：

| 语言（lang） | 描述 |
| :--- | :--- |
| LANG\_EN | 英文 |
| LANG\_CN | 简体中文 |
| LANG\_TW | 繁体中文 |
| LANG\_FR | 法文 |
| LANG\_TH | 泰文 |
| LANG\_KO | 韓文 |

> #### 例子

```csharp
GameSambaSDK.SetLanguage(GameSambaSDKLanguage.LANG_TW);
```



### 设置Debug模式

> #### API

```csharp
GameSambaSDK.SetDebug(bool isDebug);
```

> #### 参数

| 参数 | 类型 | 必须 | 描述 |
| :--- | :--- | :--- | :--- |
| isDebug | **bool** | 是 | 是否是Debug模式 |

> #### 例子

```csharp
GameSambaSDK.SetDebug(true);
```



### 设置支持的帐号类型

> #### API

```csharp
GameSambaSDK.SetSupportAccount(bool isSupportGamesamba, bool isSupportGoogle, bool isSupportFacebook);
```

> #### 参数

| 参数 | 类型 | 必须 | 描述 |
| :--- | :--- | :--- | :--- |
| isSupportGamesamba | **bool** | 是 | 是否支持Gamesamba登录 |
| isSupportGoogle | **bool** | 是 | 是否支持Google登录 |
| isSupportFacebook | **bool** | 是 | 是否支持Facebook登录 |

> #### 例子

```csharp
GameSambaSDK.SetSupportAccount(false, true, true);
```



### 设置是否支持切换帐号（默认开启）

> #### API

```csharp
GameSambaSDK.SetSupportSwitchAccount(bool isSupport);
```

> #### 参数

| 参数 | 类型 | 必须 | 描述 |
| :--- | :--- | :--- | :--- |
| isSupport | **bool** | 是 | 是否支持账号切换 |

> #### 例子

```csharp
GameSambaSDK.SetSupportSwitchAccount(true);
```



### 设置内购商品列表（iOS需要）

> #### API

```csharp
GameSambaSDK.SetIAPItems(string[] itemsIDArray);
```

> #### 参数

| 参数 | 类型 | 必须 | 描述 |
| :--- | :--- | :--- | :--- |
| itemsIDArray | **string\[\]** | 是 | 内购商品ID数组 |

> #### 例子

```csharp
string[] array = { "ipa.aot.na001", "ipa.aot.na002", "ipa.aot.na003" };
GameSambaSDK.SetIAPItems(array);
```



## 登录

### 登录游客账号

> #### API

```csharp
GameSambaSDK.LoginGuest();
```



### 登录Facebook账号

> #### API

```csharp
GameSambaSDK.LoginFacebook();
```



### 登录Google账号

> #### API

```csharp
GameSambaSDK.LoginGoogle();
```



### 登录GameSamba账号

> #### API

```csharp
GameSambaSDK.LoginGameSamba();
```



### 登录IOS游戏中心

> #### API

```csharp
GameSambaSDK.LoginGameCenter();
```

## 登录成功后设置

{% hint style="info" %}
登录帐号成功后，选择游戏服务器，选择游戏角色后，需要调用以下方法设置服务器和角色信息。
{% endhint %}

### 设置服务器信息

> #### API

```csharp
GameSambaSDK.SetServerInfo(string serverId, string serverName);
```

> #### 参数

| 参数 | 类型 | 必须 | 描述 |
| :--- | :--- | :--- | :--- |
| serverId | **string** | 是 | 服务器ID |
| serverName | **string** | 是 | 服务器名称 |

> #### 例子

```csharp
string serverId = "1"; //服务器ID
string serverName = "test"; //服务器名称
GameSambaSDK.SetServerInfo(serverId, serverName);
```



### 设置角色信息

> #### API

```csharp
GameSambaSDK.SetRoleInfo(string roleName);
```

> #### 参数

| 参数 | 类型 | 必须 | 描述 |
| :--- | :--- | :--- | :--- |
| roleName | **string** | 是 | 角色名称 |

> #### 例子

```csharp
string roleName = "user"; //角色名称
GameSambaSDK.SetRoleInfo(roleName);
```





## 悬浮框

{% hint style="info" %}
登录帐号成功后，再登录游戏角色，之后再去调用显示悬浮框。
{% endhint %}

### 显示悬浮气泡框

> #### API

```csharp
GameSambaSDK.ShowPop();
```



### 隐藏悬浮气泡框

> #### API

```csharp
GameSambaSDK.HidePop();
```



### 设置悬浮气泡框位置

> #### API

```csharp
GameSambaSDK.SetPopPosition(PopDirection direction, float yPercentage);
```

> #### 参数

| 参数 | 类型 | 必须 | 描述 |
| :--- | :--- | :--- | :--- |
| direction | **PopDirection** | 是 | 悬浮框方向（左边，右边） |
| yPercentage | **float** | 是 | Y轴位置，屏幕高度的百分比，上方为0，下方为1 |

> #### 例子

```csharp
 //设置悬浮框初始位置, iPhone注意避开刘海范围
 GameSambaSDK.SetPopPosition(PopDirection.Left, 0.3f); 
```



### 设置悬浮气泡框支持功能

> #### API

```csharp
GameSambaSDK.SetPopSupportFunction(bool isOpenShare, bool isOpenFeedback, bool isOpenDiscord);
```

> #### 参数

| 参数 | 类型 | 必须 | 描述 |
| :--- | :--- | :--- | :--- |
| isOpenShare | **bool** | 是 | 否显示分享功能 |
| isOpenFeedback | **bool** | 是 | 是否显示客服功能 |
| isOpenDiscord | **bool** | 是 | 是否显示Discord |

> #### 例子

```csharp
//设置悬浮功能开启
GameSambaSDK.SetPopSupportFunction(false, true, true); 
```



## 分享

### 分享链接到Facebook

> #### API

```csharp
GameSambaSDK.ShareFacebookLink(string shareLink, string quote);
```

> #### 参数

| 参数 | 类型 | 必须 | 描述 |
| :--- | :--- | :--- | :--- |
| shareLink | **string** | 是 | 分享链接 |
| quote | **string** | 是 | 引用文字 |

> #### 例子

```csharp
string shareLink = "http://tg.gamesamba.com";
string quote = "这是一条引文";
GameSambaSDK.ShareFacebookLink(shareLink, quote);
```



### 分享图片文件到Facebook

> #### API

```csharp
GameSambaSDK.ShareFacebookImage(string imagePath);
```

> #### 参数

| 参数 | 类型 | 必须 | 描述 |
| :--- | :--- | :--- | :--- |
| imagePath | **string** | 是 | 图片文件本地路径 |

> #### 例子

```csharp
String imagePath = "/storage/emulated/0/game321/image.png";
GameSambaSDK.ShareFacebookImage(imagePath);
```



## 内购

### 谷歌内购

> #### API

```csharp
GameSambaSDK.PurchaseGoogle(string itemId);
```

> #### 参数

| 参数 | 类型 | 必须 | 描述 |
| :--- | :--- | :--- | :--- |
| itemId | **string** | 是 | 商品ID |

> #### 例子

```csharp
string itemId = "ipa.tg.na002"; //商品ID
GameSambaSDK.PurchaseGoogle(itemId);
```



### 苹果内购

> #### API

```csharp
GameSambaSDK.PurchaseApple(string itemId);
```

> #### 参数

| 参数 | 类型 | 必须 | 描述 |
| :--- | :--- | :--- | :--- |
| itemId | **string** | 是 | 商品ID |

> #### 例子

```csharp
string itemId = "ipa.tg.na002"; //商品ID
GameSambaSDK.PurchaseApple(itemId);
```



### 第三方内购

> #### API

```csharp
GameSambaSDK.PurchaseThird(string itemId);
```

> #### 参数

| 参数 | 类型 | 必须 | 描述 |
| :--- | :--- | :--- | :--- |
| itemId | **string** | 是 | 商品ID |

> #### 例子

```csharp
string itemId = "ipa.tg.na002"; //商品ID
GameSambaSDK.PurchaseThird(itemId);
```



## 事件统计

### 设置客户用户ID

> #### 描述

可以帮助您交叉引用自己的独有 ID 以及 AppsFlyer 的独有 ID 和其他设备的 ID。该 ID 与回传 IP 一同出现在 AppsFlyer CSV 报告中，用于与您的内部 ID 交叉引用。

> #### API

```csharp
GameSambaSDK.SetUserId(string userId);
```

> #### 参数

| 参数 | 类型 | 必须 | 描述 |
| :--- | :--- | :--- | :--- |
| userId | **string** | 是 | 用户ID |

> #### 例子

```csharp
string userId = "123";
GameSambaSDK.SetUserId(userId);
```



### 记录统计事件

> #### API

```csharp
GameSambaSDK.RecordEvent(string eventName, IDictionary<string, string> parameters = null);
```

> #### 参数

| 参数 | 类型 | 必须 | 描述 |
| :--- | :--- | :--- | :--- |
| eventName | **string** | 是 | 事件名称，注意：应用内事件名称长度不得超过 45 个字符 |
| parameters | **Dictionary** | 否 | 记录内容（字典） |

> #### 例子

```csharp
string eventName = "Test";
Dictionary<string, string> evetParams = new Dictionary<string, string>();
evetParams.Add("id", "1");
evetParams.Add("level", "1");
GameSambaSDK.RecordEvent(eventName, evetParams);
```



### 追踪购买事件

> #### API

```csharp
GameSambaSDK.RecordPurchaseEvent(string itemId, string itemType, float revenue, string currencyCode);
```

> #### 参数

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x53C2;&#x6570;</th>
      <th style="text-align:left">&#x7C7B;&#x578B;</th>
      <th style="text-align:left">&#x5FC5;&#x987B;</th>
      <th style="text-align:left">&#x63CF;&#x8FF0;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">itemId</td>
      <td style="text-align:left"><b>string</b>
      </td>
      <td style="text-align:left">&#x662F;</td>
      <td style="text-align:left">&#x5546;&#x54C1;ID</td>
    </tr>
    <tr>
      <td style="text-align:left">itemType</td>
      <td style="text-align:left"><b>string</b>
      </td>
      <td style="text-align:left">&#x662F;</td>
      <td style="text-align:left">&#x5546;&#x54C1;&#x7C7B;&#x578B;</td>
    </tr>
    <tr>
      <td style="text-align:left">revenue</td>
      <td style="text-align:left"><b>float</b>
      </td>
      <td style="text-align:left">&#x662F;</td>
      <td style="text-align:left">&#x6536;&#x5165;</td>
    </tr>
    <tr>
      <td style="text-align:left">currencyCode</td>
      <td style="text-align:left"><b>string</b>
      </td>
      <td style="text-align:left">&#x662F;</td>
      <td style="text-align:left">
        <p>&#x8D27;&#x5E01;&#x5355;&#x4F4D;&#xFF08;ISO 4217 &#x4EE3;&#x7801;&#xFF09;</p>
        <p>&#x4F8B;&#x5982;&quot;USD&quot;,&quot;HKD&quot;,&quot;CNY&quot;,&quot;TWD&quot;&#x7B49;</p>
        <p>&#x53C2;&#x8003;&#xFF1A;https://www.xe.com/iso4217.php</p>
      </td>
    </tr>
  </tbody>
</table>> #### 例子

```csharp
string itemId = "good1"; //商品ID
string itemType = "good"; //商品类型
float revenue = 2.99f; //商品价格
string currencyCode = "USD"; //货币单位
GameSambaSDK.RecordPurchaseEvent(itemId, itemType, revenue, currencyCode);
```



### 记录GoogleAnalysis事件

> #### API

```csharp
GameSambaSDK.RecordGAEvent(string eventName, IDictionary<string, string> parameters = null);
```

> #### 参数

| 参数 | 类型 | 必须 | 描述 |
| :--- | :--- | :--- | :--- |
| eventName | **string** | 是 | 事件名称，注意：应用内事件名称长度不得超过 45 个字符 |
| parameters | **Dictionary** | 否 | 记录内容（字典） |

> #### 例子

```csharp
string eventName = "Test";
Dictionary<string, string> evetParams = new Dictionary<string, string>();
evetParams.Add("id", "1");
evetParams.Add("level", "1");
GameSambaSDK.RecordGAEvent(eventName, evetParams);
```




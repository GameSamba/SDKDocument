# Google 支付

## 初始化

> ####  API介绍

谷歌支付初始化

> #### API原型

```java
/**
 * 初始化谷歌内购实例
 * @param activity        当前Activity
 * @param publicKey       谷歌PublicKey
 * @param billingCallback 购买回调
 * @return
 */
public static GoogleBillingSupport newBillingInstance(Activity activity, String publicKey, BillingCallback billingCallback) 
```

> #### 示例

```text
private GoogleBillingSupport googleBillingSupport;
```

```java
googleBillingSupport = GoogleBillingSupport.newBillingInstance(MainActivity.this, getString(R.string.google_public_key), new BillingCallback() {
    @Override
    public void onPurchased(String productId, String orderId) {
        //购买成功
        logText.setText("orderId=" + orderId);
    }
    
    @Override
    public void onBillingInitialized() {
        //GooglePlay IAP服务初始化成功
    }
    
    @Override
    public void onError(int errorCode) {
        //购买失败
        logText.setText("errorCode=" + errorCode);
    }
});
```

## 商品购买

> ####  API介绍

调用谷歌内购

> #### API原型

```java
/**
 * 购买商品
 * @param itemId     商品ID
 * @param userId     用户ID
 * @param userName   用户角色名称
 * @param serverId   服务器ID
 * @param serverName 服务器名称
 */
public void purchase(String itemId, String userId, String userName, String serverId, String serverName) 
```

> #### 示例

```java
String itemId = "ipa.tg.na002";//商品ID
String userId = ngamesSdk.getCurrentUserId();//用户ID
String userName = "test";//用户名称
String serverId = "1";//服务器ID
String serverName = "test";//服务器名称
//购买商品
googleBillingSupport.purchase(itemId, userId, userName, serverId, serverName);
```



## 生命周期

### 1.onResume

#### 在主Activity\#onResume中 <a id="src-cnt-0-0"></a>

```java
...
@Override
protected void onResume() {
    super.onResume();
    ...
    if (googleBillingSupport != null) {
        googleBillingSupport.onResume();
    }
}
```

### 2.onDestroy

#### 在主Activity\#onDestroy中 <a id="src-cnt-0-0"></a>

```java
...
@Override
protected void onDestroy() {
    super.onDestroy();
    ...
    if (googleBillingSupport != null) {
        googleBillingSupport.onDestroy();
    }
}
```

### 3.onActivityResult

#### 在主Activity\#onActivityResult中 <a id="src-cnt-0-0"></a>

```java
...
@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    ...
    if (googleBillingSupport != null && googleBillingSupport.handleActivityResult(requestCode, resultCode, data)) {
        return;
    }
    ...
    super.onActivityResult(requestCode, resultCode, data);
}
```




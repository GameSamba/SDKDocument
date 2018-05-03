# 支付

## Google支付

> ####  API介绍

使用谷歌支付

> #### API原型

```java
/**
 * 初始化谷歌内购实例
 * @param activity 当前Activity
 * @param publicKey 谷歌PublicKey
 * @param orderDetail 订单信息
 * @param billingCallback 购买回调
 * @param isDebug 是否是Debug,Debug模式下会输出日志到SD卡中
 * @return
 */
public static GoogleBillingSupport newBillingInstance(Activity activity, String publicKey, OrderDetail orderDetail, BillingCallback billingCallback, boolean isDebug) 
```

```java
/**
 * 购买
 */
public void purchase() 
```

> #### 示例

```java
private GoogleBillingSupport googleBillingSupport;
```

```java
//实例化订单详情
OrderDetail orderDetail = new OrderDetail();
orderDetail.setGid(NgamesUtil.getAppId(MainActivity.this));//设置游戏ID
orderDetail.setItemid("ipa.tg.na002");//设置商品ID
orderDetail.setLang(Const.LANG_EN);//设置语言
orderDetail.setSid("1");//设置服务器ID
orderDetail.setSname("test");//设置服务器名称
orderDetail.setTime(String.valueOf(System.currentTimeMillis()));//设置当前时间
orderDetail.setType("123");//设置类型
orderDetail.setUid(ngamesSdk.getCurrentUserId());//设置当前用户ID
orderDetail.setUsername("test");//设置用户帐号

googleBillingSupport = GoogleBillingSupport.newBillingInstance(MainActivity.this, getString(R.string.base64EncodedPublicKey), orderDetail, new BillingCallback() {
    @Override
    public void onPurchased(String productId, String orderId) {
        //购买成功
        logText.setText("orderId=" + orderId);
    }
    
    @Override
    public void onBillingInitialized() {
    }
    
    @Override
    public void onError(int errorCode) {
        //购买失败
        logText.setText("errorCode=" + errorCode);
    }
}, false);
googleBillingSupport.purchase();
```

{% hint style="info" %}
 
{% endhint %}




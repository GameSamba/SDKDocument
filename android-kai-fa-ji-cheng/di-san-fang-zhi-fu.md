# 第三方 支付

**Note**: 第三方充值接口

## 购买商品 <a id="ji-lu-tong-ji-shi-jian"></a>

> #### API介绍 <a id="api-jie-shao"></a>

通过第三方购买商品

> #### API原型 <a id="api-yuan-xing-2"></a>

```java
/**
 * 打开第三方充值界面
 * @param activity 当前Activity
 * @param sid 区服ID
 * @param sname 区服名称
 * @param username 角色名称
 * @param itemid 商品ID
 * @param billingCallback 购买回调
 */
public void purchaseByThird(Activity activity, String sid, String sname, String username, String itemid, BillingCallback billingCallback)
```

> #### 示例 <a id="shi-li"></a>

```java
String userName = "test";//用户名称
String serverId = "1";//服务器ID
String serverName = "test";//服务器名称
String itemId = "na001";//商品ID
//购买商品
ngamesSdk.purchaseByThird(MainActivity.this, serverId, serverName, userName, itemId, new BillingCallback() {
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
```




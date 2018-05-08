# Samsung 支付

SDK中使用三星IAP 5.0版本

## 商品类型

1. 物品（可消耗，不可消耗）
2. 订购（无自动订购（NRS），自动订购）

## 接入要求

* IAP 5.0 支持Android API 14及以上版本，在更早版本上无法正常运行
* IAP 5.0 需要Galaxy Apps商店 4.2.13.xx 版本或以上

{% hint style="info" %}
请注意：下图中的弹窗出现时，说明该应用仍在测试模式下
{% endhint %}

 IAP支持封闭beta测试，用户可以从Galaxy Apps下载并购买商品。在BETA测试中，注册阶段的内容可 以被浏览，购买，消耗，真实交易付款或者测试交易。

 更多信息请参考三星开发者网站: \(http://developer.samsung.com/iap/how-to-start\).





需要添加权限，用来链接IAP

“com.samsung.android.iap.permission.BILLING” 





测试购买流程的步骤：

请按以下步骤测试此代码： 

1 在主页面上点击Purchase One Item .验证三星账号页面出现。

 2 输入三星账号密码并点击确认

 3 支付页面出现，可以选择支付方式

 4 点击选择需要的支付方式 

5 点击Buy 开始IAP支付流程



{% hint style="info" %}
 四个activities必须为透明背景，需设置 android:theme=”@style/Theme.Empty”. 否则会覆盖原本的 应用。
{% endhint %}


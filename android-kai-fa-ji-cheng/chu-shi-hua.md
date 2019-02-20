# 初始化

## 初始化

#### 在主Activity\#onCreate初始化 <a id="src-cnt-0-0"></a>

```java
private NgamesSdk ngamesSdk;
...
@Override
protected void onCreate(Bundle savedInstanceState) {
	super.onCreate(savedInstanceState);
	...
	// 初始化
	ngamesSdk = NgamesSdk.getInstance(this, this, Const.LANG_EN);
}
```

> ####  API原型

```java
public static NgamesSdk getInstance(Context context, Activity activity, String lang)
```

> ####  参数

* Context context ：上下文对象
* Activity activity ：当前Activity
* String lang ：SDK显示的语言

> ####  lang 参数说明

| 语言（lang） | 描述 |
| :--- | :--- |
| Const.LANG\_EN | 英文 |
| Const.LANG\_CN | 简体中文 |
| Const.LANG\_TW | 繁体中文 |
|  Const.LANG\_FR | 法文 |
|  Const.LANG\_TH | 泰文 |
|  Const.LANG\_KO | 韓文 |

{% hint style="info" %}
SDK使用前必须初始化
{% endhint %}

## 生命周期

### 1.onResume

#### 在主Activity\#onResume中 <a id="src-cnt-0-0"></a>

```java
...
@Override
protected void onResume() {
    super.onResume();
    ...
    if (ngamesSdk != null) {
        ngamesSdk.onResume();
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
    if (ngamesSdk != null) {
        ngamesSdk.onDestroy();
    }
}
```

### 3.onConfigurationChanged

#### 在主Activity\#onConfigurationChanged中 <a id="src-cnt-0-0"></a>

```java
...
@Override
public void onConfigurationChanged(Configuration newConfig) {
    super.onConfigurationChanged(newConfig);
    ...
    if (ngamesSdk != null) {
        ngamesSdk.onConfigurationChanged();
    }
}
```

### 4.onActivityResult

#### 在主Activity\#onActivityResult中 <a id="src-cnt-0-0"></a>

```java
...
@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    ...
    if (ngamesSdk != null && ngamesSdk.handleActivityResult(requestCode, resultCode, data)) {
        return;
    }
    if (requestCode == Const.THIRD_LOGIN_REQUEST_CODE) {
            switch (resultCode) {
                case Const.INTENT_RESULT_OK:
                    AccountResult loginUser = (AccountResult) data.getSerializableExtra(Const.LOGIN_USER);
                    //获取登录的用户信息
                    break;
                case Const.INTENT_RESULT_CANCELED:
                    //登录取消
                    break;
                case Const.INTENT_RESULT_ERROR:
                    //登录失败
                    break;
            }
            return;
        }
    ...
    super.onActivityResult(requestCode, resultCode, data);
}
```

## 设置调试模式 <a id="ji-lu-tong-ji-shi-jian"></a>

> #### API介绍 <a id="api-jie-shao"></a>

设置SDK调试模式

> #### API原型 <a id="api-yuan-xing-2"></a>

```java
/**
 * 设置调试模式
 * @param isDebug
 */
public void setDebug(boolean isDebug)
```

> #### 示例 <a id="shi-li"></a>

```java
ngamesSdk.setDebug(true);//设置Debug模式
```

{% hint style="info" %}
调试模式下，Android日志会打印出来。
{% endhint %}

{% hint style="danger" %}
打包发布前，测试完成，务必将调试模式设置为false 
{% endhint %}

![](blob:https://gamesamba.gitbook.io/226c1cbe-210e-4592-9856-e5ba1c9aa02a)![](blob:https://gamesamba.gitbook.io/953fad3c-8583-45f9-bb59-9925cb7b1891)


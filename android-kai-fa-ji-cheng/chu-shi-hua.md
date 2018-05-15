# 初始化

## 初始化

#### 在主Activity\#onCreate初始化 {#src-cnt-0-0}

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
| --- | --- | --- | --- | --- | --- | --- |
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

#### 在主Activity\#onResume中 {#src-cnt-0-0}

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

#### 在主Activity\#onDestroy中 {#src-cnt-0-0}

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

#### 在主Activity\#onConfigurationChanged中 {#src-cnt-0-0}

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

#### 在主Activity\#onActivityResult中 {#src-cnt-0-0}

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


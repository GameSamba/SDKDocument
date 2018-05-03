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




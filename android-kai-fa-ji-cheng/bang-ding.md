# 绑定

## 绑定Facebook账号

> ####  API介绍

帐号绑定Facebook帐号

> #### API原型

```java
/**
 * 绑定Facebook帐号
 * @param bindCallback 绑定回调
 */
public void bindFacebook(BindCallback bindCallback)
```

> #### 示例

```java
ngamesSdk.bindFacebook(new NgamesSdk.BindCallback() {
    @Override
    public void onSuccess(AccountResult bindAccountResult) {
        //绑定成功
        String msg = bindAccountResult.getMsg();
        logText.setText("bind facebook:" + msg);
    }
});
```

## 绑定Google账号

> ####  API介绍

帐号绑定Google帐号

> #### API原型

```java
/**
 * 绑定Google帐号
 * @param bindCallback 绑定回调
 */
public void bindGoogle(BindCallback bindCallback)
```

> #### 示例

```java
ngamesSdk.bindGoogle(new NgamesSdk.BindCallback() {
    @Override
    public void onSuccess(AccountResult bindAccountResult) {
        //绑定成功
        String msg = bindAccountResult.getMsg();
        logText.setText("bind google:" + msg);
    }
});
```

##  查看绑定状态

> #### API介绍

查看游戏帐号绑定状态

> #### API原型

```java
/**
 * 检测帐号绑定状态
 * @param checkBindCallback 绑定回调
 */
public void checkGuestBind(CheckBindCallback checkBindCallback)
```

> #### 示例

```java
ngamesSdk.checkGuestBind(new NgamesSdk.CheckBindCallback() {
    @Override
    public void onSuccess(boolean isFacebookBind, boolean isGoogleBind) {
        //绑定状态查看回调
        logText.setText("facebook bind status: " + isFacebookBind + " ,google bind status: " + isGoogleBind);
    }
});
```



## 




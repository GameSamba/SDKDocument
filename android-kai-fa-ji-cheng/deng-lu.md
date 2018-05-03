# 登录

SDK登录分为游客登录，GameSamba帐号登录，Facebook帐号登录和Google帐号登录 4种模式。

## 游客登录

> #### API介绍

SDK会根据设备ID生成游客帐号，玩家使用游客帐号登录。

> #### API原型

```java
/**
 * 游客登录
 * @param tokenLoginCallback 登录结果回调
 */
public void guestLogin(TokenLoginCallback tokenLoginCallback)
```

> #### 示例

```java
ngamesSdk.guestLogin(new NgamesSdk.TokenLoginCallback() {
    @Override
    public void onSuccess(TokenLoginResult.Data data) {
        //登录成功
    }

    @Override
    public void onError(BaseResult error) {
        //登录失败
    }
});
```

## GameSamba 账号登录

> #### API介绍

 SDK会根据设备ID生成游客帐号，玩家使用游客帐号登录。

> ####  API原型

```java
/**
 * 登录GameSamba账号
 * @param registerCallback 
 */
public void loginGameSamba(final RegisterCallback registerCallback)
```

> ####  示例

```java
ngamesSdk.loginGameSamba(new NgamesSdk.RegisterCallback() {
    @Override
    public void onSuccess(AccountResult bindAccountResult) {
        //登录成功
    }

    @Override
    public void onError(BaseResult error) {
        //登录失败
    }
});
```

## Facebook 账号登录

> ####  API介绍

使用Facebook帐号登录，登录结果会通当前Activity中的 `onActivityResult` 中返回

> ####  API原型

```java
/**
 * Facebook登录
 * @param activity 当前Activity
 */
public static void facebookLogin(Activity activity)
```

> ####  示例

```java
FacebookSocialHelper.facebookLogin(MainActivity.this);
```

#### 添加登录回调：

 [Facebook和Google登录结果回调](deng-lu.md#facebook-he-google-deng-lu-jie-guo-hui-tiao)

## Google 帐号登录

> ####  API介绍

使用 Google帐号登录

> ####  API原型

```java
/**
 * Google帐号登录
 * @param activity 当前Activity
 */
public static void googleLogin(Activity activity) 
```

> ####  示例

```java
GoogleSocialHelper.googleLogin(MainActivity.this);
```

####  添加登录回调：

 [Facebook和Google登录结果回调](deng-lu.md#facebook-he-google-deng-lu-jie-guo-hui-tiao)

## Facebook和Google登录结果回调

如果使用了Facebook或者Google登录，必须实现 `onActivityResult` 中的回调方法进行结果回调。

####  添加登录回调：

```java
@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    ...
    if (ngamesSdk != null && ngamesSdk.handleActivityResult(requestCode, resultCode, data)) {
        return;
    }
    if (requestCode == Const.THIRD_LOGIN_REQUEST_CODE) {
        switch (resultCode) {
            case Const.INTENT_RESULT_OK:
                //登录成功
                AccountResult loginUser = (AccountResult) data.getSerializableExtra(Const.LOGIN_USER);
                logText.setText("user type:" + loginUser.getAccountType() + " ,user id=" + loginUser.getData().getId());
                break;
            case Const.INTENT_RESULT_CANCELED:
                //取消登录
                Toast.makeText(MainActivity.this, "canceled", Toast.LENGTH_SHORT).show();
                break;
            case Const.INTENT_RESULT_ERROR:
                //登录失败
                Toast.makeText(MainActivity.this, "error", Toast.LENGTH_SHORT).show();
                break;
            default:
                logText.setText("resultCode=" + resultCode);
                break;
        }
        return;
    }
    ...
    super.onActivityResult(requestCode, resultCode, data);
}
```

## 登录成功

登录成功后，**游戏研发**需要在登录成功回调中实现：

```java
//设置服务器ID
ngamesSdk.setSid(mServerId);
//设置角色名称
ngamesSdk.setRoleName(mRoleName);
//显示悬浮框（自己决定是否显示）
ngamesSdk.showPop();
```






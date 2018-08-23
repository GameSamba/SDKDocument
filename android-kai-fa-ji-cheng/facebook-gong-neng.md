# Facebook 功能

## 分享链接

> ####  API介绍

Facebook分享链接功能

> #### API原型

```java
/**
 * Facebook分享
 * @param link 分享链接
 * @param quote 引用
 * @param shareCallback 分享回调
 */
public void share(String link, String quote, FacebookCallback<Sharer.Result> shareCallback)
```

> #### 示例

```java
ngamesSdk.getFacebookSocialHelper().share("http://tg.gamesamba.com/default/share", "", new FacebookCallback<Sharer.Result>() {
    @Override
    public void onSuccess(Sharer.Result result) {
        //分享成功
        Toast.makeText(MainActivity.this, "succeed", Toast.LENGTH_SHORT).show();
    }
    
    @Override
    public void onCancel() {
        //分享取消
        Toast.makeText(MainActivity.this, "canceled！", Toast.LENGTH_SHORT).show();
    }
    
    @Override
    public void onError(FacebookException error) {
        //分享失败
        Toast.makeText(MainActivity.this, "error！", Toast.LENGTH_SHORT).show();
    }
});
```

## 分享图片

> ####  API介绍

Facebook分享图片功能

> #### API原型

```java
/**
 * 分享图片
 * @param imagePath 本地图片地址
 * @param shareCallback 分享回调
 */
public void shareImage(String imagePath, FacebookCallback<Sharer.Result> shareCallback)
```

> #### 示例

```java
String imagePath = "/storage/emulated/0/game321/image.png";
ngamesSdk.getFacebookSocialHelper().shareImage(imagePath, new FacebookCallback<Sharer.Result>() {
    @Override
    public void onSuccess(Sharer.Result result) {
        Toast.makeText(MainActivity.this, "succeed", Toast.LENGTH_SHORT).show();
    }

    @Override
    public void onCancel() {
        Toast.makeText(MainActivity.this, "canceled！", Toast.LENGTH_SHORT).show();
    }

    @Override
    public void onError(FacebookException e) {
        Toast.makeText(MainActivity.this, "error！", Toast.LENGTH_SHORT).show();
    }
});
```

## 邀请

> #### API介绍

 Facebook邀请功能

> #### API原型

```java
/**
 * Facebook邀请
 * @param gameRequestCallback 回调
 * @param title 标题
 * @param message 内容
 */
public void invite(FacebookCallback<GameRequestDialog.Result> gameRequestCallback, String title, String message) 
```

> #### 示例

```java
ngamesSdk.getFacebookSocialHelper().invite(new FacebookCallback<GameRequestDialog.Result>() {
    @Override
    public void onSuccess(GameRequestDialog.Result result) {
        //邀请成功
        Toast.makeText(MainActivity.this, "succeed", Toast.LENGTH_SHORT).show();
        //ngamesSdk.putInvitationsNumber(eventId, result);
    }
    
    @Override
    public void onCancel() {
        //取消邀请
        Toast.makeText(MainActivity.this, "canceled！", Toast.LENGTH_SHORT).show();
    }

    @Override
    public void onError(FacebookException error) {
        //邀请失败
        Toast.makeText(MainActivity.this, "error！", Toast.LENGTH_SHORT).show();
    }
}, "游戏邀请", "和我一起玩吧！");
```

## 获取用户照片

> ####  API介绍

Facebook获取用户照片URL

> #### API原型

```java
/**
 * 获取Facebook用户图片URL
 * @param width 图片宽度
 * @param height 图片高度
 * @return
 */
public String getFacebookUserPictureUri(int width, int height)
```

> #### 示例

```java
String url = ngamesSdk.getFacebookSocialHelper().getFacebookUserPictureUri(width, height);
if (url != null) {
    //获取用户图片
}
```

## 邀请数量

####  API介绍

获取用户邀请数量

> #### API原型

```java
/**
 * 获取Facebook邀请数量
 * @param eventId
 * @param fbInvitationsNumberCallback
 */
public void getFbInviteNums(String eventId, FbInvitationsNumberCallback fbInvitationsNumberCallback)
```

> #### 示例

```java
ngamesSdk.getFbInviteNums(eventId, new NgamesSdk.FbInvitationsNumberCallback() {
    @Override
    public void onSuccess(List<String> fbIds) {
        //获取成功
        if (fbIds != null && fbIds.size() > 0) {
            Toast.makeText(MainActivity.this, "FB邀请人数为：" + fbIds.size(), Toast.LENGTH_SHORT).show();
        } else {
            Toast.makeText(MainActivity.this, "FB邀请人数为：0", Toast.LENGTH_SHORT).show();
        }
    }
    
    @Override
    public void onError(BaseResult error) {
        //获取失败
    }
});
```

{% hint style="info" %}
 Super-powers are granted randomly so please submit an issue if you're not happy with yours.
{% endhint %}




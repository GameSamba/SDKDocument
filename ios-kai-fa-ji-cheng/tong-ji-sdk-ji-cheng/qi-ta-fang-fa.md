# 其他方法

`currencyCode` 用来设置货币单位, 默认值为`@"USD"` , 设置值可参考 [http://www.xe.com/iso4217.php](http://www.xe.com/iso4217.php)

`customerUserID` 用来在发送事件时附带上相关的用户ID, 所以需要尽快配置

> AF要求customUserID 应在 trackAppLaunch 之前设置, 但是这种情况下用户往往还没有登录,所以可以考虑使用如下:
>
> 登录SDK中有如下方法:
>
> ```objectivec
> //获取上一次成功登录的用户ID
> if([NGAGameLoginKit shareInstance].lastUser.userId) {
>   //TODO 设置customerUserID
> }
> ```
>
> 所以可以在用户未登录之前通过lastUser设置customerUserID, 在用户登录之后再设置一遍登录用户的UserID, 这样的话就比较准确了


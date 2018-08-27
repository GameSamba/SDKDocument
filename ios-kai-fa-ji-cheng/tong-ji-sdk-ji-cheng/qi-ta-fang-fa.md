# 其他说明

参考`NGAAppEvents.h`文件中

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
> 所以可以在用户**未登录**之前通过lastUser设置customerUserID, 在用户**登录之后**再通过登录用户的UserID设置一下customUserID, 这样就比较准确了



---

##### 购买事件方法会要求传递货币单位

`NGAConfig.h`头文件中, 属性`currencyCode`可以设置全局货币单位

如果设置了`currencyCode`的值,并且在购买事件方法中货币参数填写为`nil`, 那么函数内部会自动获取全局货币单位.
# 悬浮窗

### 悬浮窗的构建

```objectivec
	//请通过测方法完成悬浮窗的初始化    
	//传递CGPointZero参数则显示在默认左下角位置, 也可以传入其他位置参数, 但是要注意避开iPhone的刘海区域
    NGADragBallView *dragBallView = [NGADragBallView dragBallViewWithPosition:CGPointZero];

    //设置悬浮窗中分享按钮的功能
    dragBallView.openShare = YES;   //开启分享功能
    [dragBallView setupShareAction:@selector(share) onTarget:self];

    /*
    - (void)share{
      //分享代码, 具体实现参考Demo代码并结合分享方式
    }
    */

    //开启客服功能并设置玩家姓名参数便于提交相关表单信息
    dragBallView.openForum = YES;   //开启Support功能
    [dragBallView setRoleName:@"Someone"];  //Support需传入角色名
```



### 悬浮窗的显示与关闭

*建议在完成用户的登入后再显示悬浮窗*

悬浮窗的显示与关闭可以通过基本的视图管理来完成
例如: 

```objectivec
//显示
[AppRootViewController.view addSubView:dragBallView];

//关闭
[dragBallView removeFromSuperview];
```



也可以通过NGADragBallView的内部方法完成
例如: 

```objectivec
//显示
[dragBallView showPopView];

//关闭
[dragBallView closePopView];
```



### 悬浮窗中账号切换功能实现

实现文档 [登录](deng-lu.md)中 1. 代理方法`gameLoginKit: didUserChanged:`



### 悬浮窗按钮文字的自定义更改

NGALoginSDKStrings.bundle中存放着界面UI及部分提示用语的本地化.

悬浮窗按钮用到的按钮本地化语言包括如下, 可以根据需要进行相应的调整

```
"B_Bind" = "帳戶";  		//对应账号按钮
"B_Facebook" = "分享";	//对应分享按钮
"B_Support" = "客服";		//对应客服支援按钮
```


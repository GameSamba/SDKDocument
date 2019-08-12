# 悬浮窗

```objectivec
    //构建悬浮窗,传递CGPointZero参数则显示在默认左下角位置, 也可以穿入其他位置参数, 但是要注意避开iPhone的刘海区域
    NGADragBallView *drag = [NGADragBallView dragBallViewWithPosition:CGPointZero];
    [self.view addSubview:drag];

    //设置悬浮窗中分享按钮的功能
    drag.openShare = YES;   //开启分享功能
    [drag setupShareAction:@selector(share) onTarget:self];
/*
- (void)share{
	//...
}
*/
    //开启客服功能并设置玩家姓名参数便于提交相关表单信息
    drag.openForum = YES;   //开启Support功能
    [drag setRoleName:@"Someone"];  //Support需传入角色名
```


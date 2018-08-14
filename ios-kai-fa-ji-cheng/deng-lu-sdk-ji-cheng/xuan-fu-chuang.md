# 悬浮窗

```objective-c
    //获取悬浮窗控件并添加到视图中
    NGAGameDragBallView *dragballView=[[NGAGameDragBallView alloc] initWithFrame:CGRectMake(0, 250, 0, 0)];
    [self.view addSubview:dragballView];

    //通过此方法设置App的rootViewController, 便于展示UI
    [dragballView setupShowManageAccountViewFromViewController:nil];

    //设置悬浮窗中分享按钮的功能
    dragballView.isOpenShare = YES;
    [dragballView setupShareAction:@selector(share:) onTarget:self];

    //开启客服功能并设置玩家姓名参数便于提交相关表单信息
    dragballView.isOpenforum = YES;
    [dragballView setupRoleNameForSupport:@"角色 名"];
```


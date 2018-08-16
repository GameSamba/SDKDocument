# Facebook相关功能

## 1. Facebook分享

```objectivec
    //showFromViewController参数应该填写的是当前app的rootViewController
    [[NGAFacebookHelper shareInstance] fbShareParam:@"desc" contentURL:@"https://www.facebook.com/SuperheroBrawl" 
     showFromViewController:self Complate:^(BOOL isShareSuccess) {
        if (isShareSuccess) {
            NSLog(@"分享链接成功");
        }else{
            NSLog(@"分享链接失败");
        }
    }];
```

## 2. Facebook游戏邀请

```objectivec
    //eventID:活动的事件ID, 回调返回的是被邀请的fb的userid数组
    [[NGAFacebookHelper shareInstance] GameFBInviteMessage:@"一起来玩呀" Title:@"邀请测试" 
        eventID:@"1001" Complate:^(InviteResultType type, NSArray *ids) {
        if (type == InviteSuccessed){
            NSLog(@"分享成功, 已邀请用户:%@", ids);
        }
    }];
```

## 2.1. Facebook邀请计数

```objectivec
    [[NGAFacebookHelper shareInstance] getFBInvitedUsersWithEventID:@"1001" 
        handler:^(NSArray *inviteUserFBIDs) {
        //回调返回被邀请的fb的userid数组

    }];
```


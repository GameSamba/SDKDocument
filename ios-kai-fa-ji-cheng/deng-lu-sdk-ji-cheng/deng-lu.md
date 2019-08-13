# 登录

## 1. 设置代理方法及相关的参数

```objectivec
//设置服务器ID, 必要, 和购买物品时传入的sid需一致
[NGAGameLoginKit shareInstance].sid = @"1"; 

//设置遵循NGAGameLoginKitDelegate协议并实现代理对象方法获取通过UI登陆以及用户切换返回的User, 比如GameSamba, 账号切换登录等情况
[NGAGameLoginKit shareInstance].delegate = self;

//代理方法 (主要是通过悬浮窗界面进行用户切换时, 需要进行User变更后的用户处理)
- (void)gameLoginKit:(NGAGameLoginKit *)gameLoginKit didUserChanged:(UserModel *)user{
    //TODO: 此处返回通过界面UI登陆以及切换用户后获得的user
}

//具体可查看Demo示例代码
```

## 2.  游客登录

```objectivec
    [[NGAGameLoginKit shareInstance] guestUserLoginSuccess:^(UserModel *user) {
        //TODO: 此处返回Guest User

    } error:^(NSError *errorinfo) {

    }];
```

## 3. Facebook 登录

```objectivec
    [[NGAGameLoginKit shareInstance] fbLoginSuccess:^(UserModel *user) {
        NSLog(@"facebook 用户ID:%@", [FBSDKAccessToken currentAccessToken].userID);
        //TODO: 此处返回绑定fb的 User

    } error:^(NSError *errorinfo) {

    }];
```

## 4. GameCenter登录

```objectivec
    [[NGAGameLoginKit shareInstance] gameCenterLoginSuccess:^(UserModel *user) {
        //TODO: 此处返回绑定GameCenter的User

    } error:^(NSError *errorinfo) {

    }];
```


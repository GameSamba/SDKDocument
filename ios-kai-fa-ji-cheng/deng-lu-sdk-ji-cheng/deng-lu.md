# 登录

## 1. 设置代理方法及相关的参数

```text
//设置服务器ID, 必要
[NGAGameLoginKit shareInstance].sid = @"1"; 

//设置代理对象并实现代理方法获取通过UI登陆以及用户切换返回的User, 比如GameSamba登录等情况
[NGAGameLoginKit shareInstance].delegate = self;

//代理方法
- (void)gameLoginKit:(NGAGameLoginKit *)gameLoginKit didUserChanged:(UserModel *)user{
    //TODO: 此处返回通过界面UI登陆以及切换用户后获得的user
}
```

## 2.  游客登录

```text
    [[NGAGameLoginKit shareInstance] guestUserLoginSuccess:^(UserModel *user) {
        //TODO: 此处返回Guest User

    } error:^(NSError *errorinfo) {

    }];
```

## 3. Facebook 登录

```text
    [[NGAGameLoginKit shareInstance] fbLoginSuccess:^(UserModel *user) {
        NSLog(@"facebook 用户ID:%@", [FBSDKAccessToken currentAccessToken].userID);
        //TODO: 此处返回绑定fb的 User

    } error:^(NSError *errorinfo) {

    }];
```

## 4. GameCenter登录

```text
    [[NGAGameLoginKit shareInstance] gameCenterLoginSuccess:^(UserModel *user) {
        //TODO: 此处返回绑定GameCenter的User

    } error:^(NSError *errorinfo) {

    }];
```


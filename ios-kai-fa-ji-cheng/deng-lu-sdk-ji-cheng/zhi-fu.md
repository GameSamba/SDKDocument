# 支付

## 1. 初始化商品集合并设置代理方法

```text
- (void)shopsInit{
    //初始化iap对象
    if(![IAPShare sharedHelper].iap) {
        //TODO: 请配置相应的物品列表ID集合
        NSSet *goods = [NSSet setWithObjects:
                        @"com.ngames.mobile.ngamesloginapp.shop1",
                        @"com.ngames.mobile.ngamesloginapp.shop2",
                        @"com.ngames.mobile.ngamesloginapp.shop3",
                        @"com.ngames.mobile.ngamesloginapp.shop4",
                        @"com.ngames.mobile.ngamesloginapp.shop5",
                        nil];
        [IAPShare sharedHelper].iap = [[IAPHelper alloc] initWithProductIdentifiers:goods];
        //设置接收苹果支付回调的代理对象
        [IAPShare sharedHelper].iap.delegate = self;
    }

    //向AppStore请求以获取商品列表
    [[IAPShare sharedHelper].iap requestProductsWithCompletion:^(SKProductsRequest* request,SKProductsResponse* response){
        NSLog(@"商品初始化完成, 数量:%lu",(unsigned long)response.products.count]);
     }];
}


//支付回调:当Apple通知SDK购买完成时, SDK会把完成的交易通过代理方法返回给代理对象, 代理对象需要去获取服务器验证
-(void)recordTransaction:(SKPaymentTransaction *)transaction{
    //获取到商品并且购买后, 如果返回的状态是已购买, 需要进行服务器校验
    if(transaction.transactionState == SKPaymentTransactionStatePurchased) {   
        NSData *receiptData = [NSData dataWithContentsOfURL:[[NSBundle mainBundle] appStoreReceiptURL]];
        //验证方法
        [[IAPShare sharedHelper].iap checkOrderByOrderId:transaction.payment.applicationUsername receiptData:receiptData  success:^(NSString *orderid, NSError *error) {
            if (error) {
                NSLog(@"支付成功,校验订单号:%@失败!!!, %@", transaction.payment.applicationUsername, error);
            }else{
                NSLog(@"交易完成");
            }
        }];
    }
}
```

## 2. 发起购买物品的请求

```text
- (void)shopBtnClicked{
    //获取商品对象
    SKProduct* product =[[IAPShare sharedHelper].iap.products objectAtIndex:1];
    //发起购买请求
    [[IAPShare sharedHelper].iap buyProduct:product username:userName sname:serverName sid:serverId uid:[NGAGameLoginKit shareInstance].lastUser.userId itemid:itemid
     onCompletion:^(SKPaymentTransaction *trans, NSString *orderid) {
        if(trans.error || trans.transactionState == SKPaymentTransactionStateFailed){
            NSLog(@"错误: %@",[trans.error localizedDescription]);
        }
    }];
}
```

## 3. 验证

验证内购请参考`1`中 的支付回调部分


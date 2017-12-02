# 目录

- [自定义方法模块](#自定义方法模块)


## 自定义方法模块

 ```
   aa.h  //头文件
   #import <aaaa.h>   //sdk
   #import "RCTBridgeModule.h" //自定义？

   @interface Name : UIViewController<RCTBridgeModule(类)...>
   +(void) handleCallback:(NSURL *)url;

   @end
  ```

  ```
     aa.mm  //实体文件

     #import "aa.h"  //引入头文件
     #import <AlipaySDK/AlipaySDK.h>

     static RCTPromiseResolveBlock _resolve;  
     static RCTPromiseRejectBlock  _reject;

     @implementation Name  //定义模块名

     RCT_EXPORT_MODULE();  //抛出模块

     // 定义name 方法
     RCT_REMAP_METHOD(name,infoStr:(NSString *)infoStr resolver:(RCTPromiseResolveBlock) resolve rejecter:
          (RCTPromiseRejectBlock)reject)
    {
      _resolve = resolve;
      _reject = reject;
      [[AlipaySDK defaultService] auth_V2WithInfo:infoStr fromScheme:@"aaa" callback:^(NSDictionary *resultDic){
        NSlog(@"-->>authCallback");
        }];
    }
    @end
  ```





---
layout: post

title:  iOS Touch ID使用

categories: Swift

description: 

keywords: Touch ID,Swift,iOS

topmost: true
---

* Swift:

```swift
import LocalAuthentication
```



```swift
var context = LAContext()
    
    @IBAction func loginBtnClick(_ sender: Any) {
        context = LAContext()
        context.localizedCancelTitle = "Cancel";
        //        context.localizedFallbackTitle = "";
        var error:NSError?
        if context.canEvaluatePolicy(.deviceOwnerAuthentication, error: &error){
            let reason = "Run App"      
            context.evaluatePolicy(.deviceOwnerAuthentication, localizedReason: reason) { (success, error) in
                if success{
                    DispatchQueue.main.async {
                        /// do Something
                    }
                }else{
                    print(error?.localizedDescription ?? "Failed to authenticate")
                }
            }
            
        }else{
            print(error?.localizedDescription ?? "Can't evaluate policy")
        }
        
    }

```



* OC

  ```swift
  #import <LocalAuthentication/LocalAuthentication.h>
  
  @property(nonatomic,strong) LAContext *context;
  
  - (IBAction)buttonClick:(id)sender {
      NSError *error;
      if ([self.context canEvaluatePolicy:LAPolicyDeviceOwnerAuthentication error:&error]) {
          [self.context evaluatePolicy:LAPolicyDeviceOwnerAuthentication localizedReason:@"Cancel" reply:^(BOOL success, NSError * _Nullable error) {
              if (success) {
                  dispatch_sync(dispatch_get_main_queue(), ^{
                     /// do Something
                  });
              }else{
                   NSLog(@"%@", error.localizedDescription);
              }
          }];
      }else{
          NSLog(@"%@", error.localizedDescription);
      }
  }
  
  ```

  


PureCamera
=
 

[![CI Status](http://img.shields.io/travis/wubianxiaoxian/PureCamera.svg?style=flat)](https://travis-ci.org/wubianxiaoxian/PureCamera)
[![Version](https://img.shields.io/cocoapods/v/PureCamera.svg?style=flat)](http://cocoapods.org/pods/PureCamera)
[![License](https://img.shields.io/cocoapods/l/PureCamera.svg?style=flat)](http://cocoapods.org/pods/PureCamera)
[![Platform](https://img.shields.io/cocoapods/p/PureCamera.svg?style=flat)](http://cocoapods.org/pods/PureCamera)



一个自定义相机，拍照完成可自由裁剪
----

Requirements
----

* Xcode 6 or higher
* iOS 7.0 or higher
* ARC

Version
----

* 1.0




使用方法
----

*  Installation with CocoaPods：pod 'PureCamera'，引入        
     
        #import <PureCamera.h>  
* 或者下载demo到本地将PureCamera添加到工程，引入 
     
        #import "PureCamera.h"
*  在info.plist 里面添加
         Privacy - Microphone Usage Description  使用麦克风
         Privacy - Camera Usage Description      使用相机


* 按照下面的方法引用相机

      
        PureCamera *homec=[[PureCamera alloc]init];
        __weak typeof(self)myself=self;
        homec.fininshcapture=^(UIImage *ss){
        if (ss) {
            NSLog(@"照片存在");
          //在这里获取裁剪后的照片
            myself.ViewImageview.image=ss;
        }
        } ;
        [self presentViewController:homec animated:NO completion:^{}];}

* 按照下面的方法引用图片裁剪页
   
        首先引入 #import "TOCropViewController.h"
        遵守@interface ViewController ()<TOCropViewControllerDelegate>
        传入一张图片，就可以present图片裁剪页了
        TOCropViewController *cropController = [[TOCropViewController alloc] initWithImage:self.cropImageview.image];
        cropController.delegate = self;
        [self presentViewController:cropController animated:YES completion:nil];
        - (void)cropViewController:(TOCropViewController *)cropViewController didCropToImage:(UIImage *)image withRect:(CGRect)cropRect angle:(NSInteger)angle
        {
        self.cropImageview.image=image;
        self.navigationItem.rightBarButtonItem.enabled = YES;
        //下面定义了一个动画的效果，就是图片裁剪页消失的时候，会以下面你定义的view的frame为消失后的边界。
        CGRect viewFrame = [self.view convertRect:self.cropImageview.frame toView:self.navigationController.view];
        [cropViewController dismissAnimatedFromParentViewController:self withCroppedImage:image toFrame:viewFrame completion:^{
        }];
         }

        
![](http://i1.piimg.com/4851/0071da17a0c177d6.gif)

使用过程中，有任何问题，欢迎大家题issues


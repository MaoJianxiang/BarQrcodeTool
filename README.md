# BarQrcodeTool

[![CI Status](http://img.shields.io/travis/Mao Jianxiang/BarQrcodeTool.svg?style=flat)](https://travis-ci.org/Mao Jianxiang/BarQrcodeTool)
[![Version](https://img.shields.io/cocoapods/v/BarQrcodeTool.svg?style=flat)](http://cocoapods.org/pods/BarQrcodeTool)
[![License](https://img.shields.io/cocoapods/l/BarQrcodeTool.svg?style=flat)](http://cocoapods.org/pods/BarQrcodeTool)
[![Platform](https://img.shields.io/cocoapods/p/BarQrcodeTool.svg?style=flat)](http://cocoapods.org/pods/BarQrcodeTool)

## 0.0.1 特性

BarQrcodeTool有两个类: 

1. BarcodeGenerator 处理生成条形码和生成二维码的类方法。
2. ScanBarcodeView 处理扫描条码的方法。

### 注意，在使用扫描时需要用到相册，所以需要在工程的info.plist中添加 NSCameraUsageDescription key 即Privacy - Camera Usage Description设置String值。

不然会出现崩溃报错：
contain an NSCameraUsageDescription key with a string value explaining to the user how the app uses this data.

## 原理

生成二维码主要是靠<CoreImage/CoreImage.h>中的滤镜CIFilter类分别设置它的name类型为CICode128BarcodeGenerator和CIQRCodeGenerator，就可以生成对应的条形码和二维码。

### 扫描条码：

1. 输入源（配置摄像头）
2. 会话将摄像头采集到的条码转换成字符串数据
3. 输入数据
4. 预览图层显示扫描场景

最后我是通过代理的方式将结果返回。

## 使用

### 生成条形码

* barcodeString:传入数据

```
//size: 生成一维码的图片大小
+ (UIImage *)createBarcodeImageString:(NSString *)barcodeString imagSize:(CGSize)size;

```

### 生成二维码

1. QRString:传入数据
2. with:生成二维码的图片大小
3. image:想要二维码中间有个logo,就可以传过来，否则可以传nil

```
+ (UIImage *)createQRImageString:(NSString *)QRString imageWidth:(CGFloat)width logo:(UIImage *)image;
```

### 扫描条码


1. 生成扫描视图ScanBarcodeView
2. 设置代理,通过代理把扫描的结果返回
3. 设置标题，可以让扫描页有个人的页面标题 （默认标题 "二维码/条码"）
4. 显示手电筒，可以实际扫描时打开手电筒功能（默认不显示）

```
//MARK:-- 设置标题
- (void)setTitle:(NSString *)title;

//MARK:-- 初始化view
- (instancetype)initWithScanBarcodeView;


//MARK:-- ScanBarcodeViewDelegate,扫描结果返回 result
- (void)didFinishResultForScanBarcodeView:(ScanBarcodeView *)view value:(NSString *)result;

```

## Author

毛建祥, 邮箱: 15208105440@163.com

## License

BarQrcodeTool is available under the MIT license. See the LICENSE file for more info.

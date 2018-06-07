# TXBoardView白板SDK使用手册

## 1. TXBoardView简介

`TXBoardView.framework`是一个实现了基本白板功能的UIView扩展组件，提供了包括画笔、橡皮擦、背景图、标准图形、移动涂鸦和多白板实例等功能。
除了以上的本地白板功能之外，白板SDK还提供了网络多终端互通的扩展能力。

## 2. 集成
将TXBoardView.framework直接拖到项目目录下，添加以下依赖库：

|需添加的系统库|
|---|
|libc++.tbd|
|libstdc++.6.0.9.tbd|
|libz.tbd|

## 3. 白板使用方法

### 3.1 创建一块白板

`TXBoardView`的创建方法普通的UIView一致，创建实例后需要添加到一个UIView中。
为了正常使用白板功能，我们要求`TXBoardView`可以直接捕获用户的UI交互事件。

**创建一块白板的示例代码：**

```objc
TXBoardView *boardView = [[TXBoardView alloc] initWithFrame:frame];
[self.view addSubview:boardView];
```

### 3.2 设置白板的delegate

> 注意：如果使用 TICSDK，则不需要设置该代理对象，TICSDK内部已经实现了所有代理方法

为了使白板SDK正常运行，开发者需要在`TXBoardView`中设置满足`TXBoardViewDelegate`声明的delegate对象。

**delegate声明：**

```objc
#pragma mark - 白板代理
@protocol TXBoardViewDelegate <NSObject>

- (void)sendMessage:(NSDictionary *)message;

- (void)uploadImage:(NSString *)imagePath succ:(TXSuccBlock)succ failed:(TXFailBlock)failed;

- (void)downloadImage:(NSString *)imageURL succ:(TXSuccBlock)succ failed:(TXFailBlock)failed;

- (uint32_t)getTimestamp;

- (TXBoardDataConfig *)getBoardDataConfig;

@end

```

**方法说明：**

接口 | 说明
---|---
sendMessage: | 向网络中其他白板终端发送协议数据，开发者可以透传NSDictionary的json字符串
getTimestamp | 获取秒级的时间戳，在多终端白板互通场景下使用服务器时间
getBoardDataConfig | 获取白板所需外部参数，包含sdkAppId、uid、userSig、roomID
uploadImage:succ:failed | 上传指定路径上的图片文件，返回下载url
downloadImage:succ:failed | 下载指定url的图片文件，返回数据


### 3.3 选择白板的画笔状态

开发者使用白板SDK过程中，需要主动设置白板的画笔类型，才能实现画线、橡皮擦、缩放、添加标准图形等操作。

**相关接口：**

```objc

typedef NS_ENUM(NSInteger, TXBoardBrushModel)
{
    TXBoardBrushModelNone = 0,
    TXBoardBrushModelLine = 1,  //线条（默认）
    TXBoardBrushModelEraser,    //橡皮擦
    TXBoardBrushModelTransform, //缩放
    TXBoardBrushModelTapSel,    //点击选择涂鸦
    TXBoardBrushModelRectSel,   //框选涂鸦
    TXBoardBrushModelSegment,   //直线
    TXBoardBrushModelOval,      //椭圆
    TXBoardBrushModelRound,     //正圆
    TXBoardBrushModelRectangle, //矩形
};

@interface TXBoardView : UIView

- (void)setBrushModel:(TXBoardBrushModel)model;

- (TXBoardBrushModel)getBrushModel;

@end

```

当选择对应的画笔类型后，用户操作白板区域时，会展示对应的效果。

### 3.4 白板的接口列表

除了通过设置白板模式参数，调整白板功能外，开发者可以调用`TXBoardView`的其他接口，触发白板功能。
例如：创建子白板、更新背景图、选择颜色等操作。

**TXBoardView接口声明：**

```objc

@interface TXBoardView : UIView

#pragma mark - 白板配置
@property (nonatomic, weak) id<TXBoardViewDelegate> boardViewDelegate;

- (NSString *)currentBoardId;

- (NSString *)createSubBoard;

- (BOOL)switchToSubBoard:(NSString *)boardId;

- (BOOL)deleteSubBoard:(NSArray<NSString *> *)boardIds stayBoard:(NSString *)stayBoard;

- (NSArray<NSString *> *)boardList;

#pragma mark - 更新背景图片
- (void)updateBgImageWithPath:(NSString *)imagePath mode:(TXBoardImageMode)mode  succ:(TXSuccBlock)succ failed:(TXFailBlock)failed;//本地路径

- (void)updateBgImageWithURL:(NSString *)imageURL mode:(TXBoardImageMode)mode  succ:(TXSuccBlock)succ failed:(TXFailBlock)failed;//远程URL

#pragma mark - 画笔相关
- (void)setBrushColor:(UIColor *)color;
- (UIColor *)getBrushColor;

- (void)setBrushWidth:(CGFloat)width;
- (CGFloat)getBrushWidth;

- (void)setBrushModel:(TXBoardBrushModel)model;
- (TXBoardBrushModel)getBrushModel;

#pragma mark - 橡皮
- (void)setEraserRadius:(CGFloat)radius;

- (CGFloat)getEraserRadius;

#pragma mark - 白板
- (void)setBackgroundColor:(UIColor *)color;

- (void)setGlobalBackgroundColor:(UIColor *)color;

- (void)clear;

- (void)clearDraws;

- (void)saveToAlbumWithFinish:(void (^)())finishBlcok;

- (void)undo;

- (BOOL)canUndo;

- (void)redo;

- (BOOL)canRedo;

#pragma mark - 数据

- (void)recvBoardViewData:(NSArray<NSDictionary *> *)data;

- (NSArray<TXBoardData *> *)getSnapShot;

- (void)getBoardData:(void (^)(void))succ failed:(void (^)(void))failed;

@end

```

**白板的基本功能：**

接口 | 说明
---|---
setBrushColor: | 设置画线、添加标准图形时线条的颜色
getBrushColor | 获取当前画笔颜色
setBrushWidth: | 设置画线、添加标准图形时线条的宽度
getBrushWidth | 获取当前画笔宽度
setEraserRadius: | 设置擦除效果的范围半径
getEraserRadius: | 获取擦除效果的范围半径
setBackgroundColor: | 设置当前白板背景颜色
setGlobalBackgroundColor: | 设置全局白板背景颜色
clear: | 清空当前白板所有数据，包含背景图片
clearDraws: | 清空当前白板涂鸦数据，不包含背景图片、PPT
undo | 撤销上一步操作
canUndo | 获取是否可以进行撤回操作
redo | 重做上一步被撤回的操作
canRedo | 获取是否可以进行重做操作

**创建多个白板的接口：**

接口 | 说明
---|---
currentBoardId | 获取当前的白板实例id，默认的id为字符串 #DEFAULT
createSubBoard | 创建一个内部白板实例，返回标识id；创建白板后默认使用#DEFAULT为id白板实例；
switchToSubBoard | 切换当前白板的展示内容，返回切换结果
deleteSubBoard:stayBoard: | 删除一系列白板实例，指定当前白板展示内容，返回结果；SDK不允许删除#DEFAULT的白板实例；
boardList | 返回所有白板ID数组

**数据的接收与同步：**

接口 | 说明
---|---
recvBoardViewData: | 填入远端的白板操作数据，白板会同步展示远端画面

接口 | 说明
---|---
getBoardData:failed: | 拉取白板数据（加入课堂后，从服务器拉取课堂白板数据，填充白板））


## 4. 白板数据实时收发

**白板操作端捕获操作白板的数据：**

```objc

@protocol TXBoardViewDelegate <NSObject>

- (int)sendMessage:(NSDictionary *)message;

@end

```

**白板观看端展示白板画面：**

```objc

@interface TXBoardView : UIView

- (void)recvBoardViewData:(NSArray<NSDictionary *> *)data;

@end

```

<!--**Demo中实时数据传输方案：**
在线教育解决方案，使用[腾讯云通信](https://cloud.tencent.com/document/product/269/1569#1.7-.E8.87.AA.E5.AE.9A.E4.B9.89.E6.B6.88.E6.81.AF.E5.8F.91.E9.80.81)提供的群组聊天能力，实现多个用户白板画面的同步功能。
1. 所有用户加入同一个IM群组中。
2. 发送的数据小于7K时，使用`TIMCustomElem`类型消息发送数据。`TIMOfflinePushInfo`中的`ext`字段设置为"TXWhiteBoardExt"，`TIMCustomElem`中的`ext`字段设置为"TXWhiteBoardExt"。
3. 如果发送的数据大于7K时，使用TIMFileElem类型消息发送数据。TIMOfflinePushInfo中的ext字段设置为"TXWhiteBoardExt"，TIMFileElem中的filename字段设置为"TXWhiteBoardExt"
4. 接收端根据`TIMOfflinepushInfo`中`ext`字段的字符串信息，对消息中内容进行还原，还原结果填充回白板对象中。

详见Demo代码。-->

## 5. 白板数据上报备份和拉取填充

课堂中，老师对白板的操作，涂鸦、图片、PPT、撤销、清空等操作需要上报到后台，并进行存储，这样后面中途加入课堂的成员就能拉取之前的白板数据进行展示。

该过程主要分为两步，数据上报和数据拉取：

**白板数据上报：**
在每次对白板操作后，SDK会将操作的数据上报到白板后台，目前表白SDK已经内部实现了该功能，白板后台服务也是我们在维护，用户无需自行实现。

**白板数据拉取（同步）：**
数据拉取在白板中提供了一个接口，用户只需要在进房成功之后调用该接口拉取白板数据即可， 方法内部已经实现了数据的解析即填充到白板的功能。（包括异常退出重新进入房间时同步数据的场景）

```objc

@interface TXBoardView : UIView

/**
 拉取白板数据（加入课堂后，从服务器拉取课堂白板数据，填充白板）
 */
- (void)getBoardData:(void (^)())succ failed:(void (^)())failed;

@end

```






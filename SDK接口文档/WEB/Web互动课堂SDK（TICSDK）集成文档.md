# 腾讯互动课堂SDK（TICSDK）集成使用文档
## 1. 简介
腾讯互动课堂（Tencent Interact Class，TIC）SDK 是一个提供在线教育场景下综合解决方案，它对`WebRTCAPI`、`boardSDK`、`ImSDK`和`COSSDK`等SDK进行了业务封装，提供了【多人音视频】，【多人即时通信】，【多人互动画板】【文档云端转码预览】等功能。适用于在线互动课堂，在线会议，你画我猜等场景。

## 2.准备工作
TICSDK使用了实时音视频服务（WebRTCAPI）、云通讯服务（IMSDK）、COS服务等腾讯云服务能力，在使用腾讯互动课堂服务时，请对点时间了解以上服务的基本概念和基本业务流程。

[实时音视频](https://cloud.tencent.com/document/product/647) 提供了实时音视频通话的能力

[云通讯服务（IMSDK）](https://cloud.tencent.com/document/product/269/1504) 提供单聊、群聊

[COS服务](https://cloud.tencent.com/document/product/436/6225) 提供云端存储以及文档在线预览服务

## 3. TICSDK接口简介

先总体说明下SDK中暴露的接口的主要功能：

类名 | 主要功能
--------- | ---------
TICSDK | 整个SDK的入口类，提供了SDK【初始化】、【登录/登出SDK】、【创建/加入/销毁课堂】、【音视频操作】、【IM操作】以及【获取IMSDK实例、WebRTCAPI实例、白板实例，COS实例】的接口


## 4. 业务流程图


## 5.集成SDK

> 完成以下三步，即可简单实现互动课堂

#### 5.1 加载必须的SDK
```
<!-- WebRTC SDK -->
<script src="https://sqimg.qq.com/expert_qq/webrtc/2.2/WebRTCAPI.min.js"></script>
<!-- WebIM SDK -->
<script src="https://sqimg.qq.com/expert_qq/webim/1.7.1/webim.min.js"></script>
<!-- 白板SDK -->
<script src="./libs/sketchpad_sdk.mini.js"></script>
<!-- COS SDK -->
<script src="./libs/cos.mini.js"></script>
<!-- TIC SDK -->
<script src="./libs/TICSDK.js"></script>
```

#### 5.2 初始化TICSDK，并监听TICSDK关键事件

```
// 初始化TICSDK
this.ticSdk = new TICSDK();
this.ticSdk.init();

// 监听登录成功事件 老师创建课堂，学生则加入课堂
this.ticSdk.on(TICSDK.CONSTANT.EVENT.IM.LOGIN_SUCC, res => {
  if (是老师) {
    // 老师就创建课堂
    this.ticSdk.createClassroom({
      roomID: 房间号
    });
  } else { // 如果是学生
    this.ticSdk.joinClassroom(房间号, webrtc推流配置, 白板配置);
  }
});

// 监听创建课堂成功
this.ticSdk.on(TICSDK.CONSTANT.EVENT.TIC.CREATE_CLASS_ROOM_SUCC, (res) => {
  if (是老师) {
    this.ticSdk.joinClassroom(房间号, webrtc推流配置, 白板配置, COS配置);
  }
});

// 监听接收到本地流
this.ticSdk.on(TICSDK.CONSTANT.EVENT.WEBRTC.LOCAL_STREAM_ADD, data => {
  document.getElementById('local_video').srcObject = data.stream;
});

// 监听接收到远端流
this.ticSdk.on(TICSDK.CONSTANT.EVENT.WEBRTC.REMOTE_STREAM_UPDATE, data => {
  document.getElementById('remote_video').srcObject = data.stream;
});

```

roomID参数：
参数名 | 类型 | 是否必填 | 备注
--------- | --------- | -----| ---
roomID | integer | 是 | 由业务方下发，并保证每次下发的roomID是唯一不重复的。

webrtc推流配置参数：

参数	| 类型	| 是否必填 | 描述
--------- | --------- | ----- | --------- |
closeLocalMedia | boolean | 否，默认 false | 是否关闭自动推流（如果置为 true，则在完成加入/建房操作后，不会发起本端的推流，如需推流，需要由业务主动调推流接口 ）
audio | boolean | 否，默认 true | 是否启用音频采集
video | boolean | 否，默认 true | 是否启用视频采集

白板配置参数：

参数	| 类型	| 是否必填 | 描述
--------- | --------- | ----- | --------- |
id | string | 是 | 白板渲染的在dom节点id，并保证该节点有position: relative样式，否则可能会引起白板定位异常的问题。
canDraw | boolean | 否，默认 false | 默认白板是不能进行涂鸦，如果需要进行涂鸦请设置为true
color | string | 否，默认红色 |画笔颜色，只接受hex色值，如#ff00ff，大小写不敏感
globalBackgroundColor | string | 否，默认白色 | 全局的白板背景色


COS配置：

参数	| 类型	| 是否必填 | 描述
--------- | --------- | ----- | --------- |
appid | string | 是 | APPID 是腾讯云账户的账户标识之一。在[腾讯云账号中心](https://console.cloud.tencent.com/developer)中可以看到。
bucket | string | 是 | 在 COS 中用于存储对象。一个存储桶中可以存储多个对象。在[COS控制台](https://console.cloud.tencent.com/cos5/bucket)中可以看到
region | string | 是 | 地域即 Region，表示 COS 的数据中心所在的地域。在[COS控制台](https://console.cloud.tencent.com/cos5/bucket)中可以看到
sign | string | 是 | COS鉴权sign，需要业务方自行下发

#### 5.3 登录TICSDK

```
this.ticSdk.login(loginConfig);
```

loginConfig参数：
参数名 | 是否必填 | 备注
--------- | --------- | -----
identifier | 是 | 用户名
identifierNick | 否 | 用户昵称，不填则使用identifier
userSig | 是 | 登录鉴权信息
sdkAppId | 是 | 腾讯云应用的唯一标识，可以登录[实时音视频控制台](https://console.qcloud.com/rav)查看
accountType | 是 | 腾讯云应用的账号类型，可以登录[实时音视频控制台](https://console.qcloud.com/rav)，选择指定的应用后，在功能配置页面中查看

## 6.常见问题



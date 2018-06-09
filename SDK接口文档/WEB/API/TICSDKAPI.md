<a name="TICSDK"></a>

## TICSDK
**Kind**: global class  
**Version**: 2.0.0  

* [TICSDK](#TICSDK)
    * [new TICSDK()](#new_TICSDK_new)
    * _instance_
        * [.init()](#TICSDK+init)
        * [.login(loginConfig)](#TICSDK+login)
        * [.on(name, callback)](#TICSDK+on)
        * [.getSketchInstance()](#TICSDK+getSketchInstance) ⇒ <code>Sketch</code>
        * [.getImInstance()](#TICSDK+getImInstance) ⇒ <code>webim</code>
        * [.getWebRTCInstance()](#TICSDK+getWebRTCInstance) ⇒ <code>WebRTC</code>
        * [.createClassroom(课堂信息)](#TICSDK+createClassroom)
        * [.joinClassroom(roomID, webrtcConfig, boardConfig, cosConfig)](#TICSDK+joinClassroom)
        * [.quitClassroom()](#TICSDK+quitClassroom)
        * [.destroyClassRoom()](#TICSDK+destroyClassRoom)
        * [.getCameraDevices(callback)](#TICSDK+getCameraDevices)
        * [.getMicDevices(callback)](#TICSDK+getMicDevices)
        * [.startRTC()](#TICSDK+startRTC)
        * [.enableCamera(true)](#TICSDK+enableCamera)
        * [.switchCamera(device)](#TICSDK+switchCamera)
        * [.enableMic(true)](#TICSDK+enableMic)
        * [.switchMic(device)](#TICSDK+switchMic)
        * [.sendC2CTextMessage(receiveUserIdentifier, msgText)](#TICSDK+sendC2CTextMessage)
        * [.sendC2CCustomMessage(receiveUserIdentifier, msgObj)](#TICSDK+sendC2CCustomMessage)
        * [.sendGroupTextMessage(msgText)](#TICSDK+sendGroupTextMessage)
        * [.sendGroupCustomMessage(msgObject)](#TICSDK+sendGroupCustomMessage)
        * [.uploadFile(file, succ, fail)](#TICSDK+uploadFile)
        * [.logout()](#TICSDK+logout)
    * _static_
        * [.CONSTANT](#TICSDK.CONSTANT) : <code>string</code>

<a name="new_TICSDK_new"></a>

### new TICSDK()
TICSDK 互动课堂入口类

<a name="TICSDK+init"></a>

### ticsdK.init()
TICSDK初始化

**Kind**: instance method of [<code>TICSDK</code>](#TICSDK)  
<a name="TICSDK+login"></a>

### ticsdK.login(loginConfig)
TICKSDK登录 抛出登录成功和登录失败事件

**Kind**: instance method of [<code>TICSDK</code>](#TICSDK)  

| Param | Type | Description |
| --- | --- | --- |
| loginConfig | <code>Object</code> | 登录信息 |

<a name="TICSDK+on"></a>

### ticsdK.on(name, callback)
事件监听

**Kind**: instance method of [<code>TICSDK</code>](#TICSDK)  

| Param | Type | Description |
| --- | --- | --- |
| name | <code>String</code> | 事件名称 |
| callback | <code>function</code> | 事件回调 |

<a name="TICSDK+getSketchInstance"></a>

### ticsdK.getSketchInstance() ⇒ <code>Sketch</code>
获取白板实例， 白板实例需要在监听到进房成功事件[TICSDK.CONSTANT.EVENT.TIC.JOIN_CLASS_ROOM_SUCC]()后才返回

**Kind**: instance method of [<code>TICSDK</code>](#TICSDK)  
**Returns**: <code>Sketch</code> - sketch 返回白板实例，操作白板请查看[白板API](白板SDKAPI)  
<a name="TICSDK+getImInstance"></a>

### ticsdK.getImInstance() ⇒ <code>webim</code>
获取IM实例, 初始化TICKSDK后即可获得IM实例

**Kind**: instance method of [<code>TICSDK</code>](#TICSDK)  
**Returns**: <code>webim</code> - im 返回IM实例  
<a name="TICSDK+getWebRTCInstance"></a>

### ticsdK.getWebRTCInstance() ⇒ <code>WebRTC</code>
获取WebRTC实例， WebRTC实例需要在监听到进房成功事件[TICSDK.CONSTANT.EVENT.TIC.JOIN_CLASS_ROOM_SUCC]()后才返回

**Kind**: instance method of [<code>TICSDK</code>](#TICSDK)  
**Returns**: <code>WebRTC</code> - cos 返回WebRTC实例  
<a name="TICSDK+createClassroom"></a>

### ticsdK.createClassroom(课堂信息)
创建课堂 抛出创建课堂成功和创建课堂失败的事件

**Kind**: instance method of [<code>TICSDK</code>](#TICSDK)  

| Param | Type |
| --- | --- |
| 课堂信息 | <code>Object</code> | 

<a name="TICSDK+joinClassroom"></a>

### ticsdK.joinClassroom(roomID, webrtcConfig, boardConfig, cosConfig)
加入课堂 抛出房间/课堂ID为空，加入课堂成功，加入课堂失败事件

**Kind**: instance method of [<code>TICSDK</code>](#TICSDK)  

| Param | Type | Description |
| --- | --- | --- |
| roomID | <code>Number</code> | 房间ID |
| webrtcConfig | <code>Object</code> | webrtc信息 |
| boardConfig | <code>Object</code> | 白板信息 |
| cosConfig | <code>Object</code> | cos信息 |

<a name="TICSDK+quitClassroom"></a>

### ticsdK.quitClassroom()
退出课堂 抛出退出课堂成功和退出课堂失败的事件

**Kind**: instance method of [<code>TICSDK</code>](#TICSDK)  
<a name="TICSDK+destroyClassRoom"></a>

### ticsdK.destroyClassRoom()
销毁课堂 只有创建创建者才能销毁课堂 抛出销毁课堂成功和销毁课堂失败的事件

**Kind**: instance method of [<code>TICSDK</code>](#TICSDK)  
<a name="TICSDK+getCameraDevices"></a>

### ticsdK.getCameraDevices(callback)
获取摄像头设备

**Kind**: instance method of [<code>TICSDK</code>](#TICSDK)  

| Param | Type | Description |
| --- | --- | --- |
| callback | <code>function</code> | 回调方法返回摄像头列表 |

<a name="TICSDK+getMicDevices"></a>

### ticsdK.getMicDevices(callback)
获取麦克风设备

**Kind**: instance method of [<code>TICSDK</code>](#TICSDK)  

| Param | Type | Description |
| --- | --- | --- |
| callback | <code>function</code> | 回调方法返回麦克风列表 |

<a name="TICSDK+startRTC"></a>

### ticsdK.startRTC()
开始推流，[手动推流](./H)才需用到

**Kind**: instance method of [<code>TICSDK</code>](#TICSDK)  
<a name="TICSDK+enableCamera"></a>

### ticsdK.enableCamera(true)
开启或者关闭摄像头

**Kind**: instance method of [<code>TICSDK</code>](#TICSDK)  

| Param | Type | Description |
| --- | --- | --- |
| true | <code>Boolean</code> | 开启摄像头； false 关闭摄像头 |

<a name="TICSDK+switchCamera"></a>

### ticsdK.switchCamera(device)
切换摄像头

**Kind**: instance method of [<code>TICSDK</code>](#TICSDK)  

| Param | Type | Description |
| --- | --- | --- |
| device | <code>Object</code> | 摄像头设备 通过<a href='#ticsdk-getcameradevices-callback-'>getCameraDevices</a>获取摄像头设备 |

<a name="TICSDK+enableMic"></a>

### ticsdK.enableMic(true)
开启或者关闭麦克风

**Kind**: instance method of [<code>TICSDK</code>](#TICSDK)  

| Param | Type | Description |
| --- | --- | --- |
| true | <code>Boolean</code> | 开启麦克风； false 关闭麦克风 |

<a name="TICSDK+switchMic"></a>

### ticsdK.switchMic(device)
切换麦克风

**Kind**: instance method of [<code>TICSDK</code>](#TICSDK)  

| Param | Type | Description |
| --- | --- | --- |
| device | <code>Object</code> | 麦克风设备，通过<a href='#ticsdk-getmicdevices-callback-'>getMicDevices</a>获取麦克风设备 |

<a name="TICSDK+sendC2CTextMessage"></a>

### ticsdK.sendC2CTextMessage(receiveUserIdentifier, msgText)
发送私聊文本消息

**Kind**: instance method of [<code>TICSDK</code>](#TICSDK)  

| Param | Type | Description |
| --- | --- | --- |
| receiveUserIdentifier | <code>String</code> | 接收方用户名 |
| msgText | <code>String</code> | 要发送的消息内容 |

<a name="TICSDK+sendC2CCustomMessage"></a>

### ticsdK.sendC2CCustomMessage(receiveUserIdentifier, msgObj)
发送私聊自定义文本消息对象

**Kind**: instance method of [<code>TICSDK</code>](#TICSDK)  

| Param | Type | Description |
| --- | --- | --- |
| receiveUserIdentifier | <code>String</code> | 接收方用户名 |
| msgObj | <code>Object</code> | 自定义文本消息对象 |

<a name="TICSDK+sendGroupTextMessage"></a>

### ticsdK.sendGroupTextMessage(msgText)
发送课堂群消息

**Kind**: instance method of [<code>TICSDK</code>](#TICSDK)  

| Param | Type | Description |
| --- | --- | --- |
| msgText | <code>String</code> | 要发送的消息文本内容 |

<a name="TICSDK+sendGroupCustomMessage"></a>

### ticsdK.sendGroupCustomMessage(msgObject)
发送课堂群消息

**Kind**: instance method of [<code>TICSDK</code>](#TICSDK)  

| Param | Type | Description |
| --- | --- | --- |
| msgObject | <code>Object</code> | 自定义文本消息对象 msgObject = {data: '发送的内容', desc: '描述', ext: '扩展'} |

<a name="TICSDK+uploadFile"></a>

### ticsdK.uploadFile(file, succ, fail)
上传文件, 支持图片和doc，docx, excel, ppt, pdf

**Kind**: instance method of [<code>TICSDK</code>](#TICSDK)  

| Param | Type | Description |
| --- | --- | --- |
| file | <code>File</code> | 文件对象，通常这样获取document.getElementById('file_input').files[0] |
| succ | <code>function</code> | 成功回调 如果文件类型是图片，回调函数参数第一个值是文件名，第二个参数为图片的url; 如果上传文件类型为doc，docx, excel, ppt, pdf， 回调函数第一个参数为该文档的总页数，第二个参数为文件信息，包含[文件名，文件下载地址，文件每一页预览的图片地址] |
| fail | <code>function</code> | 失败回调 |

<a name="TICSDK+logout"></a>

### ticsdK.logout()
TICKSDK登出 抛出登出成功和登出失败事件

**Kind**: instance method of [<code>TICSDK</code>](#TICSDK)  
<a name="TICSDK.CONSTANT"></a>

### TICSDK.CONSTANT : <code>string</code>
**Kind**: static constant of [<code>TICSDK</code>](#TICSDK)  

# 腾讯互动教育SDK接口文档

## 背景
为打造腾讯课堂一体化接入方案，在满足多种场景需求的前提下，简化客户接入流程，提高接入效率，给客户提供最好的服务体验。在现有的腾讯互动视频、云通讯和COS服务能力的基础上，构建简单好用的的互动教育服务。


## 关键字
* 课堂：Classroom
* 白板：Whiteboard
* 腾讯互动教育：Tencent Interact Class，TIC
* 腾讯互动教育SDK：TIC SDK


## 结构框图 

如下：

![](../../资源文件/结构框图.png)

## 主要接口

| 类                  	| 说明             |
| ------------------	| --------------- |
| TICSDK     			 	|  教育SDK总入口 	 |
| TICClassroomOption		|  课堂参数配置类 |
| TICManager    			|  教育SDK业务管理类 |
| TICWhiteboardManager    	|  白板业务管理类 |
| TICSDKCosConfig    		|  COS管理类 |
| IClassroomIMListener 		| 课堂IM消息监听接口 |
| IClassroomWhiteboardListener | 课堂白板绘制数据回调监听接口|
| IClassEventListener 		| 课堂事件监听器|




### TICSDK
TICSDK是使用教育服务SDK的总入口，主要是SDK的初始化工作，主要接口如下：

| 主要方法                  	| 说明             |
| ------------------		| ---------------    |
| GetSDKInstance   			|  教育SDK总入口      |
| getVersion    			|  获取版本信息     |
| initSDK					|  初始化TICSDK     |
| uninitSDK					|  反初始化TICSDK     |
| initWhiteBoard			|  初始化白板SDK     |
| getTICManager				|  获得TICManager实例     |
| getTICWhiteBoardManager	|  获得TICWhiteBoardManager实例     |

```C++
	/**
	@brief 获取版本号
	@return 版本号
	*/
	static const char* getVersion();
	
	/**
	@brief 获取TICSDK实例指针
	@return TICSDK指针
	*/
	static TICSDK* GetSDKInstance();
	
	/**
	@brief 初始化TICSDK
	@param iLiveSDKAppId 腾讯云控制台注册的应用ID
	@param iLiveAccountType腾讯云控制台注册的应用的账号类型
	@return 初始化结果，0代表成功，其他代表失败
	*/
	virtual int initSDK(int iLiveSDKAppId, int iLiveAccountType) = 0;
	
	/**
	@brief 反初始化TICSDK
	*/
	virtual void uninitSDK() = 0;
	
	/**
	@brief 初始化白板SDK，在加入房间之后
	@param id 用户id
	@param classID 课堂ID
	@param parentHWnd 白板父窗口句柄
	@return 结果，0表示成功
	*/
	virtual int initWhiteBoard(const char* id, HWND parentHWnd = nullptr) = 0;
	
	/**
	@brief 获取TICManager实例指针
	@return TICManager指针
	*/
	virtual TICManager* getTICManager() = 0;
	
	/**
	@brief 获取白板管理类实例指针
	@return 白板管理类指针
	*/
	virtual TICWhiteboardManager* getTICWhiteBoardManager() = 0;	
```

### TICClassroomOption
课堂参数配置类，主要是用于创建课堂或者加入课堂时的参数配置，暂时定义如下（还不够完整，需要持续更新）：

| 主要配置项             | 说明                |
| ------------------	|  ---------------    |
| setRoomID     		|  设置房间ID     |
| setRoomOption     	|  设置进房间参数配置      |
| setIsTeacher			|  设置是否为老师    |
| classroomWhiteboardListener   |	课堂白板绘制事件回调 |
| classroomIMListener     		|	课堂文字互动消息事件回调 |
| classEventListener     		| 课堂事件监听器     |

回调接口定义如下：

| 接口             |回调方法     			| 说明                |
| ------------------	| -------------	| ---------------    |
| **IClassroomIMListener**     	|onRecvC2CTextMsg |  收到C2C文本消息      |
|     	| 	onRecvC2CCustomMsg		|  收到C2C自定义消息      |
|		| 	onRecvGroupTextMsg		|  开启白板，默认true，开启      |
|     	|	onRecvGroupCustomMsg|  收到Group文本消息 |
|		|	onRecvGroupSystemMsg|  收到Group系统消息 |
|		|	onSendMsg|  发送IM消息 |
|		|	onSendWBData|  发送白板消息 |
| **IClassroomWhiteboardListener**  |onStatusChanged|  通知白板状态变化 |
|		|	onGetBoardData|  白板数据同步 |
|		|	onUploadProgress|  文件上传进度 |
|		|	onUploadResult|  图片文件上传结果 |
|		|	onFileUploadResult|  PPT文件上传结果 |
| **IClassEventListener**  |onLiveVideoDisconnect|  视频流异常退出 |
|   |onMemStatusChange|  成员状态变化通知|
|   |onCreateClassroom|  创建房间成功通知|




### TICManager
课堂业务管理类，负责课堂管理和课堂互动管理等主要业务。主要业务接口如下：

| 主要接口                  	| 说明（括号里标识改接口为某端特有）             |
| ------------------	| ---------------       |
| init     			 	|  初始化      |
| login     			 	|  IM登陆      |
| logout     			 	|  注销登陆      |
| startRecord     			 	|  开始课堂录制      |
| stopRecord     			 	|  结束课堂录制      |
| setCosHandler     			 |  设置cos信息      |
| createClassroom    			|  创建课堂    |
| joinClassroom    			|  加入互动课堂    |
| quitClassroom    			| 中途退出课堂，可重新进入    |
| enableCamera    			|  打开/关闭摄像头    |
| switchCamera    			|  前后摄像头切换    |
| enableMic    			|  打开/关闭麦克风    |
| enableSpeaker				| 打开/关闭扬声器  |
| switchMic    			|  切换麦克风(Web)    |
| openScreenShare    			|  开启屏幕分享    |
| changeScreenShareSize			|  修改屏幕分享的区域    |
| closeScreenShare				|  关闭屏幕共享         |
| openPlayMediaFile    			|  开启播片功能    |
| closePlayMediaFile    		|  关闭播片功能    |
| setLocalVideoCallBack    			|  设置本地数据回调   |
| setRemoteVideoCallBack    		|  设置远端数据回调   |
| setForceOfflineCallback    		|  设置强制下线通知   |
| setDeviceOperationCallback    	|  设置设备操作回调   |
| sendC2CTextMessage    			|  发送C2C文本消息    |
| sendC2CCustomMessage    			|  发送C2C自定义消息    |
| sendGroupTextMessage    			|  发送群文本消息    |
| sendGroupCustomMessage    		|  发送群组自定义消息    |
| uploadFile    					|  上传文件到cos   |

详细说明如下

```C++
	/**
	* \brief 登录iliveSDK
	* \param id 用户ID
	* \param sig 用户签名
	* \param success 登录成功回调
	* \param err		登录错误回调
	* \param data   用户自定义数据
	* \return 结果，0表示成功
	*/
	virtual int login(const char * id, const char * userSig, ilive::iLiveSucCallback success = nullptr, ilive::iLiveErrCallback err = nullptr, void* data = nullptr) = 0;

	/**
	* \brief 登出iliveSDK
	* \param success 成功回调
	* \param err 错误回调
	* \param data   用户自定义数据
	*/
	virtual void logout(ilive::iLiveSucCallback success = nullptr, ilive::iLiveErrCallback err = nullptr, void* data = nullptr) = 0;

	/**
	* \brief 获取iliveSDK实例指针
	* \return iliveSDK指针
	*/
	virtual ilive::iLive* GetILive() = 0;

	/**
	* \brief 创建课堂
	* \param roomID 课堂房间ID
	* \param listener 创建课堂回调指针
	*/
	virtual void createClassroom(uint32_t roomID, IClassroomEventListener* listener = nullptr) = 0;

	/**
	* \brief 加入课堂
	* \param opt 课堂配置类对象
	* \param success 加入课堂成功回调
	* \param err 加入课堂失败回调
	*/
	virtual void joinClassroom(TICClassroomOption& opt, ilive::iLiveSucCallback success = nullptr, ilive::iLiveErrCallback err = nullptr, void* data = nullptr) = 0;

	/**
	* \brief 退出课堂
	* \param success 退出课堂成功回调
	* \param err 退出课堂失败回调
	*/
	virtual void quitClassroom(ilive::iLiveSucCallback success = nullptr, ilive::iLiveErrCallback err = nullptr, void* data = nullptr) = 0;

	/**
	* \brief 开始录制
	*/
	virtual void startRecord() = 0;

	/**
	* \brief 结束录制
	*/
	virtual void stopRecord() = 0;
	
	/**
	* \brief 打开/关闭摄像头
	* \param enable   true：打开默认摄像头；false：关闭
	*/
	virtual void enableCamera(bool bEnable) = 0;

	/**
	* \brief 切换摄像头
	* \param cameraId   摄像头设备标识
	*/
	virtual void switchCamera(const char* cameraId) = 0;

	/**
	* \brief 打开/关闭麦克风
	* \param enable   true：打开默认麦克风；false：关闭
	*/
	virtual void enableMic(bool bEnable) = 0;

	/**
	* \brief 切换麦克风
	* \param deviceID   麦克风设备标识
	*/
	virtual void switchMic(const char* deviceID) = 0;

	/**
	* \brief 打开/关闭扬声器
	* \param enable   true：打开默认扬声器；false：关闭
	*/
	virtual void enablePlayer(bool bEnable) = 0;

	/**
	* \brief 设置本地视频预览回调
	* \param OnLocalVideo   回调函数接口
	* \param data   用户自定义数据
	*/
	virtual void setLocalVideoCallBack(ilive::iLivePreviewCallback OnLocalVideo, void* data = nullptr) = 0;

	/**
	* \brief 设置远程视频数据接收
	* \param OnRemoteVideo   回调函数接口
	* \param data   用户自定义数据
	*/
	virtual void setRemoteVideoCallBack(ilive::iLivePreviewCallback OnRemoteVideo, void* data = nullptr) = 0;

	/**
	* \brief 设置设备操作回调
	* \param OnDeviceOperation   回调函数接口
	* \param data   用户自定义数据
	*/
	virtual void setDeviceOperationCallback(ilive::iLiveDeviceOperationCallback OnDeviceOperation, void* data = nullptr) = 0;

	/**
	* \brief 设置被踢下线回调
	* \param OnForceOffline   回调函数接口
	*/
	virtual void setForceOfflineCallback(ilive::ForceOfflineCallback OnForceOffline) = 0;

	/**
	* \brief 打开屏幕分享(指定窗口)
	* \param hWnd 所要捕获的窗口句柄(NULL表示全屏)
	* \param fps 捕获帧率
	*/
	virtual void openScreenShare(HWND hWnd, uint32& fps) = 0;

	/**
	* \brief 打开屏幕共享(指定区域)
	* \param left/top/right/bottom 所要捕获屏幕画面的区域的左上角坐标(left, top)和右下角坐标(right, bottom)
	* \param fps 捕获帧率
	*/
	virtual void openScreenShare(int32& left, int32& top, int32& right, int32& bottom, uint32& fps) = 0;

	/**
	* \brief 动态修改屏幕分享的区域
	* \param left/top/right/bottom 所要捕获屏幕画面的区域的左上角坐标(left, top)和右下角坐标(right, bottom)
	* \param fps 捕获帧率
	*/
	virtual int changeScreenShareSize(int32& left, int32& top, int32& right, int32& bottom) = 0;

	/**
	* \brief 关闭屏幕共享
	*/
	virtual void closeScreenShare() = 0;

	/**
	* \brief 打开文件播放
	* \param [in] szMediaFile 文件路径(可以是本地文件路径，也可以是一个网络文件的url);
	*/
	virtual void openPlayMediaFile(const char* szMediaFile) = 0;

	/**
	* \brief 关闭文件播放
	*/
	virtual void closePlayMediaFile() = 0;

	/**
	* \brief 从头播放文件
	* \return 操作结果，0表示无错误
	*/
	virtual int restartMediaFile() = 0;

	/**
	* \brief 暂停播放文件
	* \return 操作结果，0表示无错误
	*/
	virtual int pausePlayMediaFile() = 0;

	/**
	* \brief 恢复播放文件
	* \return 操作结果，0表示无错误
	*/
	virtual int	resumePlayMediaFile() = 0;

	/**
	* \brief 设置播放文件进度
	* \param n64Pos 播放位置(单位: 秒)
	* \return 操作结果，0表示无错误
	*/
	virtual int setPlayMediaFilePos(const int64& n64Pos) = 0;

	/**
	* \brief 获取播放文件进度。
	* \param n64Pos 当前播放位置(单位: 秒)
	* \param n64MaxPos 当前所播放文件的总长度(单位: 秒)
	* \return 操作结果，0表示无错误。
	*/
	virtual int getPlayMediaFilePos(int64& n64Pos, int64& n64MaxPos) = 0;

	/**
	* \brief 发送C2C文本消息
	* \param identifier   消息接收者
	* \param msg  发送内容
	* \param OnSuccess 发送成功回调
	* \param OnError   发送失败回调
	*/
	virtual void sendC2CTextMsg(const char * identifier, const char * msg) = 0;

	/**
	* \brief 发送群文本消息
	* \param msg  发送内容
	* \param OnSuccess 发送成功回调
	* \param OnError   发送失败回调
	*/
	virtual void sendGroupTextMsg(const char * msg) = 0;

	/**
	* \brief 发送C2C自定义消息
	* \param identifier   消息接收者
	* \param msg  发送内容
	* \param OnSuccess 发送成功回调
	* \param OnError   发送失败回调
	*/
	virtual void sendC2CCustomMsg(const char * identifier, const char * msg) = 0;

	/**
	* \brief 发送群组自定义消息
	* \param msg  发送内容
	* \param OnSuccess 发送成功回调
	* \param OnError   发送失败回调
	*/
	virtual void sendGroupCustomMsg(const char * msg) = 0;

	/**
	* \brief 设置COS参数配置
	* \param cfg  COS配置
	*/
	virtual void setCosHandler(TICSDKCosConfig cfg) = 0;

	/**
	* \brief 上传文件到cos
	* \param fileName   文件名
	*/
	virtual void uploadFile(const std::wstring& fileName) = 0;

	/**
	* \brief 上传文件到cos
	* \param fileName   文件名
	* \param sig			cos签名
	*/
	virtual void uploadFile(const std::wstring& fileName, std::string& sig) = 0;

	/**
	* \brief 获得上传地址
	* \param obj_name cos文件名
	*/
	virtual std::wstring getUploadUrl(const std::wstring &obj_name) = 0;

	/**
	* \brief 获得下载地址
	* \param obj_name cos文件名
	*/
	virtual std::wstring getDownloadUrl(const std::wstring &obj_name) = 0;

	/**
	* \brief 获得预览地址
	* \param obj_name cos文件名
	*/
	virtual std::wstring getPreviewUrl(const std::wstring &obj_name, int page) = 0;

```    
    
## TICWhiteboardManager
白板管理类，负责对白板SDK接口的管理和封装，。主要业务接口如下：

| 主要接口                  	| 说明（括号里标识改接口为某端特有）             |
| ------------------	| ---------------       |
| getTICWhiteBoard     	|  获得白板SDK实例     |
| getRenderWindow     	|  获得白板窗口句柄    |
| clearWhiteBoard     	|  清空白板对象    |
| useTool     			 	|  使用画板工具      |
| setWidth     			 	|  设置线宽      |
| setColor     			 	|  设置颜色      |
| setFill     				|  设置填充      |
| undo    					|  撤销    |
| redo    					|  重做    |
| remove    				|  删除    |
| clear    					|  清除白板数据    |
| clearDraws    			|  清除白板涂鸦    |
| useBackground    			|  设置白板背景    |
| setBackgroundColor		| 设置白板背景色  |
| setAllBackgroundColor    	|  设置全局背景色   |
| getBoardData    			|  拉取离线数据    |
| getPageIndex				|  获取当前页码  |
| getPageCount				|  获取总页数    |
| refreshPageInfo    		|  刷新页码    |
| gotoPage    				|  页码跳转 |
| gotoLastPage    			|  跳转上一页  |
| gotoNextPage    			|  跳转下一页   |
| insertPage    			|  插入新的一页   |
| deletePage    			|  删除当前页   |
| addPage    				|  新增一页    |
| addFile    				|  添加一个PPT所有页并生成白板    |


详细说明如下
```C++

	/**
	* \brief 获得白板窗口句柄
	*/
	virtual HWND getRenderWindow() = 0;
	
	/**
	* \brief 清空白板数据
	*/
	virtual void clearWhiteBoard() = 0;
	
	/**
	* \brief 使用画板工具
	* \param tool  画板工具
	*/
	virtual void useTool(BoardTool tool) = 0;
	
	/**
	* \brief 设置线宽
	* \param width  宽度
	*/
	virtual void setWidth(uint32_t width) = 0;
	
	/**
	* \brief 设置颜色
	* \param rgba  颜色RGBA值
	*/
	virtual void setColor(uint32_t rgba) = 0;
	
	/**
	* \brief 设置填充
	* \param fill  是否填充
	*/
	virtual void setFill(bool fill) = 0;
	
	/**
	* \brief 撤销
	*/
	virtual void undo() = 0;
	
	/**
	* \brief 重做
	*/
	virtual void redo() = 0;
	
	/**
	* \brief 删除
	*/
	virtual void remove() = 0;
	
	/**
	* \brief 清除白板
	*/
	virtual void clear() = 0;
	
	/**
	* \brief 清除涂鸦
	*/
	virtual void clearDraws() = 0;
	
	/**
	* \brief 设置白板背景
	* \param url  背景图地址
	* \param pageID 白板ID，默认为当前白板
	*/
	virtual void useBackground(const wchar_t *url, const char *pageID = nullptr) = 0;
	
	/**
	* \brief 设置白板背景色
	* \param rgba  颜色RGBA值
	*/
	virtual void setBackgroundColor(uint32_t rgba) = 0;
	
	/**
	* \brief 设置全局背景色
	* \param rgba  颜色RGBA值
	*/
	virtual void setAllBackgroundColor(uint32_t rgba) = 0;
	
	/**
	* \brief 拉取离线数据
	*/
	virtual void getBoardData() = 0;
	
	/**
	* \brief 获取当前页码
	* \return 当前页码
	*/
	virtual uint32_t getPageIndex() = 0;
	
	/**
	* \brief 获取总页数
	* \return 总页数
	*/
	virtual uint32_t getPageCount() = 0;
	
	/**
	* \brief 刷新页码
	*/
	virtual void refreshPageInfo() = 0;
	
	/**
	* \brief 页码跳转
	* \param pageIndex  跳转的页码
	*/
	virtual void gotoPage(uint32_t pageIndex) = 0;
	
	/**
	* \brief 跳转上一页
	*/
	virtual void gotoLastPage() = 0;
	
	/**
	* \brief 跳转下一页
	*/
	virtual void gotoNextPage() = 0;
	
	/**
	* \brief 插入新的一页
	*/
	virtual void insertPage() = 0;
	
	/**
	* \brief 删除当前页
	*/
	virtual void deletePage() = 0;
	
	/**
	* \brief 新增一页（用户指定白板ID）
	*/
	virtual void addPage(const std::string boardId) = 0;
	
	/**
	* \brief 添加一个PPT所有页并生成白板
	* \param urls  一个PPT所有的url
	*/
	virtual void addFile(std::vector<std::wstring>& urls) = 0;
```  

	
## TICSDKCosConfig
COS参数配置类，主要是用于COS上传的参数配置，定义如下：

| 主要配置项             | 说明                |
| ------------------	|  ---------------    |
| setCosAppId     		|  cos APPID     |
| setCosBucket     		|  COS BUCKET    |
| setRegion				|  COS Region    |
| setSign   			|  COS 签名 |



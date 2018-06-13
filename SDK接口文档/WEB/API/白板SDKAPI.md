<a name="BoardSDK"></a>

## BoardSDK
**Kind**: global class  
**Version**: 2.0.0  

* [BoardSDK](#BoardSDK)
    * [new BoardSDK(options)](#new_BoardSDK_new)
    * _instance_
        * [.getBoardData()](#BoardSDK+getBoardData) ⇒ <code>Array</code>
        * [.addBoard()](#BoardSDK+addBoard)
        * [.deleteBoard(要删除的白板ID，为空表示删除当前页)](#BoardSDK+deleteBoard)
        * [.prevBoard()](#BoardSDK+prevBoard)
        * [.nextBoard()](#BoardSDK+nextBoard)
        * [.getBoardList()](#BoardSDK+getBoardList) ⇒ <code>Array</code>
        * [.getCurrentBoard()](#BoardSDK+getCurrentBoard) ⇒ <code>String</code>
        * [.switchBoard(boardId)](#BoardSDK+switchBoard)
        * [.setGlobalBackgroundColor(color)](#BoardSDK+setGlobalBackgroundColor)
        * [.setBackgroundColor(color)](#BoardSDK+setBackgroundColor)
        * [.setColor(color)](#BoardSDK+setColor)
        * [.setThin(thin)](#BoardSDK+setThin)
        * [.setType(type)](#BoardSDK+setType)
        * [.undo()](#BoardSDK+undo)
        * [.canUndo()](#BoardSDK+canUndo) ⇒ <code>Boolean</code>
        * [.redo()](#BoardSDK+redo)
        * [.canRedo()](#BoardSDK+canRedo) ⇒ <code>Boolean</code>
        * [.clear()](#BoardSDK+clear)
        * [.clearDraws()](#BoardSDK+clearDraws)
        * [.setBackgroundPic(url)](#BoardSDK+setBackgroundPic)
        * [.clearGlobalBgColor()](#BoardSDK+clearGlobalBgColor)
        * [.addFile(urls, title)](#BoardSDK+addFile) ⇒ <code>String</code>
        * [.deleteFile(fid)](#BoardSDK+deleteFile)
        * [.switchFile(fid)](#BoardSDK+switchFile)
        * [.getFile()](#BoardSDK+getFile) ⇒ <code>Array</code>
        * [.getBoardByFile(fid)](#BoardSDK+getBoardByFile) ⇒ <code>Array</code>
        * [.getBoardByFile(true)](#BoardSDK+getBoardByFile)
    * _static_
        * [.DRAW_TYPE](#BoardSDK.DRAW_TYPE) : <code>enum</code>

<a name="new_BoardSDK_new"></a>

### new BoardSDK(options)
BoardSDK 白板类


| Param | Type | Description |
| --- | --- | --- |
| options | <code>Object</code> | 构造函数参数 |

<a name="BoardSDK+getBoardData"></a>

### boardSDK.getBoardData() ⇒ <code>Array</code>
获取白板数据

**Kind**: instance method of [<code>BoardSDK</code>](#BoardSDK)  
**Returns**: <code>Array</code> - 返回白板数据  
<a name="BoardSDK+addBoard"></a>

### boardSDK.addBoard()
新增白板

**Kind**: instance method of [<code>BoardSDK</code>](#BoardSDK)  
<a name="BoardSDK+deleteBoard"></a>

### boardSDK.deleteBoard(要删除的白板ID，为空表示删除当前页)
删除白板

**Kind**: instance method of [<code>BoardSDK</code>](#BoardSDK)  

| Param | Type |
| --- | --- |
| 要删除的白板ID，为空表示删除当前页 | <code>String</code> | 

<a name="BoardSDK+prevBoard"></a>

### boardSDK.prevBoard()
向前翻页

**Kind**: instance method of [<code>BoardSDK</code>](#BoardSDK)  
<a name="BoardSDK+nextBoard"></a>

### boardSDK.nextBoard()
向后翻页

**Kind**: instance method of [<code>BoardSDK</code>](#BoardSDK)  
<a name="BoardSDK+getBoardList"></a>

### boardSDK.getBoardList() ⇒ <code>Array</code>
向后翻页

**Kind**: instance method of [<code>BoardSDK</code>](#BoardSDK)  
**Returns**: <code>Array</code> - 返回白板ID列表  
<a name="BoardSDK+getCurrentBoard"></a>

### boardSDK.getCurrentBoard() ⇒ <code>String</code>
获取当前白板ID

**Kind**: instance method of [<code>BoardSDK</code>](#BoardSDK)  
**Returns**: <code>String</code> - 返回当前白板ID  
<a name="BoardSDK+switchBoard"></a>

### boardSDK.switchBoard(boardId)
白板翻页

**Kind**: instance method of [<code>BoardSDK</code>](#BoardSDK)  

| Param | Type | Description |
| --- | --- | --- |
| boardId | <code>String</code> | 要展示的白板ID |

<a name="BoardSDK+setGlobalBackgroundColor"></a>

### boardSDK.setGlobalBackgroundColor(color)
设置全局颜色

**Kind**: instance method of [<code>BoardSDK</code>](#BoardSDK)  

| Param | Type | Description |
| --- | --- | --- |
| color | <code>String</code> | hex色值，如 #ff00ff |

<a name="BoardSDK+setBackgroundColor"></a>

### boardSDK.setBackgroundColor(color)
设置当前页颜色

**Kind**: instance method of [<code>BoardSDK</code>](#BoardSDK)  

| Param | Type | Description |
| --- | --- | --- |
| color | <code>String</code> | hex色值，如 #ff00ff |

<a name="BoardSDK+setColor"></a>

### boardSDK.setColor(color)
设置画笔颜色

**Kind**: instance method of [<code>BoardSDK</code>](#BoardSDK)  

| Param | Type | Description |
| --- | --- | --- |
| color | <code>string</code> | hex色值 #ff00ff |

<a name="BoardSDK+setThin"></a>

### boardSDK.setThin(thin)
设置线条的粗细

**Kind**: instance method of [<code>BoardSDK</code>](#BoardSDK)  

| Param | Type | Description |
| --- | --- | --- |
| thin | <code>Number</code> | 默认100 |

<a name="BoardSDK+setType"></a>

### boardSDK.setType(type)
修改涂鸦类型

**Kind**: instance method of [<code>BoardSDK</code>](#BoardSDK)  

| Param | Type | Description |
| --- | --- | --- |
| type | [<code>DRAW_TYPE</code>](#BoardSDK.DRAW_TYPE) | 如 BoardSDK.DRAW_TYPE.LINE |

<a name="BoardSDK+undo"></a>

### boardSDK.undo()
当前白板页撤销

**Kind**: instance method of [<code>BoardSDK</code>](#BoardSDK)  
<a name="BoardSDK+canUndo"></a>

### boardSDK.canUndo() ⇒ <code>Boolean</code>
判断当前白板页是否还能撤销

**Kind**: instance method of [<code>BoardSDK</code>](#BoardSDK)  
**Returns**: <code>Boolean</code> - true 还能撤销 false 不能再撤销了  
<a name="BoardSDK+redo"></a>

### boardSDK.redo()
当前白板页恢复

**Kind**: instance method of [<code>BoardSDK</code>](#BoardSDK)  
<a name="BoardSDK+canRedo"></a>

### boardSDK.canRedo() ⇒ <code>Boolean</code>
判断当前白板页是否还能恢复

**Kind**: instance method of [<code>BoardSDK</code>](#BoardSDK)  
**Returns**: <code>Boolean</code> - true 还能恢复 false 不能再恢复了  
<a name="BoardSDK+clear"></a>

### boardSDK.clear()
清空当前页涂鸦 + 背景色/图片

**Kind**: instance method of [<code>BoardSDK</code>](#BoardSDK)  
<a name="BoardSDK+clearDraws"></a>

### boardSDK.clearDraws()
清空当前页涂鸦(保留背景色/图片)

**Kind**: instance method of [<code>BoardSDK</code>](#BoardSDK)  
<a name="BoardSDK+setBackgroundPic"></a>

### boardSDK.setBackgroundPic(url)
设置当前页的背景图

**Kind**: instance method of [<code>BoardSDK</code>](#BoardSDK)  

| Param | Type | Description |
| --- | --- | --- |
| url | <code>String</code> | 图片的URL地址 |

<a name="BoardSDK+clearGlobalBgColor"></a>

### boardSDK.clearGlobalBgColor()
清除全局背景色

**Kind**: instance method of [<code>BoardSDK</code>](#BoardSDK)  
<a name="BoardSDK+addFile"></a>

### boardSDK.addFile(urls, title) ⇒ <code>String</code>
上传文件

**Kind**: instance method of [<code>BoardSDK</code>](#BoardSDK)  
**Returns**: <code>String</code> - 返回文件唯一ID  

| Param | Type | Description |
| --- | --- | --- |
| urls | <code>Array</code> | 文件转码后的图片urls |
| title | <code>String</code> | 文件名 |

<a name="BoardSDK+deleteFile"></a>

### boardSDK.deleteFile(fid)
删除文件

**Kind**: instance method of [<code>BoardSDK</code>](#BoardSDK)  

| Param | Type | Description |
| --- | --- | --- |
| fid | <code>String</code> | 文件唯一ID |

<a name="BoardSDK+switchFile"></a>

### boardSDK.switchFile(fid)
切换文件

**Kind**: instance method of [<code>BoardSDK</code>](#BoardSDK)  

| Param | Type | Description |
| --- | --- | --- |
| fid | <code>String</code> | 文件唯一ID |

<a name="BoardSDK+getFile"></a>

### boardSDK.getFile() ⇒ <code>Array</code>
获取白板中所有的文件

**Kind**: instance method of [<code>BoardSDK</code>](#BoardSDK)  
**Returns**: <code>Array</code> - 返回白板中所有的文件  
<a name="BoardSDK+getBoardByFile"></a>

### boardSDK.getBoardByFile(fid) ⇒ <code>Array</code>
根据文件获取该文件的所有白板

**Kind**: instance method of [<code>BoardSDK</code>](#BoardSDK)  
**Returns**: <code>Array</code> - 返回对应文件下的所有白板  

| Param | Type | Description |
| --- | --- | --- |
| fid | <code>String</code> | 文件ID, 为空时，表示默认的分组 |

<a name="BoardSDK+getBoardByFile"></a>

### boardSDK.getBoardByFile(true)
设置是否可以操作白板

**Kind**: instance method of [<code>BoardSDK</code>](#BoardSDK)  

| Param | Type | Description |
| --- | --- | --- |
| true | <code>Boolean</code> | 可以操作  false 不能操作 |

<a name="BoardSDK.DRAW_TYPE"></a>

### BoardSDK.DRAW_TYPE : <code>enum</code>
白板支持的涂鸦类型

**Kind**: static enum of [<code>BoardSDK</code>](#BoardSDK)  
**Read only**: true  
**Properties**

| Name | Type | Default | Description |
| --- | --- | --- | --- |
| LINE | <code>String</code> | <code>line</code> | 普通画笔 |
| ERASER | <code>String</code> | <code>eraser</code> | 橡皮擦 |
| RASER | <code>String</code> | <code>raser</code> | 激光笔 |
| POINTSELECT | <code>String</code> | <code>pointselect</code> | 点选 |
| SELECT | <code>String</code> | <code>select</code> | 框选 |
| GRAPH_LINE | <code>String</code> | <code>graph-line</code> | 直线 |
| GRAPH_CIRCLE | <code>String</code> | <code>graph-circle</code> | 空心圆 |
| GRAPH_RECT | <code>String</code> | <code>graph-rect</code> | 空心矩形 |
| GRAPH_OVAL | <code>String</code> | <code>graph-oval</code> | 空心椭圆 |
| GRAPH_CIRCLE_SOLID | <code>String</code> | <code>graph-circle-solid</code> | 实心圆 |
| GRAPH_RECT_SOLID | <code>String</code> | <code>graph-rect-solid</code> | 实心矩形 |
| GRAPH_OVAL_SOLID | <code>String</code> | <code>graph-oval-solid</code> | 实心椭圆 |


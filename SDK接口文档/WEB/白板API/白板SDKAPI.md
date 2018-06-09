<a name="Sketch"></a>

## Sketch
**Kind**: global class  

* [Sketch](#Sketch)
    * [new Sketch(options)](#new_Sketch_new)
    * _instance_
        * [.getBoardData()](#Sketch+getBoardData) ⇒ <code>Array</code>
        * [.addBoard()](#Sketch+addBoard)
        * [.deleteBoard(要删除的白板ID，为空表示删除当前页)](#Sketch+deleteBoard)
        * [.prevBoard()](#Sketch+prevBoard)
        * [.nextBoard()](#Sketch+nextBoard)
        * [.getBoardList()](#Sketch+getBoardList) ⇒ <code>Array</code>
        * [.getCurrentBoard()](#Sketch+getCurrentBoard) ⇒ <code>String</code>
        * [.switchBoard(boardId)](#Sketch+switchBoard)
        * [.setGlobalBackgroundColor(color)](#Sketch+setGlobalBackgroundColor)
        * [.setBackgroundColor(color)](#Sketch+setBackgroundColor)
        * [.setColor(color)](#Sketch+setColor)
        * [.setThin(thin)](#Sketch+setThin)
        * [.setType(type)](#Sketch+setType)
        * [.undo()](#Sketch+undo)
        * [.canUndo()](#Sketch+canUndo) ⇒ <code>Boolean</code>
        * [.redo()](#Sketch+redo)
        * [.canRedo()](#Sketch+canRedo) ⇒ <code>Boolean</code>
        * [.clear()](#Sketch+clear)
        * [.clearDraws()](#Sketch+clearDraws)
        * [.setBackgroundPic(url)](#Sketch+setBackgroundPic)
        * [.clearGlobalBgColor()](#Sketch+clearGlobalBgColor)
        * [.addFile(urls, title)](#Sketch+addFile) ⇒ <code>String</code>
        * [.deleteFile(fid)](#Sketch+deleteFile)
        * [.switchFile(fid)](#Sketch+switchFile)
        * [.getFile()](#Sketch+getFile) ⇒ <code>Array</code>
        * [.getBoardByFile(fid)](#Sketch+getBoardByFile) ⇒ <code>Array</code>
    * _static_
        * [.DRAW_TYPE](#Sketch.DRAW_TYPE) : <code>enum</code>

<a name="new_Sketch_new"></a>

### new Sketch(options)
Sketch 白板类


| Param | Type | Description |
| --- | --- | --- |
| options | <code>Object</code> | 构造函数参数 |

<a name="Sketch+getBoardData"></a>

### sketch.getBoardData() ⇒ <code>Array</code>
获取白板数据

**Kind**: instance method of [<code>Sketch</code>](#Sketch)  
**Returns**: <code>Array</code> - 返回白板数据  
<a name="Sketch+addBoard"></a>

### sketch.addBoard()
新增白板

**Kind**: instance method of [<code>Sketch</code>](#Sketch)  
<a name="Sketch+deleteBoard"></a>

### sketch.deleteBoard(要删除的白板ID，为空表示删除当前页)
删除白板

**Kind**: instance method of [<code>Sketch</code>](#Sketch)  

| Param | Type |
| --- | --- |
| 要删除的白板ID，为空表示删除当前页 | <code>String</code> | 

<a name="Sketch+prevBoard"></a>

### sketch.prevBoard()
向前翻页

**Kind**: instance method of [<code>Sketch</code>](#Sketch)  
<a name="Sketch+nextBoard"></a>

### sketch.nextBoard()
向后翻页

**Kind**: instance method of [<code>Sketch</code>](#Sketch)  
<a name="Sketch+getBoardList"></a>

### sketch.getBoardList() ⇒ <code>Array</code>
向后翻页

**Kind**: instance method of [<code>Sketch</code>](#Sketch)  
**Returns**: <code>Array</code> - 返回白板ID列表  
<a name="Sketch+getCurrentBoard"></a>

### sketch.getCurrentBoard() ⇒ <code>String</code>
获取当前白板ID

**Kind**: instance method of [<code>Sketch</code>](#Sketch)  
**Returns**: <code>String</code> - 返回当前白板ID  
<a name="Sketch+switchBoard"></a>

### sketch.switchBoard(boardId)
白板翻页

**Kind**: instance method of [<code>Sketch</code>](#Sketch)  

| Param | Type | Description |
| --- | --- | --- |
| boardId | <code>String</code> | 要展示的白板ID |

<a name="Sketch+setGlobalBackgroundColor"></a>

### sketch.setGlobalBackgroundColor(color)
设置全局颜色

**Kind**: instance method of [<code>Sketch</code>](#Sketch)  

| Param | Type | Description |
| --- | --- | --- |
| color | <code>String</code> | hex色值，如 #ff00ff |

<a name="Sketch+setBackgroundColor"></a>

### sketch.setBackgroundColor(color)
设置当前页颜色

**Kind**: instance method of [<code>Sketch</code>](#Sketch)  

| Param | Type | Description |
| --- | --- | --- |
| color | <code>String</code> | hex色值，如 #ff00ff |

<a name="Sketch+setColor"></a>

### sketch.setColor(color)
设置画笔颜色

**Kind**: instance method of [<code>Sketch</code>](#Sketch)  

| Param | Type | Description |
| --- | --- | --- |
| color | <code>string</code> | hex色值 #ff00ff |

<a name="Sketch+setThin"></a>

### sketch.setThin(thin)
设置线条的粗细

**Kind**: instance method of [<code>Sketch</code>](#Sketch)  

| Param | Type | Description |
| --- | --- | --- |
| thin | <code>Number</code> | 默认100 |

<a name="Sketch+setType"></a>

### sketch.setType(type)
修改涂鸦类型

**Kind**: instance method of [<code>Sketch</code>](#Sketch)  

| Param | Type | Description |
| --- | --- | --- |
| type | [<code>DRAW_TYPE</code>](#Sketch.DRAW_TYPE) | 如 Sketch.DRAW_TYPE.LINE |

<a name="Sketch+undo"></a>

### sketch.undo()
当前白板页撤销

**Kind**: instance method of [<code>Sketch</code>](#Sketch)  
<a name="Sketch+canUndo"></a>

### sketch.canUndo() ⇒ <code>Boolean</code>
判断当前白板页是否还能撤销

**Kind**: instance method of [<code>Sketch</code>](#Sketch)  
**Returns**: <code>Boolean</code> - true 还能撤销 false 不能再撤销了  
<a name="Sketch+redo"></a>

### sketch.redo()
当前白板页恢复

**Kind**: instance method of [<code>Sketch</code>](#Sketch)  
<a name="Sketch+canRedo"></a>

### sketch.canRedo() ⇒ <code>Boolean</code>
判断当前白板页是否还能恢复

**Kind**: instance method of [<code>Sketch</code>](#Sketch)  
**Returns**: <code>Boolean</code> - true 还能恢复 false 不能再恢复了  
<a name="Sketch+clear"></a>

### sketch.clear()
清空当前页涂鸦 + 背景色/图片

**Kind**: instance method of [<code>Sketch</code>](#Sketch)  
<a name="Sketch+clearDraws"></a>

### sketch.clearDraws()
清空当前页涂鸦(保留背景色/图片)

**Kind**: instance method of [<code>Sketch</code>](#Sketch)  
<a name="Sketch+setBackgroundPic"></a>

### sketch.setBackgroundPic(url)
设置当前页的背景图

**Kind**: instance method of [<code>Sketch</code>](#Sketch)  

| Param | Type | Description |
| --- | --- | --- |
| url | <code>String</code> | 图片的URL地址 |

<a name="Sketch+clearGlobalBgColor"></a>

### sketch.clearGlobalBgColor()
清除全局背景色

**Kind**: instance method of [<code>Sketch</code>](#Sketch)  
<a name="Sketch+addFile"></a>

### sketch.addFile(urls, title) ⇒ <code>String</code>
上传文件

**Kind**: instance method of [<code>Sketch</code>](#Sketch)  
**Returns**: <code>String</code> - 返回文件唯一ID  

| Param | Type | Description |
| --- | --- | --- |
| urls | <code>Array</code> | 文件转码后的图片urls |
| title | <code>String</code> | 文件名 |

<a name="Sketch+deleteFile"></a>

### sketch.deleteFile(fid)
删除文件

**Kind**: instance method of [<code>Sketch</code>](#Sketch)  

| Param | Type | Description |
| --- | --- | --- |
| fid | <code>String</code> | 文件唯一ID |

<a name="Sketch+switchFile"></a>

### sketch.switchFile(fid)
切换文件

**Kind**: instance method of [<code>Sketch</code>](#Sketch)  

| Param | Type | Description |
| --- | --- | --- |
| fid | <code>String</code> | 文件唯一ID |

<a name="Sketch+getFile"></a>

### sketch.getFile() ⇒ <code>Array</code>
获取白板中所有的文件

**Kind**: instance method of [<code>Sketch</code>](#Sketch)  
**Returns**: <code>Array</code> - 返回白板中所有的文件  
<a name="Sketch+getBoardByFile"></a>

### sketch.getBoardByFile(fid) ⇒ <code>Array</code>
根据文件获取该文件的所有白板

**Kind**: instance method of [<code>Sketch</code>](#Sketch)  
**Returns**: <code>Array</code> - 返回对应文件下的所有白板  

| Param | Type | Description |
| --- | --- | --- |
| fid | <code>String</code> | 文件ID, 为空时，表示默认的分组 |

<a name="Sketch.DRAW_TYPE"></a>

### Sketch.DRAW_TYPE : <code>enum</code>
白板支持的涂鸦类型

**Kind**: static enum of [<code>Sketch</code>](#Sketch)  
**Read only**: true  
**Properties**

| Name | Type | Default | Description |
| --- | --- | --- | --- |
| LINE | <code>String</code> | <code>line</code> | 普通画笔 |
| ERASER | <code>String</code> | <code>eraser</code> | 橡皮擦 |
| RASER | <code>String</code> | <code>raser</code> | 激光笔 |
| POINTSELECT | <code>String</code> | <code>pointselect</code> | 点选 |
| SELECT | <code>String</code> | <code>select</code> | 框选 |
| "GRAPH-LINE" | <code>String</code> | <code>graph-line</code> | 直线 |
| "GRAPH-CIRCLE" | <code>String</code> | <code>graph-circle</code> | 空心圆 |
| "GRAPH-RECT" | <code>String</code> | <code>graph-rect</code> | 空心矩形 |
| "GRAPH-OVAL" | <code>String</code> | <code>graph-oval</code> | 空心椭圆 |
| "GRAPH-CIRCLE-SOLID" | <code>String</code> | <code>graph-circle-solid</code> | 实心圆 |
| "GRAPH-RECT-SOLID" | <code>String</code> | <code>graph-rect-solid</code> | 实心矩形 |
| "GRAPH-OVAL-SOLID" | <code>String</code> | <code>graph-oval-solid</code> | 实心椭圆 |


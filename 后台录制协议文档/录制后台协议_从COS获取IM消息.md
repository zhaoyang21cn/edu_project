
### 从cos获取IM消息

    接口背景：
    IM后台策略：当IM群组中消息超过1w时，会从前往后依次丢消息；
    为了获取所有消息，录制后台做了消息旁路，将所有消息另存一份，并提供此接口，供外部调用

* 1、只有IM管理员才有权限调用
* 2、请求URL`https://console.tim.qq.com/v4/ilvb_edu/record?sdkappid=140001533&identifier=admin&usersig=adminsigstr&contenttype=json`
* 3、要使用消息转存的先决条件，客户端在开课时需要上报群组ID到录制后台, 这样录制后台才会监听这个群组的IM消息, 客户后台发起离线录制时，录制后台会从队列中删除这个群组ID,如果没有发起离线录制，那么这个群组在队列中最多存在24小时，24小时后会被自动删除
* 4、cos转存的原理：客户端上报群组ID到录制后台，录制后台将群组ID加入到监控队列中，每隔10min检查一次，发现当前群最大seq大于1W,则立马启动转存逻辑
* 5、转存逻辑：新起线程，从第一条消息开始拉取，每60KB消息转存为1个文件(每个文件<=60KB)，文件命名从0开始，每次递增；调用本接口时，请求中的index, 就是文件名对应的索引。
* 6、调用本接口前，客户后台必须自己先判断群组消息数是否大于1W, 如果是小于1W的群组，调用这个接口，是不可能拉到消息的(判断方法：调用IM restapi ,获取群组中最近的一条消息，比较消息seq是否大于1w)
* 7、因为每次分片是达到60KB后才会分片，如果群消息的最后10min，消息数不足60KB,会导致最后10min的消息没有转存到COS中, 客户后台可以根据从COS这里拿到的最后一条消息的seq, 再去IM后台获取最后10min的消息； 如果发起过离线录制，则没有这个问题，因为在发起离线录制的时候，后台会单独跑一个逻辑，将剩余的零碎消息全部转存到COS(即使不足60KB)

参数详解

| 参数 | 类型 | 描述 |
| -- | -- | -- |
| cmd | string | 主命令字，本接口固定为`open_record_svc`|
| sub_cmd | string | 子命令字，本接口固定为`get_im_msg_from_cos`|
| groupid | string | IM群组ID|
| index |int | IM消息的文件索引，第一次拉取时填0， 轮训拉取，每次+1，直到is_finish=true,如果此值小于0，则会自动修正为0|
| is_finish | bool | 是否拉取完所有消息 true-拉取完/false-未拉完 |
| msg_list |Array | IM消息数组，数组中的对象是IM消息对象，IM消息对象参考腾讯云官网`云通信`|

request 
```
{
    "cmd":"open_record_svc",
    "sub_cmd":"get_im_msg_from_cos",
    "groupid":"1234",
    "index":0
}
```

response

```
{
    "error_code":0,
    "error_msg":"",
    "is_finish":true,
    "msg_list":[
        IMMsgObj1,
        IMMsgObj2,
        IMMsgObj3
    ]
}
```

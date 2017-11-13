Pushd Android SDK
=================



# sdk提供的功能：
* 发送文字消息
* 发送语音、图片、视频消息
* 接收好友、群聊的消息推送  


## sdk目前尚不具备的功能
* 网络断开恢复后，不能立即与im服务器重连（目前sdk没有实时检测网络恢复操作）。需要开发者自己完成此情况下的重连机制  
   1、目前sdk ImAssistent中提供了reConnectImServer方法，断网后可调用此方法重连  
   2、断网恢复后，调用此方法不能保证一次即可重连成功（因为网络的通畅），最好放到一个for循环中调用2~3次，直到返回true  

* 接收到的消息类型需开发者区分  
    1、目前sdk接收到的服务器推送的消息不区分类型  
    2、对于消息属于图片、语音、视频、文字哪一类，需要开发者根据消息的开头标签来区分  
    3、各标签[video]、[voice]、[pic]，分别是视频、语音、图片，没有标签则为文本,对应的音视频文件地址在标签后面。如：[pic]http://git.oschina.net/logo.svg?201702241900  




## sdk初始化

* 使用PushdManager类初始化，得到ImAssistant对象，此对象使用单例模式，全局唯一
```java

    1、 在Application的onCreatef方法中调用
    PushdManager.init()

    2、目前网络状态改变需要app端的支持，需要在网络改变方法初调用：
    INetWorkStatChanCallBack iNetWorkStatChanCallBack = PushdManager.getNetWorkStatChanCallBack()
    // 网络断开时调用
    iNetWorkStatChanCallBack.disConnectedCallBack();
    // 网络连接恢复时调用
    iNetWorkStatChanCallBack.connectedCallBack();

    3、认证用户
    ImAssistant imAssistant = PushdManager.getImAssistant();
    try {
        PushdManager.setOrUpdateUserId(token, userId);
    } catch (TokenException e) {
        // token 失效
    } catch (NetworkException e) {
        // 网络异常
    }

    Note: 这三部之间没有依赖关系，所以不用考虑 是不是第一步还没有完成时不能开始第三步的问题。


```


## 自定义Excetion介绍

* TokenException
    * 访问Token错误

* ConnectExcetion
    *  与im服务器建立连接异常

* NetworkException
    *  网络异常：网速异常缓慢、网络断开


## ImAssitant中各方法说明
  
  
``` java
@Deprecated 过时方法
//重连im服务器，当网络断开又恢复后，调用此方法。
boolean reConnectImServer()  
  
  
  
//设置接收服务器推送消息回调函数  
void setIProcessor(IProcessor iProcessor)  
  
  
  
  
// 发送文字消息  
//msg:          消息内容  
//channelId：   聊天室id  
//iSendResult： 回调函数 
void sendText(String msg, String channelId, ISendResult iSendResult)  
 
    
    
    
    
//发送图片消息  
void sendPicture(String cookie, String channelId, File picture, ISendResult iSendResult)  
//cookie：     web端的cookie字符串  
//channelId：  聊天室id  
//picture：    图片文件  
//iSendResult：回掉函数  
  
  
  
  
  
//发送语音消息  
void sendSound(String cookie, String channelId, File voice, ISendResult iSendResult)  
//cookie：     web端的cookie字符串  
//channelId：  聊天室id  
//voice：      语音文件  
//iSendResult：回调函数  
  
  
  
  
//发送视频消息  
void sendVideo(String cookie, String channelId, File video, ISendResult iSendResult)  
//cookie：     web端的cookie字符串  
//channelId：  聊天室id  
//video：      视频文件  
//iSendResult：回调函数  
  
  
  
  
//获取某个聊天室的历史消息  
void fetchHistoryMsg(String channelId, Long ts, ISendResult iSendResult)  
//channelId:  聊天室id  
//ts:         时间戳  
//iSendResult：回调函数    
  
  
  
  
//重发文字消息  
void reSendText(long msgId, String msg, String channelId, ISendResult iSendResult)  
//msgId:       上次发送的消息id：从iSendResult中获取  
//msg          消息内容  
//channelId：  聊天室id  
//video：      视频文件  
//iSendResult：回调函数    
  
  
  
  
//重发图片消息  
void reSendPicture(long msgId, String cookie, String channelId, File picture, ISendResult iSendResult)  
//同上  
  
  
  
//重发语音消息  
void reSendSound(long msgId, String cookie, String channelId, File voice, ISendResult iSendResult)  
//同上  
  
  
  
  
//重发视频消息  
void reSendVideo(long msgId, String cookie, String channelId, File video, ISendResult iSendResult)  
//同上  

 
```

## 两个关键回调函数
* 1、ISendResult 接口
``` java
        public interface ISendResult {

            void success(String msg, SendResultMsg data);
            // msg: 发送成功返回消息

            void failed(String msg, SendResultMsg data);
            // msg: 发送失败返回消息

        }




```

* 2、SendResultMsg类
```java

    // 下面是类中暴露出来的三个方法


    // 获取消息的id
    long getMsgId()

    // 获取发送结果详情
    String getMsg()  

    // 获取结果状态码
    int getStatus()

    // 返回sdk内部封装的消息对象（一般不需要）
    SendMsg getSdkSendMsg()


```

* 3、发送结果个状态码介绍

```java

    // 需要开发者处理的状态码：success、timeOut、tokenInvalid

    public static class ResultStatus {

        // 发送成功
        public final static int success = 200;

        // 开发者可忽略此错误
        public final static int failed = 400;

        // 服务器响应超时
        public final static int timeOut = 500;

        // 访问token失效，此时需要开发者重新获取token，并调用imAssistant.updateToken()
        public final static int tokenInvalid = 600;
    }


```

* 2、IProcessor 接口
```java

// 全局接收im服务器消息推送，回调函数

public interface IProcessor {

    void procPushMsg(PushMsg pushMsg);

}

```

* 3、 PushMsg类
``` java
public class PushMsg {

    private int msgType;
    private String channelId;
    private String content;
    private String userId;
    private long msgId;
    private long ts;

    public PushMsg(int msgType, String channelId, String userId, long msgId, String content, long ts){
        this.msgType = msgType;
        this.channelId = channelId;
        this.userId = userId;
        this.msgId = msgId;
        this.content = content;
        this.ts = ts;
    }

    // 消息类型
    // 目前只有一种类型，（音视频文字图片消息看作是一种消息类型，以后随着业务的扩展可能会添加）
    public int getMsgType() {
        return msgType;
    }

    // 聊天室id
    public String getChannelId() {
        return channelId;
    }

    // 消息内容
    public String getContent() {
        return content;
    }

    // 发送者id
    public String getUserId() {
        return userId;
    }

    // 消息id
    public long getMsgId() {
        return msgId;
    }

    // 消息发送时间戳
    public Long getTs() {
        return ts;
    }
}
```

## 实时语音视频相关接口

### 一、说明
* 同一个群聊中有且只有一个用户发起有且只有一种的实时通讯活动。
* 同一用户可以在不同群聊中同时发起实时通讯活动。
* 当实时通讯申请后，只要实时通讯活动还存在，那么在一个群中的所有用户，在每次登陆的时候，都会收到apply推送通知。此通知会在sdk每次与服务器重连时被推送。所以即使用户没有退出app，也可能会收到重复的推送通知。
* 当收到dismiss、refuse推送时，sdk会自动向服务器发送quit命令退出实时通讯，无需开发者调用quit接口。
* 一对一的实时通讯涉及到的接口为：applyOneToOneXXXXXX、refuseXXXX、acceptXXXX、dismissXXXX
* 群聊实时通讯涉及到的接口为： applyMulXXXXX、joinXXXXXX、quitXXXXXX、dismissXXXXX


### 二、接口详情
``` java


    /**
     *  申请一对一语音聊天
     * @param channelId 当前所在的channelId（以下雷同）
     * @param iSendResult 成功后会返回一个新的channelId，之后通过此新的channelId通信（以下雷同）
     */
    public void applyOneToOneSoundChat(String channelId, ISendResult iSendResult)


    /**
     * 申请语音群聊
     * @param channelId
     * @param iSendResult
     */
    public void applyMulSoundChat(String channelId, ISendResult iSendResult)


    /**
     * 申请一对一视频聊天
     * @param channelId
     * @param iSendResult
     */
    public void applyOneToOneVideoChat(String channelId, ISendResult iSendResult)


    /**
     * 申请视频群聊
     * @param channelId
     * @param iSendResult
     */
    public void applyMulVideoChat(String channelId, ISendResult iSendResult)


    /**
     * 拒绝一对一语音或视频聊天
     * @param channleId
     * @param iSendResult
     */
    public void refuseVideoOrPhoneChat(String channleId, ISendResult iSendResult)


    /**
     * 解散语音或视频群聊
     * @param channelID
     * @param iSendResult
     */
    public void dismissVideoOrPhoneChat(String channelID, ISendResult iSendResult)


    /**
     * 加入语音或视频群聊
     * @param channelId
     * @param iSendResult
     */
    public void joinVideoOrPhoneChat(String channelId, ISendResult iSendResult)


    /**
     * 退出语音或视频群聊
     * @param channelId
     * @param iSendResult
     */
    public void quitVideoOrPhoneChat(String channelId, ISendResult iSendResult)


    /**
     * 获取语音或视频群聊实时信息
     * @param channelId
     * @param iSendResult
     */
    public void fetchVideoOrPhoneChatRealTimeInfo(String channelId, ISendResult iSendResult)


    /**
     * 设置服务器推送指令接收回调函数
     * @param iInstructions
     */
    public void setIInstructions(IInstructions iInstructions)


    /**
    * 所有与服务器推送命令相关的类
    * 
    **/
    public class InstructMsg

    /**
    * 内部类Type说明了所有的服务器命令类型
    */
    public class InstructMsg {
        public static class Type{
            public static int FRAME_CHAT = 1;// 实时语音视频相关命令
        }
    }

    /**
    * 方法getInstruction，获取具体的命令类，通过上转形转为具体的命令对象
    */
    public class InstructMsg {
        public Object getInstruction()
    }


    /**
    * 此类是实时语音视频命令的具体类，两个内部类说明了此命令中的具体子命令，及聊天的类型
    */
    public class InstructFrameMsg {
        public static class Instructions{
            public static final int FRAME_CHAT_APPLY = 1;
            public static final int FRAME_CHAT_DISMISS = 2;
            public static final int FRAME_CHAT_JOIN = 3;
            public static final int FRAME_CHAT_OUT = 4;
            public static final int FRAME_CHAT_REFUSE = 5;
            public static final int FRAME_CHAT_ACCEPT = 6;
        }

        public static class FrameChatType {
            public static final int TYPE_ONE_TO_ONE_SOUND  = 1;
            public static final int TYPE_MUL_SOUND  = 2;
            public static final int TYPE_ONE_TO_ONE_VIDEO  = 3;
            public static final int TYPE_MUL_VIDEO  = 4;
        }
    }

```
### 三、状态码介绍     
* 10001： 此群聊中已经由其他人发起了一个实时通讯活动，同一个群聊中只能发起有且只有一个有且只有一种实时通讯 applyXXX 会遇到
* 10002： 此群聊中你已经发起了一个实时通讯活动，同一个群聊中只能发起有且只有一个有且只有一种实时通讯  applyXXX 会遇到
* 10003： 此实时通话已经结束，joinXXXX、acceptXXXX 会遇到

##

## 全局状态码
* 200 成功
* 500 服务器出错
* 300 timeout 访问超时
* 110 token失效

## 群通知类型


```java

    // 这些通知在 IProcessor 的 void procChatRoomNotification(String data); 中处理
    // data 为json格式数据

    // 某人加入群聊
	public static final int SOME_ONE_JOIN_CHAT_ROOM = 4;
    {
        "type": 4,
        "channel": "roomId0",
        "msg": "userId0 name0 name1,name2,name3 userId1,userId2,userId3"  // userId0 加入了群聊roomId0
        /**
         userId0 userId1 userId2 userId3 是群中的所有用户id
        **/
    }

	// 某人退出群聊
	public static final int SOME_ONE_QUIT_CHAT_ROOM = 5;
    {
        "type": 5,
        "channel": "roomId0",
        "msg": "userId0 name0"  // 用户userId0退出了群聊roomId0
    }

	// 某人被踢出群聊
	public static final int SOME_ONE_EXPELLED_FROM_CHAT_ROOM = 6;
    {
        "type": 6,
        "channel": "roomId0",
        "msg": "userId0,userId1,userId2,userId3 name0,name1,name2,name3"       // 用户userId1,userId2,userId3被用户userId0踢出了群聊
    }

	// 某人修改了群名称
	public static final int SOME_ONE_MODIFY_NAME_OF_CHAT_ROOM = 7;
    {
        "type": 7,
        "channel": "roomId0",
        "msg": "userId0,name0,roomNewName"  // 用户userId0将群聊roomId0的名字改为roomNewName
    }

	// 某人被邀请加入群聊
	public static final int SOME_ONE_BE_INVITED_OT_CHAT_ROOM = 8;
    {
        "type": 8,
        "channel": "roomId0",
        "msg": "userId0,userId1,userId2 name0,name1,name2 name3,name4,name5,name6,name7 userId3,userId4,userId5,userId6,userId7"  // 用户userId0邀请userId1,userId2进去群聊roomId0
        // userId0,userId1,userId2,userId3,userId4,userId5,userId6,userId7 是群中的所有用户
    }

    // 面对面群中某人第一个加入了群聊
	public static final int FACE_TO_FACE_SOME_ONE_JOIN_CHAT_ROOM = 9;
    {
        "type": 9,
        "channel": "roomId0",
        "msg": "userId0,name0,26453"  // userId0第一个加入了面对面群聊roomId0

    }

```
	














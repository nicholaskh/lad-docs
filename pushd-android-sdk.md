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
    3、各标签[video]、[voice]、[pic]，分别是视频、语音、图片，没有标签则为文本,对应的音视频文件地址在标签后main。如：[pic]http://git.oschina.net/logo.svg?201702241900  




## sdk初始化

* 使用PushdManager类初始化，得到ImAssistant对象，此对象使用单例模式，全局唯一
```java
 ImAssistant imAssistant = PushdManager.init(host, port, token, userId);


Note: 如果返回的imAssistant为null，则初始化失败。开发者只需要关心网络是否存在情况


```



## ImAssitant中各方法说明
  
  
``` java
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
* 2、IProcessor 接口
```java

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















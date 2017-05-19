Pushd Android SDK
=================

#安卓sdk使用说明


##初始化

* .使用PushdManager类初始化，得到ImAssistant对象，此对象使用单例模式，全局唯一
* .ImAssistant imAssistant = PushdManager.init(host, 2222, token, userId);
* .参数说明：服务器地址，服务器端口号，用户登录token，用户id
* .如果得到的ImAssistant对象为null，则初始化失败。出现这种情况时，sdk使用者只需考虑手机是否没有网络


##ImAssitant方法说明
  
  
  
//重连im服务器，当网络断开又恢复后，调用此方法。
boolean reConnectImServer()  
  
  
  
//设置全局接受服务器推送消息回掉函数  
void setIProcessor(IProcessor iProcessor)  
  
  
  
  
// 发送文字消息  
void sendText(String msg, String channelId, ISendResult iSendResult)  
msg:         消息内容  
channelId：  聊天室id  
iSendResult：回掉函数  
    
    
    
    
//发送图片消息  
void sendPicture(String cookie, String channelId, File picture, ISendResult iSendResult)  
cookie：     web端的cookie字符串  
channelId：  聊天室id  
picture：    图片文件  
iSendResult：回掉函数  
  
  
  
  
  
//发送语音消息  
void sendSound(String cookie, String channelId, File voice, ISendResult iSendResult)  
cookie：     web端的cookie字符串  
channelId：  聊天室id  
voice：      语音文件  
iSendResult：回掉函数  
  
  
  
  
//发送视频消息  
void sendVideo(String cookie, String channelId, File video, ISendResult iSendResult)  
cookie：     web端的cookie字符串  
channelId：  聊天室id  
video：      视频文件  
iSendResult：回掉函数  
  
  
  
  
//获取某个聊天室的历史消息  
void fetchHistoryMsg(String channelId, Long ts, ISendResult iSendResult)  
channelId:  聊天室id  
ts:         时间戳  
iSendResult：回掉函数  
  
  
  
  
//重发文字消息  
void reSendText(long msgId, String msg, String channelId, ISendResult iSendResult)  
msgId:       上次发送的消息id：从iSendResult中获取  
msg          消息内容  
channelId：  聊天室id  
video：      视频文件  
iSendResult：回掉函数  
  
  
  
  
//重发图片消息  
void reSendPicture(long msgId, String cookie, String channelId, File picture, ISendResult iSendResult)  
同上  
  
  
  
//重发语音消息  
void reSendSound(long msgId, String cookie, String channelId, File voice, ISendResult iSendResult)  
同上  
  
  
  
  
//重发视频消息  
void reSendVideo(long msgId, String cookie, String channelId, File video, ISendResult iSendResult)  
同上  
  
  















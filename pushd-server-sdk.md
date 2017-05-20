
# 服务端tool使用说明


## 名词解释：

* 服务端token： 服务端调im服务的大部分接口时需要token，im服务器根据此token来验证服务端是否合法
* 服务端appkey： 服务端颁发的认证key，服务端需要使用appkey来获取服务端token
* 手机端token:： 手机端连接im使用的token

* im提供的不需要服务端token，即可调用的ImAssistant中的方法:  

    * getToken()
    * authServer()
    * getAppKey()


## ImAssitant方法介绍  

    1、
    // 初始化ImAssistant  
    ImAssistant init(String host, int port)  

    2、
    //设置读超时时间
    // time: 毫秒
    boolean setReadTime(int time)  

    3、
    // 创建聊天室 
    // channelName: 聊天室名称
    // channelId：  聊天室id
    // uuids：      在此聊天室的用户id
    Message subscribe(String channelName, String channelId, String... uuids)

    4、
    // 获取服务端使用的appkey
    Message getAppKey()

    5、
    // 将获取到的服务端token保存到ImAssitant对象中
    // token: 下次访问服务器时使用的token，需要调用此方法存储到ImAssisten对象中。调用其他方法时，将会附带此值访问
    void setServerToken(String token)

    6、
    // 认证服务器，并获取服务端token
    // appkey： 分发给服务器的key
    // 返回值： 从返回的Message对象中获取服务端token
    Message authServer(String appKey)



    7、
    // 关闭与im服务器的连接
    void close()









# 服务端tool使用说明


## 名词解释：

* 服务端token： 服务端调im服务的大部分接口时需要token，im服务器根据此token来验证服务端是否合法
* 服务端appkey： 服务端颁发的认证key，服务端需要使用appkey来获取服务端token
* 手机端token:： 手机端连接im使用的token

* im提供的不需要服务端token，即可调用的ImAssistant中的方法:  

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
    // 获取手机端连接im服务器使用的token
    Message getToken()


    8、
    // 关闭与im服务器的连接
    void close()


## Message状态码介绍


    // Note：开发者需要处理：success、timeOut、tokenError三种状态

    public static class Status {

        // 访问接口成功
        public static final int success = 1;

        // 等待服务器响应超时（sdk默认等待5秒，开发者可以通过setReadTime方法设置）
        public static final int timeOut = 2;

        // 接口调用失败，开发者可忽略此错误，此错误需要sdk制作者考虑。sdk制作者应保证不出现此错误
        public static final int failed = 3;

        // 服务端访问token失效，此时需要开发者重新获取服务端token
        public static final int tokenError = 4;
    }



## 使用场景用例， (每个场景都使用短连接形式)

* **创建聊天室**
```java
    // subscribe()接口具有幂等性，多次重复调用同样参数不影响结果

    //一定用到的方法
    init()
    setServerToken()
    subscribe()
    close()

    //可能涉及到的方法
    authServer()  // token过期时需要使用此方法重新获取token
    setReadTime() //
```

* **获取手机端访问token**
```java
   // 一定用到的方法
    init()
    setServerToken()
    getToken()
    close()

    //可能涉及到的方法
    authServer()  // token过期时需要使用此方法重新获取token
    setReadTime() //
```

* **获取服务端访问token**
```java
    //一定用到的方法
    init()
    authServer()
    close()

    //可能涉及到的方法
    setReadTime() //


```

## 特殊情况:
    调用ImAssistant各接口时，如果返回的Message对象为null。这种情况是读错误引起的。
    造成此错误的原因是：与im服务器的连接异常断开。如果开发者所处环境连接容易被安全软件或其他误伤，需要考虑此情况。
    出现此情况时，需要重新连接im服务器。







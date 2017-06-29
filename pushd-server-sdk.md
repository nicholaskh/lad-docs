
# 服务端tool使用说明


## 名词解释：

* api server的term： api server调 im server的大部分接口时需要term，im server根据api server 提供的term来验证api server的合法性
* api server的appkey： im server颁发的认证key，api server需要使用appkey来获取term
* 手机端token:： 手机端连接im server使用的token

* server sdk提供的不需要term，即可调用的im server中的接口:  

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
    // 获取api server使用的appkey
    Message getAppKey()

    5、
    // 将获取到的term保存到ImAssitant对象中
    // term: 下次访问im server时使用的erm，需要调用此方法存储到ImAssisten对象中。调用其他方法时，将会附带此值访问
    void setServerTerm(String term)

    6、
    // 认证，并获取term
    // appkey： 分发给api server的key
    // 返回值： 从返回的Message对象中获取term。String term = message.getMsg()
    Message authServer(String appKey)


    7、
    // 获取手机端连接im server使用的token
    Message getToken()


    8、
    // 关闭与im server的连接
    void close()


## Message状态码介绍


    // Note：开发者需要处理：success、timeOut、termError三种状态

    public static class Status {

        // 访问接口成功
        public static final int success = 1;

        // 等待im server响应超时（sdk默认等待5秒，开发者可以通过setReadTime方法设置）
        public static final int timeOut = 2;

        // 接口调用失败，开发者可忽略此错误，此错误需要sdk制作者考虑。sdk制作者应保证不出现此错误
        public static final int failed = 3;

        // api server访问的term失效，此时需要开发者重新获取term
        public static final int termError = 4;
    }



## 使用场景用例， (每个场景都使用短连接形式)

* **注册用户**
```java

    // 用户已存在时，创建失败

    //一定用到的方法
    init()
    setServerTerm()
    createUser("userid")
    close()

    //可能涉及到的方法
    authServer()  // term过期时需要使用此方法重新获取term
    setReadTime() //
```

* **创建聊天室**
```java
    // subscribe()接口具有幂等性，多次重复调用同样参数不影响结果

    //一定用到的方法
    init()
    setServerTerm()
    subscribe("channelName","channelId","uuid1","uuid2","uuid3")
    close()

    //可能涉及到的方法
    authServer()  // term过期时需要使用此方法重新获取term
    setReadTime() //
```

* **加入群聊**
```java
// subscribe()接口具有幂等性，多次重复调用同样参数不影响结果

    //一定用到的方法
    init()
    setServerTerm()
    // 第一个channleName一定要为""
    subscribe("","channelId","uuid10") 或 addUserToChatRoom("roomId", "uuid1", "uuid2")
    close()

    //可能涉及到的方法
    authServer()  // term过期时需要使用此方法重新获取term
    setReadTime() //
```

* **退出群聊**
```java
// unSubscribe()接口具有幂等性，多次重复调用同样参数不影响结果

    //一定用到的方法
    init()
    setServerTerm()
    // 用户 uuid1 uuid2 退出群 channelId
    unSubscribe("channelId","uuid1","uuid2”)
    close()

    //可能涉及到的方法
    authServer()  // term过期时需要使用此方法重新获取term
    setReadTime() //
```


* **解除好友关系 或 解散群聊**
```java
//一定用到的方法
    init()
    setServerTerm()
    // 群聊id ：channelID
    disolveRoom("channelId")
    close()

    //可能涉及到的方法
    authServer()  // term过期时需要使用此方法重新获取term
    setReadTime() //
```

* **获取手机端访问token**
```java
   // 一定用到的方法
    init()
    setServerTerm()
    getToken()
    close()

    //可能涉及到的方法
    authServer()  // term过期时需要使用此方法重新获取term
    setReadTime() //
```

* **获取服务端访问term**
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
    造成此错误的原因是：与im server的连接异常断开。如果开发者所处环境连接容易被安全软件或其他误伤，需要考虑此情况。
    出现此情况时，需要重新连接im server。







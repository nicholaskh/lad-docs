User System APIs
================

###	Common
*   cookie
    -   sessionId: session相关ID
*	return: in json
	-   ret: 0成功，非0为error code；首位为模块代码，后面为错误代码，两者组合。
*   错误码定义
	-   10001, "用户名错误"
	-   10002, "密码错误"
	-   10003, "手机号码重复"
	-   10004, "手机号码错误"
	-   10005, "未登录"
	-   10006, "用户名ID错误"
	-   10007, "手机号码为空"

	-   20001, "用户名错误"
	-   20002, "性别错误"
	-   20003, "个性签名错误"
	-   20004, "生日错误"
	-   20005, "手机号码错误"
	-   20006, "用户ID错误"

	-   30001, "密码不一致"
	-   30002, "验证码错误"

	-   40001, "访问者ID错误"
	-   40002, "首页为空"
	-   40003, "消息来源错误"
	-   40004, "消息内容错误"
	-   40005, "重复点赞"

	-   50001, "反馈为空"
	
	-   60001, "聊天室name为空"
	-   60002, "已经加入该聊天室"
	-   60003, "聊天室为空"
	-   60004, "已经加入该聊天室"

	-   70001, "PUSHED系统错误"
	
	-   80001, "朋友为空"
	-   80002, "VIP为空
	-   80003, "黑名单为空"
	-   80004, "朋友关系已经存在"
	-   80005, "朋友标签为空"
	-   80006, "朋友电话为空"
	-   80007, "朋友描述为空"
	-   80008, "备注名为空"

*   servers
    -   test: 180.76.173.200:9999
*   method
    -   约定：方法只读用get，增删改用post
*   数据库查询
    -    start_id(string)
    -    gt(boolean)
    -    limit(int)
    -    如果传入start_id为空，则取最新的limit条，否则使用start_id来确定开始位置，gt来确定比较的方向，取limit条；
    
### 注册，发送验证码
*   path: /regist/verification-send.do
*   param:
    -   phone(string)
*   return:
    -   通用返回值
*   example:
    -   curl -c cookie/cookie路径 -d 'phone=123456' 'http://180.76.173.200:9999/regist/verification-send.do'

### 注册，验证码是否正确
*   path: /regist/is-verification-right.do
*   param:
    -   verification(string)
*   return: 通用返回值
*   example:
    -   curl -b cookie/cookie路径 -d 'verification=111111' 'http://180.76.173.200:9999/regist/is-verification-right.do'

### 注册设置密码
*   path: /regist/password-set.do
*   param:
	-	password1(string)
	-	password2(string)
*	return:
	-	通用返回值
	-	成功后退出登录
*   example:
    -   curl -b cookie/cookie路径 -d 'password1=1&password2=1' 'http://180.76.173.200:9999/regist/password-set.do'

###	登录
*	path: /login/login.do
*	params:
	-	username(string): 用户名
	-	password(string): 密码
*	return: 
	-	通用返回值 token:[value]
*   example:
    -   curl -c cookie/cookie路径 -d 'phone=1234&password=1' 'http://180.76.173.200:9999/login/login.do'
	
### 快速登录 获取验证码
*	path: /login/verification-send.do
*	params:
	-	phone(string): 密码
*	return: 
	-	通用返回值 token:[value]
*   example:
    -   curl -c cookie/cookie路径 -d 'phone=123456' 'http://180.76.173.200:9999/login/verification-send.do'
	
###     快速登录
*	path: /login/login-quick.do
*	params:
	-	phone(string): 手机号码
*	return: 
	-	通用返回值
*   example:
    -   curl -b cookie/cookie路径 -d 'phone=1234&verification=111111' 'http://180.76.173.200:9999/login/login-quick.do'

###	退出登录
*   path: /login/logout
*	params:	无
*	return: 通用返回值
*   example:
    -   curl -b cookie/cookie路径 'http://180.76.173.200:9999/login/logout.do'

### 忘记密码，生成图片验证码
*   path: /image-verification/generator.do
*   param:
*   return: 图片验证码二进制内容
*   example:
    -   curl -c cookie/cookie路径 'http://180.76.173.200:9999/image-verification/generator.do?'
    -   验证码样例: http://180.76.173.200:9999/hello.jsp

### 忘记密码，发送验证码
*   path: /password/verification-send.do
*   param:
    -   phone(string)
    -   verification_img(string)
*   return: 通用返回值
*   example:
    -   curl -b cookie/cookie路径 -d 'phone=1234&verification_img=fshg' 'http://180.76.173.200:9999/password/verification-send.do?'
    
### 忘记密码，校验验证码
*   path: /password/verification-check.do
*   param:
    -   phone(string)
    -   verification(string)
*   return: 通用返回值
*   example:
    -   curl -b cookie/cookie路径 -d 'phone=1234&verification_img=fshg' 'http://180.76.173.200:9999/password/verification-check.do?'
    
### 忘记密码，设置新密码
*   path: /password/password-set.do
*   param:
	-	password1(string)
	-	password2(string)
*	return:
	-	通用返回值
	-	成功后退出登录
*   example:
    -   curl -b cookie/cookie路径 -d 'password1=111&password2=111' 'http://180.76.173.200:9999/password/password-set.do'
    
###    个人设置，设置头像
*   path: /upload/head-picture.do
*   param:
	-	head_picture(@RequestParam("head_picture") MultipartFile file)
*	return:
	-	通用返回值
*   example:
    -   curl -b cookie -F "head_picture=@/Users/gouxubo/12.png" 'http://180.76.173.200:9999/upload/head-picture.do'
    
###    个人设置，设置昵称
*   path: /person-set/username.do
*   param:
	-	username(string)
*	return:
	-	通用返回值
*   example:
    -   curl -b cookie -d 'username=haha' http://180.76.173.200:9999/person-set/username.do?
    
###    个人设置，设置生日
*   path: /person-set/birthday.do
*   param:
	-	birthday(string)
*	return:
	-	通用返回值
*   example:
    -   curl -b cookie -d 'birthday=haha' http://180.76.173.200:9999/person-set/birthday.do
    
###    个人设置，设置性别
*   path: /person-set/sex.do
*   param:
	-	sex(string)
*	return:
	-	通用返回值
*   example:
    -   curl -b cookie -d 'sex=1' http://180.76.173.200:9999/person-set/sex.do

###    个人设置，设置个性签名
*   path: /person-set/personalized-signature.do
*   param:
	-	personalized_signature(string)
*	return:
	-	通用返回值
*   example:
    -   curl -b cookie -d 'personalized_signature=haha' http://180.76.173.200:9999/person-set/personalized-signature.do
    
###    个人设置，上传地理位置信息
*   path: /person-set/location.do
*   param:
	-	px(Double)经度
	-	py(Double)纬度
*	return:
	-	通用返回值
*   example:
    -   curl -b cookie -d 'sex=1' http://180.76.173.200:9999/person-set/location.do

###    个人设置，获得个人信息
*   path: /person-set/user-info.do
*   param:
*	return:
	-	{
    "ret": 0,
    "user": {
        "birthDay": "",
        "headPictureName": "58f210b0589b559c57d5521912.png",
        "id": "58f210b0589b559c57d55219",
        "personalizedSignature": "",
        "phone": "13112345678",
        "sex": "",
        "userName": ""
    }
}
*   example:
    -   curl -b cookie  http://180.76.173.200:9999/person-set/user-info.do
    
###    个人设置，通过userid获得个人信息
*   path: /person-set/search-by-userid.do
*   param:
    -   userid(String)
*	return:
	-	{
    "ret": 0,
    "user": {
        "birthDay": "",
        "headPictureName": "58f210b0589b559c57d5521912.png",
        "id": "58f210b0589b559c57d55219",
        "personalizedSignature": "",
        "phone": "13112345678",
        "sex": "",
        "userName": ""
    }
}
*   example:
    -   curl -b cookie  http://180.76.173.200:9999/person-set/search-by-userid.do
    
###    个人设置，通过phone获得个人信息
*   path: /person-set/search-by-phone.do
*   param:
    -   phone(String)
*	return:
	-	{
    "ret": 0,
    "user": {
        "birthDay": "",
        "headPictureName": "58f210b0589b559c57d5521912.png",
        "id": "58f210b0589b559c57d55219",
        "personalizedSignature": "",
        "phone": "13112345678",
        "sex": "",
        "userName": ""
    }
}
*   example:
    -   curl -b cookie  http://180.76.173.200:9999/person-set/search-by-phone.do
    
###    个人设置，通过name获得个人信息
*   path: /person-set/search-by-name.do
*   param:
    -   name(String)
*	return:
	-	{
    "ret": 0,
    "userList": [{
        "birthDay": "",
        "headPictureName": "58f210b0589b559c57d5521912.png",
        "id": "58f210b0589b559c57d55219",
        "personalizedSignature": "",
        "phone": "13112345678",
        "sex": "",
        "userName": ""
    }
}]...
*   example:
    -   curl -b cookie  http://180.76.173.200:9999/person-set/search-by-name.do
    
  

###    账户安全，修改密码
*   path: /password/password-change.do
*   param:
	-	old_password(string)
	-	password1(string)
	-	password2(string)
*	return:
	-	通用返回值
*   example:
    -   curl -b cookie -d 'old_password=1&password1=12&password2=12' http://180.76.173.200:9999/password/password-change.do
    
###    账户安全，发送验证码到老手机
*   path: /account-security/verification-send.do
*   param:

*	return:
	-	通用返回值
*   example:
    -   curl -b cookie http://180.76.173.200:9999/account-security/verification-send.do
    
###    账户安全，老手机验证码的验证
*   path: /password/is-verification-right.do
*   param:
	-	verification(string)
*	return:
	-	通用返回值
*   example:
    -   curl -b cookie -d 'verification=111111'  http://180.76.173.200:9999/account-security/is-verification-right.do
    
###    账户安全，新号码获取验证码
*   path: /password/verification-send-phone.do
*   param:
	-	phone(string)
*	return:
	-	通用返回值
*   example:
    -   curl -b cookie -d 'phone=13111110000' http://180.76.173.200:9999/account-security/verification-send-phone.do
    
###    账户安全，提交绑定新号
*   path: /password/phone-change.do
*   param:
	-	phone(string)
	-	verification(string)
*	return:
	-	通用返回值
*   example:
    -   curl -b cookie -d 'phone=123321&verification=111111'  http://180.76.173.200:9999/account-security/phone-change.do
    
###    个人中心首页，点赞
*   path: /homepage/thumbsup.do
*   param:
	-	user_id(string)
*	return:
	-	通用返回值
*   example:
    -   curl -b  cookie  -d 'user_id=[]'  http://180.76.173.200:9999/homepage/thumbsup.do
    
###    个人中心首页，访问我的首页
*   path: /homepage/visit-my-homepage.do
*   param:
	-	visitor_id(string)
*	return:
	-	通用返回值
*   example:
    -   curl -b  cookie -d 'visitor_id=12345321'  http://180.76.173.200:9999/homepage/visit-my-homepage.do
    
###    个人中心首页，新看过我的人数
*   path: /homepage/new-visitors-count.do
*   param:
*   return:
	-	通用返回值
*   example:
    -   curl -b  cookie http://180.76.173.200:9999/homepage/new-visitors-count.do
    
###    个人中心首页，我点赞的人
*   path: /homepage/thumbsup-from-me.do
*   param:
   -	start_id(string)
   -	gt(boolean)
   -	limit(int)
*   return:
	-    通用返回值 返回的json串中：message_id表示消息ID，owner_id表示消息发布者，visitor_id表示点赞的人
*   example:
    -   curl -b cookie -d 'start_id="123"&gt=true&limit=10'  http://180.76.173.200:9999/homepage/thumbsup-from-me.do
    
###    个人中心首页，给我点赞的人
*   path: /homepage/thumbsup-to-me.do
*   param:
   -	start_id(string)
   -	gt(boolean)
   -	limit(int)
*   return:
	-    通用返回值 返回的json串中：message_id表示消息ID，owner_id表示消息发布者，visitor_id表示点赞的人
*   example:
    -   curl -b  cookie  -d 'start_id="123"&gt=true&limit=10' http://180.76.173.200:9999/homepage/thumbsup-to-me.do

###    帮助反馈，图片上传
*   path: /upload/feedback-picture.do
*   param:
	-	@RequestParam("feedback_picture") MultipartFile file
*	return:
	-	通用返回值
*   example:
    -   curl -b  cookie -F "head_picture=@/Users/gouxubo/12.png" 'http://180.76.173.200:9999/upload/feedback-picture.do'

###    帮助反馈，提交
*   path: /feedback/insert.do
*   param:
	-	@RequestParam("feedback_picture") MultipartFile file
	-	content(string)
	-	contactInfo(string)
*	return:
	-	通用返回值
*   example:
    -   curl -b  cookie -d 'content=123&contactInfo=321&image=' http://180.76.173.200:9999/feedback/insert.do

###    我的消息，插入
*   path: /message/insert.do
*   param:
	-	content(string)
	-	source(string)
*	return:
	-	通用返回值
*   example:
    -   curl -d '&content=qwerty&source=web' http://180.76.173.200:9999/message/insert.do
    
###    我的消息，我的消息列表
*   path: /message/my-info.do
*   param:
   -	start_id(string)
   -	gt(boolean)
   -	limit(int)
*	return:
   -	通用返回值 content：消息内容；source：消息来源
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d 'start_id="123"&gt=true&limit=10' http://180.76.173.200:9999/message/my-info.do
 
###  IM相关：创建聊天室
*   path: /chatroom/create.do
*   param:
   -	name(string) 聊天室名称
*	return:
   -	通用返回值 channelId：聊天室ID
*   example:
    -   curl -b cookie -d '-d 'name=test' http://180.76.173.200:9999/chatroom/create.do
    
###  IM相关：得到好友
*   path: /chatroom/get-friends.do
*   param:
*	return:
   -	通用返回值 friends 全部好友信息。
*   example:
    -   curl -b cookie -d '-d 'userid=[v]' http://180.76.173.200:9999/chatroom/get-friends.do
    
###  IM相关：得到聊天室
*   path: /chatroom/get-chatrooms.do
*   param:
*	return:
   -	通用返回值 ChatroomList 全部聊天室信息。聊天室ID和name
*   example:
    -   curl -b cookie -d '-d 'userid=[v]' http://180.76.173.200:9999/chatroom/get-chatrooms.do
   
###  修改聊天室name
*   path: /chatroom/update-name.do
*   param:
   -	roomid(string) 聊天室ID
   -	name(string) 聊天室名称
*   return:
   -	通用返回值 ChatroomList 全部聊天室信息。聊天室ID和name
*   example:
    -   curl -b cookie -d '-d 'name=[v]&roomid=[v]' http://180.76.173.200:9999/chatroom/update-name.do
  
###  个人信息：根据用户名搜索
*   path: /person-set/search-by-name.do
*   param:
   -	name(string) 用户名
*   return:
   -	通用返回值 userList 用户列表
*   example:
    -   curl -b cookie -d '-d 'name=[v]' http://180.76.173.200:9999/person-set/search-by-name.do
    
###  个人信息：根据手机号码搜索
*   path: /person-set/search-by-phone.do
*   param:
   -	phone(string) 
*   return:
   -	通用返回值 user 用户
*   example:
    -   curl -b cookie -d '-d 'phone=[v]' http://180.76.173.200:9999/person-set/search-by-phone.do
    
###  好友：加入好友
*   path: /friends/insert.do
*   param:
   -	friendid(string) 
*   return:
   -	通用返回值 
*   example:
    -   curl -b cookie -d '-d 'friendid=[v]' http://180.76.173.200:9999/friends/insert.do
    
###  好友：设置星标
*   path: /friends/set-VIP.do
*   param:
   -	friendid(string) 
   -	VIP(int) 0表示非VIP，1表示VIP。
*   return:
   -	通用返回值 
*   example:
    -   curl -b cookie -d '-d 'friendid=[v]&VIP=1' http://180.76.173.200:9999/friends/set-VIP.do
    
###  好友：设置黑名单
*   path: /friends/set-black.do
*   param:
   -	friendid(string) 
   -	black(int) 0表示非black，1表示black。
*   return:
   -	通用返回值 
*   example:
    -   curl -b cookie -d '-d 'friendid=[v]&black=1' http://180.76.173.200:9999/friends/set-black.do
    
###  好友：设置备注名
*   path: /friends/set-backname.do
*   param:
   -	friendid(string) 
   -	backname(string)
*   return:
   -	通用返回值 
*   example:
    -   curl -b cookie -d '-d 'friendid=[v]&backname=[v]' http://180.76.173.200:9999/friends/set-backname.do
    
###  好友：设置标签
*   path: /friends/set-tag.do
*   param:
   -	friendid(string) 
   -	tag(string)
*   return:
   -	通用返回值 
*   example:
    -   curl -b cookie -d '-d 'friendid=[v]&tag=[v]' http://180.76.173.200:9999/friends/set-tag.do
 
     
###  好友：设置电话号码
*   path: /friends/set-phone.do
*   param:
   -	friendid(string) 
   -	phone(string)
*   return:
   -	通用返回值 
*   example:
    -   curl -b cookie -d '-d 'friendid=[v]&phone=[v]' http://180.76.173.200:9999/friends/set-phone.do
    
###  好友：设置描述信息
*   path: /friends/set-description.do
*   param:
   -	friendid(string) 
   -	description(string)
*   return:
   -	通用返回值 
*   example:
    -   curl -b cookie -d '-d 'friendid=[v]&description=[v]' http://180.76.173.200:9999/friends/set-description.do
    
###  好友：tag列表
*   path: /friends/get-tag.do
*   param:
   -	userid(string) 
*   return:
   -	通用返回值 
*   example:
    -   curl -b cookie -d '-d 'userid=[v]' http://180.76.173.200:9999/friends/get-tag.do
    
###  好友：好友列表
*   path: /friends/get-friends.do
*   param:
   -	userid(string) 
*   return:
   -	通用返回值 userid friendid backname(备注名) tag phone(设置的朋友的电话) description VIP black username picture 
*   example:
    -   curl -b cookie -d '-d 'userid=[v]' http://180.76.173.200:9999/friends/get-friends.do

###  好友：删除好友
*   path: /friends/delete.do
*   param:
   -	userid(string) 
*   return:
   -	通用返回值 
*   example:
    -   curl -b cookie -d '-d 'userid=[v]' http://180.76.173.200:9999/friends/delete.do
    
###  好友：创建群聊
*   path: /friends/multi-insert.do
*   param:
   -	friendids(string) 用户id使用英文逗号分隔,例如："123,234"
*   return:
   -	通用返回值 
*   example:
    -   curl -b cookie -d '-d 'friendids=[v]' http://180.76.173.200:9999/friends/multi-insert.do
    
###  好友：退出群聊
*   path: /friends/multi-out.do
*   param:
   -    chatroomid(string)
*   return:
   -	通用返回值 
*   example:
    -   curl -b cookie -d '-d 'chatroomid=[v]' http://180.76.173.200:9999/friends/multi-out.do

###  投诉
*   path: /complain/create.do
*   param:
   -    content(string)
*   return:
   -	通用返回值 
*   example:
    -   curl -b cookie -d '-d 'content=[v]' http://180.76.173.200:9999/complain/create.do

###  附近的人
*   path: /location/near.do
*   param:
   -    px(double)经度
   -    py(double)纬度
*   return:
   -	通用返回值 userList
*   example:
    -   curl -b cookie -d '-d 'px=[v]&py=[v]' http://180.76.173.200:9999/location/near.do

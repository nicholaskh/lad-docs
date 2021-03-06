,User System APIs
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
*   聊天室类型type：1表示1对1聊天；2表示群聊；3表示面对面建群。
*   聊天室创建说明：1、同意添加好友后，后台会自动创建一个一对一聊天室。传入userid和friendis去subscribe。返回channelID；
2、chatroom/create 会创建一个聊天室，传入userid去subscribe，返回channelID，之后可以通过添加聊天室用户去家人。
3、friends/multi-insert，会创建一个多人聊天室，要传入friendids，这个ID要包括userid，统一由前端传入。传入friendids去subscribe，返回channelID；
    
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
*   path: /login/logout.do
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
*   path: /feedback/.do
*   param:
	-	@RequestParam("feedback_picture") MultipartFile file
	-	content(string)
	-	contactInfo(string)
*	return:
	-	通用返回值
*   example:
    -   curl -b  cookie -d 'content=123&contactInfo=321&image=' http://180.76.173.200:9999/feedback/insert.do
	
	
### 反馈，帖子举报
*   path: /feedback/note-tips-add.do
*   param:
	-	module(string) 举报分类
	-	subModule(string) 举报次级分类
	-	content(string) 举报内容
	-	targetId(string) 举报目标帖子id
	-	targetTitle(string) 举报目标帖子题目
	-   MultipartFile[] pictures 举报图片
*	return:
	-	通用返回值
*   example:
    -   curl -b  cookie -d 'module=[]&subModule=[]&content=[]&targetId=[]&targetTitle=[]pictures=[]&' http://180.76.173.200:9999/feedback/note-tips-add.do
	

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
    -   curl -b cookie -d  'name=test' http://180.76.173.200:9999/chatroom/create.do
    
###  IM相关：得到好友
*   path: /chatroom/get-friends.do
*   param:
*	return:
   -	通用返回值 friends 全部好友信息。
*   example:
    -   curl -b cookie -d 'userid=[v]' http://180.76.173.200:9999/chatroom/get-friends.do
    
###  IM相关：得到全部聊天室
*   path: /chatroom/get-my-chatrooms.do
*   param:
*	return:
   -	通用返回值 ChatroomList 全部聊天室信息.top字段表示是否置顶。
*   example:
    -   curl -b cookie -d 'userid=[v]' http://180.76.173.200:9999/chatroom/get-my-chatrooms.do

###  IM相关：得到聊天室
*   path: /chatroom/get-chatroom-info.do
*   param:
   -	chatroomid(string) 聊天室ID
*	return:
   -	通用返回值 chatroom 聊天室信息
*   example:
    -   curl -b cookie -d 'chatroomid=[v]' http://180.76.173.200:9999/chatroom/get-chatroom-info.do
   
###  修改聊天室name
*   path: /chatroom/update-name.do
*   param:
   -	roomid(string) 聊天室ID
   -	name(string) 聊天室名称
*   return:
   -	通用返回值 ChatroomList 全部聊天室信息。聊天室ID和name
*   example:
    -   curl -b cookie -d 'name=[v]&roomid=[v]' http://180.76.173.200:9999/chatroom/update-name.do

###  聊天室：加入用户
*   path: /chatroom/insert-user.do
*   param:
   -	chatroomid(string) 聊天室ID
   -	userids(string) 一个或多个用户ID，用“,”隔开
*   return:
   -	通用返回值
*   example:
    -   curl -b cookie -d 'userids=[v]&chatroomid=[v]' http://180.76.173.200:9999/chatroom/insert-user.do

###  聊天室：删除用户
*   path: /chatroom/delete-user.do
*   param:
   -	chatroomid(string) 聊天室ID
   -	userids(string) 一个或多个用户ID，用“,”隔开
*   return:
   -	通用返回值
*   example:
    -   curl -b cookie -d  'userids=[v]&chatroomid=[v]' http://180.76.173.200:9999/chatroom/delete-user.do

###  聊天室：置顶
*   path: /chatroom/set-top.do
*   param:
   -	chatroomid(string) 聊天室ID
*   return:
   -	通用返回值
*   example:
    -   curl -b cookie -d  'userid=[v]&chatroomid=[v]' http://180.76.173.200:9999/chatroom/set-top.do

###  聊天室：取消置顶
*   path: /chatroom/cancel-top.do
*   param:
   -	chatroomid(string) 聊天室ID
*   return:
   -	通用返回值
*   example:
    -   curl -b cookie -d  'userid=[v]&chatroomid=[v]' http://180.76.173.200:9999/chatroom/cancel-top.do
	
###  聊天室：面对面创建群聊，通过SEQ加入面对面群聊接口。

*  如果SEQ不存在，则创建面对面群聊，存在则加入；通过拉人的方式加入面对面群聊，请使用 chatroom/insert-user.do
*   path: /chatroom/factoface-create.do
*   param:
   -	seq(int) 面对面群聊数字序列
   -	px(double) 建立群聊人地理位置经度
   -	py(double) 建立群聊人地理位置纬度
*   return:
   -	通用返回值  channelId 聊天室ID
*   example:
    -   curl -b cookie -d  'seq=[v]&px=[v]&py=[v]' http://180.76.173.200:9999/chatroom/factoface-create.do
	
  
###  个人信息：根据用户名搜索
*   path: /person-set/search-by-name.do
*   param:
   -	name(string) 用户名
*   return:
   -	通用返回值 userList 用户列表
*   example:
    -   curl -b cookie -d 'name=[v]' http://180.76.173.200:9999/person-set/search-by-name.do
    
###  个人信息：根据手机号码搜索
*   path: /person-set/search-by-phone.do
*   param:
   -	phone(string) 
*   return:
   -	通用返回值 user 用户
*   example:
    -   curl -b cookie -d 'phone=[v]' http://180.76.173.200:9999/person-set/search-by-phone.do
    
###  好友：申请添加好友
*   path: /friends/apply.do
*   param:
   -	friendid(string) 
*   return:
   -	通用返回值 
*   example:
    -   curl -b cookie -d 'friendid=[v]' http://180.76.173.200:9999/friends/apply.do

###  好友：同意添加好友
*   path: /friends/agree.do
*   param:
   -	id(string) 好友数据表记录的ID，不是朋友ID和userid。
*   return:
   -	通用返回值 channelId 已经创建了一对一聊天室
*   example:
    -   curl -b cookie -d 'id=[v]' http://180.76.173.200:9999/friends/agree.do

###  好友：拒绝添加好友
*   path: /friends/refuse.do
*   param:
   -	id(string) 好友数据表记录的ID，不是朋友ID和userid。
*   return:
   -	通用返回值 
*   example:
    -   curl -b cookie -d 'id=[v]' http://180.76.173.200:9999/friends/refuse.do

###  好友：获得申请添加好友列表
*   path: /friends/apply-list.do
*   param:
*   return:
   -	通用返回值 userVoList 好友列表信息
*   example:
    -   curl -b cookie  http://180.76.173.200:9999/friends/apply-list.do
    
###  好友：设置星标
*   path: /friends/set-VIP.do
*   param:
   -	friendid(string) 
   -	VIP(int) 0表示非VIP，1表示VIP。
*   return:
   -	通用返回值 
*   example:
    -   curl -b cookie -d  'friendid=[v]&VIP=1' http://180.76.173.200:9999/friends/set-VIP.do
    
###  好友：设置黑名单
*   path: /friends/set-black.do
*   param:
   -	friendid(string) 
   -	black(int) 0表示非black，1表示black。
*   return:
   -	通用返回值 
*   example:
    -   curl -b cookie -d 'friendid=[v]&black=1' http://180.76.173.200:9999/friends/set-black.do
    
###  好友：设置备注名
*   path: /friends/set-backname.do
*   param:
   -	friendid(string) 
   -	backname(string)
*   return:
   -	通用返回值 
*   example:
    -   curl -b cookie -d 'friendid=[v]&backname=[v]' http://180.76.173.200:9999/friends/set-backname.do
 
###  好友：设置电话号码
*   path: /friends/set-phone.do
*   param:
   -	friendid(string) 
   -	phone(string)
*   return:
   -	通用返回值 
*   example:
    -   curl -b cookie -d  'friendid=[v]&phone=[v]' http://180.76.173.200:9999/friends/set-phone.do
    
###  好友：设置描述信息
*   path: /friends/set-description.do
*   param:
   -	friendid(string) 
   -	description(string)
*   return:
   -	通用返回值 
*   example:
    -   curl -b cookie -d  'friendid=[v]&description=[v]' http://180.76.173.200:9999/friends/set-description.do
    
###  好友：好友列表
*   path: /friends/get-friends.do
*   param:
   -	userid(string) 
*   return:
   -	通用返回值 userid friendid backname(备注名) tag phone(设置的朋友的电话) description VIP black username picture 
*   example:
    -   curl -b cookie -d 'userid=[v]' http://180.76.173.200:9999/friends/get-friends.do

###  好友：删除好友
*   path: /friends/delete.do
*   param:
   -	friendid(string) 
*   return:
   -	通用返回值 
*   example:
    -   curl -b cookie -d  'friendid=[v]' http://180.76.173.200:9999/friends/delete.do
    
###  好友：创建群聊
*   path: /friends/multi-insert.do
*   param:
   -	friendids(string) 用户id使用英文逗号分隔,例如："123,234"，包含userid
*   return:
   -	通用返回值 channelId
*   example:
    -   curl -b cookie -d  'friendids=[v]' http://180.76.173.200:9999/friends/multi-insert.do
    
###  好友：退出群聊
*   path: /friends/multi-out.do
*   param:
   -    chatroomid(string)
*   return:
   -	通用返回值 
*   example:
    -   curl -b cookie -d 'chatroomid=[v]' http://180.76.173.200:9999/friends/multi-out.do

###  投诉
*   path: /complain/create.do
*   param:
   -    content(string)
*   return:
   -	通用返回值 
*   example:
    -   curl -b cookie -d 'content=[v]' http://180.76.173.200:9999/complain/create.do

###  附近的人
*   path: /location/near.do
*   param:
   -    px(double)经度
   -    py(double)纬度
*   return:
   -	通用返回值 userList
*   example:
    -   curl -b cookie -d 'px=[v]&py=[v]' http://180.76.173.200:9999/location/near.do

###  标签:对指定的好友添加或修改标签
*   path: /tag/set-tags.do
*   param:
   -    tagNames(String) 标签,多个以英文逗号隔开
   -    friendsid(String) 好友ID
*   return:
   -	通用返回值 
*   example:
    -   curl -b cookie -d 'tagNames=[v]&friendsid=[v]' http://180.76.173.200:9999/tag/set-tags.do
 
###  标签:更具标签名称添加或修改好友
*   path: /tag/add-tag-friends.do
*   param:
   -    tagName(String) 标签
   -    friendsids(String) 好友ID,多个以英文逗号隔开
*   return:
   -	通用返回值 
*   example:
    -   curl -b cookie -d 'tagNames=[v]&friendsid=[v]' http://180.76.173.200:9999/tag/add-tag-friends.do
 

###  标签:得到指定好友标签
*   path: /tag/get-friend-tags.do
*   param:
   -    friendid(String) 好友ID
*   return:
   -	通用返回值 tags 标签列表
*   example:
    -   curl -b cookie -d 'friendid=[v]' http://180.76.173.200:9999/tag/get-friend-tags.do


###  标签: 得到当前用户添加过的所有标签名称
*   path: /tag/get-tags.do
*   param:
*   return: 
   -	通用返回值 tags 标签列表
*   example:
    -   curl -b cookie http://180.76.173.200:9999/tag/get-tags.do
 

###  标签:根据标签名称查询或搜索好友信息
*   path: /tag/get-by-tagName.do
*   param:
   -    tagName(String) 标签名称
*   return:
   -	通用返回值 userVos用户信息
*   example:
    -   curl -b cookie -d 'tagName=[v]' http://180.76.173.200:9999/tag/friends-by-tag.do
 
 
###  标签:获取所有标签及标签关联的好友
*   path: /tag/get-tag-list.do
*   param:
*   return:
   -	通用返回值 tagVos
*   example:
    -   curl -b cookie -d http://180.76.173.200:9999/tag/get-tag-list.do

###  标签: 删除标签
*   path: /tag/delete-tag.do
*   param:
   -    tagid(String) 标签ID 
*   return:
   -	通用返回值
*   example:
    -   curl -b cookie -d 'tagid=[v]'  http://180.76.173.200:9999/tag/delete-tag.do
 
 

###  圈子:圈子创建前校验用户当前圈子数量及级别
*   path: /circle/pre-create.do
*   return:
   -	通用返回值
*   example:
    -   curl -b cookie -d  http://180.76.173.200:9999/circle/pre-creat.do
 

###  圈子:创建
*   path: /circle/insert.do
*   param:
   -    px(double)
   -    py(double)
   -    name(String)
   -    tag(String)
   -    sub_tag(String)
   -    description(String) 简介
   -    province   省或者直辖市
   -    city    城市，直辖市与province一致
   -    district  县或者区
   -    isOpen(boolean) 是否5公里加入
   -    head_picture(file) 圈子头像
*   return:
   -	通用返回值
*   example:
    -   curl -b cookie -d 'px=[v]&py=[v]&name=[v]&tag=[v]&sub_tag=[v]&description=[v]&isOpen=[v]&head_picture=[v]' 
 http://180.76.173.200:9999/circle/insert.do

    
### 圈子，设置头像
*   path: /circle/head-picture/head-picture.do
*   param:
   -    head_picture(@RequestParam("head_picture") MultipartFile file)
   -    circleid(String)
*	return:
	-	通用返回值
*   example:
    -   curl -b cookie -F "head_picture=@/Users/gouxubo/12.png" 'http://180.76.173.200:9999/circle/head-picture.do'

###  圈子:申请加入
*   path: /circle/apply-insert.do
*   param:
   -    circleid(String)
   -    reason(String) 申请理由
   -    isNotice(boolean) 是否通知好友
*   return:
   -	通用返回值
*   example:
    -   curl -b cookie -d 'circleid=[v]&reason=[v]&isNotice=[v]  http://180.76.173.200:9999/circle/apply-insert.do

###  圈子:我的圈子
*   path: /circle/my-info.do
*   param:
*   return:
   -	通用返回值 circleList
*   example:
    -   curl -b cookie  http://180.76.173.200:9999/circle/my-info.do

###  圈子:申请人列表
*   path: /circle/user-apply.do
*   param:
   -    circleid(String)
*   return:
   -	通用返回值 申请人信息
*   example:
    -   curl -b cookie -d 'circleid=[v]'  http://180.76.173.200:9999/circle/user-apply.do

###  圈子:同意加入
*   path: /circle/user-apply-agree.do
*   param:
   -    circleid(String)
   -    userids(String) 多个用逗号隔开
*   return:
   -	通用返回值
*   example:
    -   curl -b cookie -d 'circleid=[v]&userids=[v]'  http://180.76.173.200:9999/circle/user-apply-agree.do

###  圈子:拒绝加入
*   path: /circle/user-apply-refuse.do
*   param:
   -    circleid(String)
   -    userids(String)多个用逗号隔开 
   -    refuse(String) 拒绝理由
*   return:
   -	通用返回值
*   example:
    -   curl -b cookie -d 'circleid=[v]&userids=[v]&refuse=[v]'  http://180.76.173.200:9999/circle/user-apply-refuse.do
 
###  圈子:列表
*   path: /circle/list.do
*   param:
   -    sub_tag(String)
   -    tag(String)
   -    category(String)
*   return:
   -	通用返回值 circleList： id name userSize用户数 notesSize 帖子数
*   example:
    -   curl -b cookie -d 'tag=[v]&sub_tag=[v]&category=[v]'  http://180.76.173.200:9999/circle/list.do
 
 
###  圈子:删除圈子成员，只有群主才能删除
*   path: /circle/delete-user.do
*   param:
   -    circleid(String)
   -    userid(String) 被删除人
*   return:
   -	通用返回值
*   example:
    -   curl -b cookie -d 'userids=[v]&circleid=[v]'  http://180.76.173.200:9999/circle/delete-user.do
 
###  圈子:转让圈子接口
*   path: /circle/transfer.do
*   param:
   -    circleid(String)
   -    userid(String) 转让人
*   return:
   -	通用返回值
*   example:
    -   curl -b cookie -d 'userid=[v]&circleid=[v]'  http://180.76.173.200:9999/circle/transfer.do
 
###  圈子:退出群组
*   path: /circle/quit.do
*   param:
   -    circleid(String)
*   return:
   -	通用返回值
*   example:
    -   curl -b cookie -d 'userid=[v]&circleid=[v]'  http://180.76.173.200:9999/circle/quit.do
 
###  圈子:我加入的圈子
*   path: /circle/my-circles.do
*   param:
   -	start_id(string)
   -	gt(boolean)
   -	limit(int)
*	return:
   -	通用返回值 circleList： id name userSize用户数 notesSize 帖子数   top ：1 表示置顶 ，0未置顶
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d 'start_id="123"&gt=true&limit=10' http://180.76.173.200:9999/circle/my-circles.do

###  圈子:猜你喜欢
*   path: /circle/guess-you-like.do
*   param:

*	return:
   -	通用返回值 circleList： id name userSize用户数 notesSize 帖子数
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d 'start_id="123"&gt=true&limit=10' http://180.76.173.200:9999/circle/guess-you-like.do

###  圈子: 红人列表
*   path: /circle/red-star-list.do
*   param:
    - circleid(string)
*	return:
   -	通用返回值 total：红人总榜 列表 ；week： 红人周榜列表
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d 'circleid=[v]' http://180.76.173.200:9999/circle/red-star-list.do

###  圈子: 圈子详情
*   path: /circle/circle-info.do
*   param:
    - circleid(string)
*	return:
   -	通用返回值  圈子信息   top ：1 表示置顶 ，0未置顶
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d 'circleid=[v]' http://180.76.173.200:9999/circle/circle-info.do	
	
###  圈子: 置顶圈子
*   path: /circle/set-top.do
*   param:
    - circleid(string)
*	return:
   -	通用返回值 
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d 'circleid=[v]' http://180.76.173.200:9999/circle/set-top.do	
	
###  圈子: 取消圈子置顶
*   path: /circle/cancel-top.do
*   param:
    - circleid(string)
*	return:
   -	通用返回值 
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d 'circleid=[v]' http://180.76.173.200:9999/circle/cancel-top.do	
	
	
### 帖子:圈子内最新动态 帖子
*   path: /note/new-situation.do
*   param:
   -	circleid(string)
   -	start_id(string)
   -	gt(boolean)
   -	limit(int)
*	return:
   -	通用返回值 noteVoList： nodeid subject content visitCount访问量 commontCount 评论数 transCount转发数
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d 'circleid=[v]&start_id="123"&gt=true&limit=10' http://180.76.173.200:9999/note/new-situation.do
	
	
### 帖子:圈子精华 帖子
*   path: /note/essential-note.do
*   param:
   -	circleid(string)
   -	start_id(string)
   -	limit(int)
*	return:
   -	通用返回值 noteVoList： nodeid subject content visitCount访问量 commontCount 评论数 transCount转发数
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d 'circleid=[v]&start_id=[v]&limit=[v]' http://180.76.173.200:9999/note/essential-note.do
	

### 帖子:圈子内置顶的 帖子
*   path: /note/top-notes.do
*   param:
   -	circleid(string)
   -	start_id(string)
   -	limit(int)
*	return:
   -	通用返回值 noteVoList： nodeid subject content visitCount访问量 commontCount 评论数 transCount转发数
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d 'circleid=[v]&start_id=[v]&limit=[v]' http://180.76.173.200:9999/note/top-notes.do
	

###  帖子:插入新的帖子

###### noteJson数据
    {
			"position":[px,py],   地理位置坐标
            "subject":"标题",
            "content":"内容",
            "landmark":"地标",
            "circleId":"圈子id",
            "type":"图片或者视频" pic or video
            "async" : true or false 是否同步到我的动态 
    }
*   path: /note/insert.do
*   param:
   -    noteJson(json)
   -    pictures(MultipartFile[])图片或视频文件数组
*   return:
   -	通用返回值
*   example:
    -   curl -b cookie -d 'px=[v]&py=[v]&subject=[v]&landmark=[v]&content=[v]&circleid=[v]&pictures=[v]'  http://180.76.173.200:9999/note/insert.do


###  帖子:设置图片
*   path: /note/phones.do
*   param:
   -    @RequestParam("photos") MultipartFile[] files
   -    noteid(String)
*   return:
   -	通用返回值
*   example


###  帖子:圈子内热门帖子列表
*   path: /note/hot-notes.do
*   param:
   -    circleid(String)
*   return:
   -	通用返回值 noteVoList： nodeid subject content visitCount访问量 commontCount 评论数 transCount转发数
*   example:
    -   curl -b cookie -F "circleid=[v]"  http://180.76.173.200:9999/note/hot-notes.do
 
 
###  帖子:帖子详情
*   path: /note/note-info.do
*   param:
   -    noteid(String) 帖子id
*   return:
   -	通用返回值 noteVo 帖子信息  is
*   example:
    -   curl -b cookie -F "noteid=[v]"  http://180.76.173.200:9999/note/note-info.do
 
###  帖子:我的帖子
*   path: /note/my-notes.do
*   param:
   -	start_id(string)
   -	gt(boolean)
   -	limit(int)
*   return:
   -	通用返回值 noteVo 帖子信息  thumbsup 表示当前用户是在这个帖子点赞
*   example:
   -   curl -b cookie -F "start_id=‘123’&gt=true&limit=10"  http://180.76.173.200:9999/note/my-notes.do
 

###  帖子:圈主删除帖子
*   path: /note/delete-circle-notes.do
*   param:
   -    noteids(String) 要删除的帖子id，多个以逗号隔开
   -    circleid(String) 圈子id
*   return:
   -	通用返回值 
*   example:
    -   curl -b cookie -F "noteids=[v]&circleid=[v]"  http://180.76.173.200:9999/note/delete-circle-notes.do

 
###  帖子:用户删除自己的帖子
*   path: /note/delete-my-notes.do
*   param:
   -    noteids(String) 要删除的帖子id，多个以逗号隔开
*   return:
   -	通用返回值 
*   example:
    -   curl -b cookie -F "noteids=[v]&circleid=[v]"  http://180.76.173.200:9999/note/delete-my-notes.do
 
 
###  帖子:回复帖子或回复帖子评论
*   path: /note/add-comment.do
*   param:
   -    circleid(String)
   -    noteid(String) 帖子id
   -    countent(String) 内容
   -    parentid(String) 如回复其他人评论则必须输入，其他人评论的id
*   return:
   -	通用返回值 commentVo 评论信息， 评论信息 commentId 评论id， userid 评论人id， username 评论人名称； parentid 其他人评论id; parentUserName 其他人的名称，parentUserid 其他人的id 
*   example:
    -   curl -b cookie -F "circleid=[v]&noteid=[v]&countent=[v]&parentid=[v]"  http://180.76.173.200:9999/note/add-comment.do
 
 
###  帖子:获取帖子评论
*   path: /note/get-comments.do
*   param:
   -    noteid(String) 帖子id
   -	start_id(string)
   -	gt(boolean)
   -	limit(int)
*   return:
   -	通用返回值 commentVoList  
*   example:
    -   curl -b cookie -F "noteid=[v]&start_id=[v]&gt=[v]&limit=[v]"  http://180.76.173.200:9999/note/get-comments.do
 
  
###  帖子:获取自己的评论
*   path: /note/get-self-comments.do
*   param:
   -	start_id(string)
   -	gt(boolean)
   -	limit(int)
*   return:
   -	通用返回值 commentVoList 评论信息 commentId 评论id， userid 评论人id， username 评论人名称； parentid 回复的评论id; parentUserName 回复评论的评论人名称，parentUserid 回复评论人的id  
*   example:
    -   curl -b cookie -F "start_id=[v]&gt=[v]&limit=[v]"  http://180.76.173.200:9999/note/get-self-comments.do
 
 
###  帖子:删除自己的评论
*   path: /note/delete-self-comment.do
*   param:
   -    commentid(String) 评论id
*   return:
   -	通用返回值 
*   example:
    -   curl -b cookie -F "commentid=[v]"  http://180.76.173.200:9999/note/delete-self-comment.do
 
 
###  帖子:获取自己被评论的帖子
*   path: /note/my-comment-notes.do
*   param:
   -	start_id(string)
   -	gt(boolean)
   -	limit(int)
*   return:
   -	通用返回值  noteVoList
*   example:
    -   curl -b cookie -F "start_id=[v]&gt=[v]&limit=[v]"  http://180.76.173.200:9999/note/my-comment-notes.do
 
 
###  帖子:帖子点赞
*   path: /note/thumbsup.do
*   param:
   -    noteid(String) 帖子id
*   return:
   -	通用返回值 
*   example:
    -   curl -b cookie -F "noteid=[v]"  http://180.76.173.200:9999/note/thumbsup.do
 
###  帖子:取消点赞
*   path: /note/cancal-thumbsup.do
*   param:
   -    noteid(String) 帖子id
*   return:
   -	通用返回值 
*   example:
    -   curl -b cookie -F "noteid=[v]"  http://180.76.173.200:9999/note/cancal-thumbsup.do
 
  
###  帖子:获取帖子点赞列表
*   path: /note/get-note-thumbsups.do
*   param:
   -    noteid(String) 帖子id
   -	start_id(string)
   -	gt(boolean)
   -	limit(int)
*   return:
   -	通用返回值  userVoList
*   example:
    -   curl -b cookie -F "noteid=[v]&start_id=[v]&gt=[v]&limit=[v]"  http://180.76.173.200:9999/note/get-note-thumbsups.do

 
###  帖子:评论点赞
*   path: /note/comment-thumbsup.do
*   param:
   -    commentid(String) 评论id
   -    isThumnbsup(boolean) true 点赞，false 取消点赞
*   return:
   -	通用返回值 
*   example:
    -   curl -b cookie -F "commentid=[v]"  http://180.76.173.200:9999/note/comment-thumbsup.do
 

 
###  用户更新地理位置
*   path: /location/update.do
*   param:
   -    px(double)经度
   -    py(double)纬度
   -    phone(string)用户电话
*   return:
   -	通用返回值
*   example:
    -   curl -b cookie -d 'px=[v]&py=[v]&phone=[v]' http://180.76.173.200:9999/location/update.do
 
 
###  圈子: 添加或删除管理员
*   path: /circle/master.do
*   param:
    - circleid(string)
	- userids(string) 一个或多个用户
	- isAdd(boolean) true 添加管理员； false 删除管理员
*	return:
   -	通用返回值 
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d 'circleid=[v]&userids=[v]&isAdd=[v]' http://180.76.173.200:9999/circle/master.do	

	
###  圈子: 根据关键字搜索圈子
*   path: /circle/search.do
*   param:
    - keyword(string)
*	return:
   -	通用返回值 
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d 'keyword=[v]' http://180.76.173.200:9999/circle/search.do 
 
###  圈子: 获取管理员
*   path: /circle/get-master.do
*   param:
    - circleid(string)
*	returncircleid
   -	通用返回值 
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d 'circleid=[v]' http://180.76.173.200:9999/circle/get-master.do 
 
###  圈子: 获取圈主
*   path: /circle/get-creater.do
*   param:
    - circleid(string)
*	return:
   -	通用返回值 
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d 'circleid=[v]' http://180.76.173.200:9999/circle/get-creater.do

###  圈子: 获取圈子分类
*   path: /circle/circle-type.do
*   param: 
*	return:
   -	通用返回值 types 一级分类及以及分类下二级分类 
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d 'circleid=[v]' http://180.76.173.200:9999/circle/circle-type.do


###  圈子: 添加圈子分类
*   path: /circle/add-circle-type.do
*   param:
    - name(string) 分类名称
    - parent(string) 父分类名称，若本身为一级分类，则不填写 
    - level(int) 分类级别， 1为一级分类； 2为二级分类
*	return:
   -	通用返回值 
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d 'name=[v]&parent=[v]&level=[v]' http://180.76.173.200:9999/circle/add-circle-type.do

###  圈子: 根据分类获取圈子
*   path: /circle/get-by-type.do
*   param:
   -tag(String)  一级分类
   -	sub_tag(String)  二级分类，如只查询一级分类，则可为空串
   -	page(int)
   -	limit(int)
*	return:
   -	通用返回值  userAdd 0 未加入， 1 已经加入， 2 已经退出 
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d 'type=[v]&level=[v]&start_id=[v]&gt=[v]&limit=[v]' http://180.76.173.200:9999/circle/get-by-type.do

###  圈子: 附近活跃人员
*   path: /circle/near-people.do
*   param:
   -circleid(String) 当前圈子id
   -	px(double) 经度
   -	py(double) 纬度
*	return:
   -	通用返回值  userVoList
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d 'circleid=[v]&px=[v]&py=[v]' http://180.76.173.200:9999/circle/near-people.do

###  圈子: 附近圈子
*   path: /circle/near-circle.do
*   param:
   -	px(double) 经度
   -	py(double) 纬度
*	return:
   -	通用返回值 circleVoList 
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d 'x=[v]&py=[v]' http://180.76.173.200:9999/circle/near-circle.do

###  圈子: 当前用户在圈子中的角色
*   path: /circle/circle-role.do
*   param:
   -	circleid(string) 圈子id
*	return:
   -	通用返回值 role  0，普通用户或未登录； 1 管理员， 2 圈主 
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d 'circleid=[v]' http://180.76.173.200:9999/circle/circle-role.do
 
###  圈子: 圈子用户
*   path: /circle/persons.do
*   param:
   -	circleid(string) 圈子id
*	return:
   -	通用返回值 userVoList 
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d 'circleid=[v]' http://180.76.173.200:9999/circle/persons.do   
 
###  圈子: 更新圈子名称
*   path: /circle/update-name.do
*   param:
   -	circleid(string) 圈子id
   -	name(string) 圈子名称
*	return:
   -	通用返回值  
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d 'circleid=[v]&name=[v]' http://180.76.173.200:9999/circle/update-name.do 

###  圈子: 圈子不允任何人加入
*   path: /circle/open.do
*   param:
   -	circleid(string) 圈子id
   -	open(boolean) 圈子不允任何人加入开关， true 打开， false 关闭
*	return:
   -	通用返回值  
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d 'circleid=[v]&open=[v]' http://180.76.173.200:9999/circle/open.do 


###  圈子: 圈子加入验证
*   path: /circle/verify.do
*   param:
   -	circleid(string) 圈子id
   -	verify(boolean) 圈子加入验证， true 打开， false 关闭
*	return:
   -	通用返回值  
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d 'circleid=[v]&&verify=[v]' http://180.76.173.200:9999/circle/verify.do 

###  圈子: 圈子公告修改
*   path: /circle/notice.do
*   param:
   -	circleid(string) 圈子id
   -	title(string)  公告标题 ，若删除公告请将标题和内容输入为空  
   -	content(string) 公告内容
*	return:
   -	通用返回值  
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d 'circleid=[v]&title=[v]&content=[v]' http://180.76.173.200:9999/circle/notice.do


###  圈子: 举报圈子
*   path: /circle/feed-tips.do
*   param:
   -	circleid(string) 圈子id
   -	title(string)  举报标题  
   -	content(string) 举报内容
   -	contact（string） 举报联系人
   -	images（file[]） 图片数组
*	return:
   -	通用返回值  
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d 'circleid=[v]&title=[v]&content=[v]' http://180.76.173.200:9999/circle/feed-tips.do

###  圈子: 圈子内帖子
*   path: /note/circle-notes.do
*   param:
   -	circleid(string) 圈子id
   -	start_id(string)  
   -	limit(int) 
*	return:
   -	通用返回值  noteVoList  essence：1表示加精，0表示未加精， top：1表示置顶， 0 表示未置顶
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d 'circleid=[v]&start_id=[v]&limit=[v]' http://180.76.173.200:9999/circle/circle-note.do


###  圈子: 圈子内帖子加精或取消加精
*   path: /note/set-essence.do
*   param:
   -	circleid(string) 圈子id
   -	noteid(string)  
   -	essence(int) 1 加精， 0 取消加精 
*	return:
   -	通用返回值  noteVoList  essence：1表示加精，0表示未加精， top：1表示置顶， 0 表示未置顶
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d 'circleid=[v]&start_id=[v]&essence=[v]' http://180.76.173.200:9999/circle/set-essences.do


###  圈子: 圈子内帖子置顶或取消置顶
*   path: /note/set-top.do
*   param:
   -	circleid(string) 圈子id
   -	noteid(string)  
   -	top(int) 1 置顶， 0 取消置顶  
*	return:
   -	通用返回值 
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d 'circleid=[v]&start_id=[v]&limit=[v]' http://180.76.173.200:9999/circle/circle-note.do

	
###  圈子: 获取圈子热搜关键字
*   path: /circle/hot-searchs.do
*   param:
*	return:
   -	通用返回值 hotWords 
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d  http://180.76.173.200:9999/circle/search.do 

###  圈子: 根据城市查找圈子
*   path: /circle/search-city.do
*   param:
    - 	province(string) 省或者直辖市
    -   city(string)    城市，直辖市与province一致
    -   district(string)  县或者区
    -   page(int) 当前展示页数，由于按照热度排序，所以不能通过id或者时间来处理，只能按照页码来，从1开始
    -   limit（int）每页展示条数
*	return:
   -	通用返回值 circleVoList 
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d  http://180.76.173.200:9999/circle/search-city.do 

	
###  圈子: 获取城市热搜
*   path: /circle/hot-citys.do
*   param:
*	return:
   -	通用返回值 hotCitys 
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d  http://180.76.173.200:9999/circle/hot-citys.do


	
###  圈子: 获取相关圈子
*   path: /circle/related.do
*   param:
    -  	circleid(string) 圈子id
    -   page(int)    当前页数，从1开始
    -   limit(int)  每页展示条数，初始默认为2
*	return:
   -	通用返回值 circleVoList 
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d  
    -   http://180.76.173.200:9999/circle/related.do



###  城市: 获取省份
*   path: /city/get-province.do
*   param:
*	return:
   -	通用返回值 provinces 
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d  http://180.76.173.200:9999/city/get-province.do 


###  城市: 获取省份下地级市
*   path: /city/get-province-city.do
*   param:
    - 	province(string) 省或者直辖市
*	return:
   -	通用返回值 citys 
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d  http://180.76.173.200:9999/city/get-province-city.do 

###  城市: 获取直辖市下区或者县，或者地级市，切换区县
*   path: /city/get-city.do
*   param:
    - 	city(string) 省或者直辖市
*	return:
   -	通用返回值 citys 
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d  http://180.76.173.200:9999/city/get-city.do 

###  城市: 非直辖市下县或者区，直辖市返回与上个方法一致
*   path: /city/get-district.do
*   param:
    - 	province(string) 省或市
    -   city(string)    城市
    -   district(string)  县或者区
*	return:
   -	通用返回值 districts 
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d  http://180.76.173.200:9999/city/get-district.do 

###  城市: 获所有城市信息
*   path: /city/get-all.do
*   param:
*	return:
   -	通用返回值 provinces 
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d  http://180.76.173.200:9999/city/get-all.do 


###  聊天：收藏聊天记录
*   path: /collect/chat.do
*   param:
   -    title(String) 具体的聊天对象或群组名称 
   -    content(String)
*   return:
   -	通用返回值   col-time:聊天收藏时间 (yyyy-MM-dd HH:mm:ss) 
*   example:
    -   curl -b cookie -F "title=[v]&content=[v]" http://180.76.173.200:9999/chat/collect/chat.do


###  聊天：获取收藏的聊天记录
*   path: /collect/my-chats.do
*   param:
   -    start_id(String) 分页时最后起始的收藏聊天记录的id，为空则表示从最新一条开发
   -    limit(int) 每页显示条数
*   return:
   -	通用返回值   col-chats 收藏聊天 
*   example:
    -   curl -b cookie -F "start_id=[v]&limit=[v]" http://180.76.173.200:9999/chat/collect/my-chats.do
    

###  用户: 获取所有兴趣列表
*   path: /homepage/interest.do
*   param:
*	return:
   -	通用返回值 
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d  http://180.76.173.200:9999/homepage/interest.do



###  用户: 获取指定兴趣类型下兴趣列表
*   path: /homepage/get-interest.do
*   param:
    -   type(int) 兴趣类型：1 sports; 2 musics; 3 lifes; 4 trips 
*	return:
    -	通用返回值 
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d   "type=[v]"  http://180.76.173.200:9999/homepage/interest.do


###  用户: 用户自己所有兴趣列表
*   path: /homepage/my-interest.do
*   param:
*	return:
   -	通用返回值 sports：运动； musics：音乐； lifes：生活； trips 旅行足迹 
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d  http://180.76.173.200:9999/homepage/my-interest.do



###  用户: 修改指定兴趣类型下兴趣列表
*   path: /homepage/modify-interest.do
*   param:
    -   interests（String） 修改后具体兴趣信息，多个以英文逗号隔开
    -   type(int) 兴趣类型：1 sports; 2 musics; 3 lifes; 4 trips 
*	return:
    -	通用返回值 
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d  http://180.76.173.200:9999/homepage/modify-interest.do
    -   

###  圈子:校验在当前分类下是否有相同名称的圈子
*   path: /circle/check-name.do
*   return:
    -   name（String） 待校验的名称
    -   tag(String)  一级分类
    -   sub_tag（String） 二级分类 
   -	通用返回值  0 不存在， 1 已经存在
*   example:
    -   curl -b cookie -d  http://180.76.173.200:9999/circle/check-name.do

###  圈子: 不通过校验直接加入圈子
*   path: /circle/free-insert.do
*   param:
   -	circleid(string) 圈子id
*	return:
   -	通用返回值  
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d 'circleid=[v]' http://180.76.173.200:9999/circle/free-insert.do

###  群聊: 转移群主
*   path: /chatroom/trans-chatroom
*   param:
   -  	chatroomid(string)  群聊id
   -	    userid（String） 转移用户id 
*	return:
   -	通用返回值  
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d 'chatroomid=[v]&userid=[v]' http://180.76.173.200:9999/chatroom/trans-chatroom.do
  

###  群聊: 修改聊天室昵称
*   path: /chatroom/update-name
*   param:
   -  	chatroomid(string)  群聊id
   -	    name（String） 要修的聊天室昵称 
*	return:
   -	通用返回值  
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d 'chatroomid=[v]&name=[v]' http://180.76.173.200:9999/chatroom/update-name.do

###  群聊: 修改聊天室公告
*   path: /chatroom/update-description
*   param:
   -  	chatroomid(string)  群聊id
   -	    description（String） 要修的公告信息
*	return:
   -	通用返回值  
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d 'chatroomid=[v]&description=[v]' http://180.76.173.200:9999/chatroom/update-description.do

###  群聊: 修改是否允许加入
*   path: /chatroom/update-open
*   param:
   -  	chatroomid(string)  群聊id
   -	    isOpen（boolean） true 允许，false 不允许 
*	return:
   -	通用返回值  
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d 'chatroomid=[v]&isOpen=[v]' http://180.76.173.200:9999/chatroom/update-open.do


###  群聊: 群聊加入是否需要验证
*   path: /chatroom/update-verify
*   param:
   -  	chatroomid(string)  群聊id
   -	    isVerify（boolean） true 需要， false 不需要 
*	return:	通用返回值  
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d 'chatroomid=[v]&isVerify=[v]' http://180.76.173.200:9999/chatroom/update-verify.do

###  群聊: 退出聊天室
*   path: /chatroom/quit
*   param:
   -  	chatroomid(string)  群聊id
*	return:
   -	通用返回值  
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d 'chatroomid=[v]' http://180.76.173.200:9999/chatroom/quit.do


###  群聊: 修改群聊中的昵称
*   path: /chatroom/update-nickname
*   param:
   -  	chatroomid(string)  群聊id
   -  	nickname（String）
*	return:
   -	通用返回值  
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d 'chatroomid=[v]&nickname=[v]' http://180.76.173.200:9999/chatroom/update-nickname.do

###  群聊: 获取群聊中的昵称
*   path: /chatroom/get-nicknames
*   param:
   -  	chatroomid(string)  群聊id
*	return:
   -	通用返回值  
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d 'chatroomid=[v]' http://180.76.173.200:9999/chatroom/get-nicknames.do


###  好友: 通讯录中已注册的好友信息
*   path: /friends/sign-users
*   param:
   -  	phones(string[])  通讯录中的电话数组
*	return:
   -	通用返回值  已进注册的好友userVos 
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d 'phones=[v]' http://180.76.173.200:9999/friends/sign-users.do

	
###  圈子: 获取圈子公告信息
*   path: /circle/get-notice.do
*   param:
   -	circleid(string) 圈子id
*	return:
   -	通用返回值 noticeTitle 公告标题；notice 公告内容； noticeTime 发布时间；  noticeUser 发布人员，若无该字段，则表示人员信息不存在  
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d 'circleid=[v]&title=[v]&content=[v]' http://180.76.173.200:9999/circle/get-notice.do
	

###  群聊: 修改群聊昵称显示
*   path: /chatroom/update-shownick
*   param:
   -  	chatroomid(string)  群聊id
   -  	isShowNick（boolean） true 显示昵称； false 不显示
*	return:
   -	通用返回值  
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d 'chatroomid=[v]&isShowNick=[v]' http://180.76.173.200:9999/chatroom/update-shownick.do


###  群聊: 修改聊天免打扰
*   path: /chatroom/update-disturb
*   param:
   -  	chatroomid(string)  群聊id
   -  	isDisturb（boolean） true 开启免打扰； false 关闭免打扰
*	return:
   -	通用返回值  
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d 'chatroomid=[v]&isDisturb=[v]' http://180.76.173.200:9999/chatroom/update-disturb.do


###  圈子: 邀请好友加入圈子
*   path: /circle/invite-user.do
*   param:
   -	circleid(string) 圈子id
   -    userids(string) 好友id,多个以逗号隔开
*	return:
   -	通用返回值   
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d 'circleid=[v]&userids=[v]' http://180.76.173.200:9999/circle/invite-user.do


###  圈子: 邀请好友列表
*   path: /circle/invite-friend-list.do
*   param:
   -	circleid(string) 准备邀请进入圈子的id
*	return:
   -	通用返回值 userVos  好友信息列表 
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d 'circleid=[v]' http://180.76.173.200:9999/circle/invite-friend-list.do


###  IM相关：得到全部聊天室,增量获取
*   path: /chatroom/my-chatrooms.do
*   param:
    -	timestamp(string) 时间戳，首次获取输入0，格式yyyy-MM-dd HH:mm:ss
*	return:
    -	通用返回值 ChatroomList timestamp最大时间戳。
*   example:
    -   curl -b cookie -d 'timestamp=[v]' http://180.76.173.200:9999/chatroom/my-chatrooms.do

	
###  好友: 通讯录中已注册的好友信息
*   path: /friends/sign-users-time
*   param:
    -  	phones(string[])  通讯录中的电话数组
    -	timestamp(string) 时间戳，首次获取输入0，格式yyyy-MM-dd HH:mm:ss
*	return:
    -	通用返回值  已进注册的好友userVos，timestamp最大时间戳
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d 'phones=[v]' http://180.76.173.200:9999/friends/sign-users-time.do	

	
###  圈子: 圈子内好友搜索
*   path: /circle/user-search
*   param:
    -  	circleid(string)  圈子id
    -	keyword(string) 搜索关键字
*	return:
    -	通用返回值  已进注册的好友userVos，timestamp最大时间戳
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d 'phones=[v]' http://180.76.173.200:9999/circle/user-search.do	
	

###  帖子: 圈子内置顶和加精帖子
*   path: /note/top-essence.do
*   param:
   -	circleid(string) 圈子id
   -	start_id(string)  
   -	limit(int)
*	return:
   -	通用返回值  noteVoList  essence：1表示加精，0表示未加精， top：1表示置顶， 0 表示未置顶
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d 'circleid=[v]&start_id=[v]&essence=[v]' http://180.76.173.200:9999/circle/top-essence.do
	
###  帖子: 帖子转发到我的动态
*   path: /note/forward-dynamic.do
*   param:
   -	noteid(string) 
*	return:
   -	通用返回值  dynamicid  动态信息id
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d 'circleid=[v]&start_id=[v]&essence=[v]' http://180.76.173.200:9999/circle/forward-dynamic.do	

	
###  圈子: 邀请加入圈子好友搜索
*   path: /circle/invite-user-search
*   param:
    -  	circleid(string)  圈子id
    -	keyword(string) 搜索关键字
*	return:
    -	通用返回值  已进注册的好友userVos，timestamp最大时间戳
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d 'circleid=[v]&keyword=[v]' http://180.76.173.200:9999/circle/invite-user-search.do	
	

###  圈子: 加入圈子
*   path: /circle/add-in-circle.do
*   param:
    -  	circleid(string)  圈子id
*	return:
    -	通用返回值  0 加入成功， -1  加入失败，需要跳转到验证流程
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d 'circleid=[v]' http://180.76.173.200:9999/circle/add-in-circle.do	

###  群聊: 二维码扫描进群
*   path: /chatroom/apply-insert.do
*   param:
   -  	chatroomid(string)  群聊id
*	return:
   -	通用返回值  0 加入成功， -1 加入失败，需要验证 
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d 'chatroomid=[v]&isDisturb=[v]' http://180.76.173.200:9999/chatroom/apply-insert.do

###  群聊: 加群验证信息提交
*   path: /chatroom/add-verify.do
*   param:
   -  	chatroomid(string)  群聊id
   -    reason(string)加群验证信息
*	return:
   -	通用返回值
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d 'chatroomid=[v]&isDisturb=[v]' http://180.76.173.200:9999/chatroom/add-verify.do

	
###  群聊: 加群验证信息列表
*   path: /chatroom/apply-list.do
*   param:
   -  	chatroomid(string)  群聊id
   -    page(int)
   -    limit(int)
*	return:
   -	通用返回值  userApplyVos  status表示状态，0 申请中， 1已同意， 2 已拒绝，-1 已过期
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d 'chatroomid=[v]&isDisturb=[v]' http://180.76.173.200:9999/chatroom/apply-list.do

	
###  群聊: 加群操作同意或拒绝
*   path: /chatroom/apply-operate.do
*   param:
   -  	chatroomid(string)  群聊id
   -    applyid(string) 申请信息id
   -    isAgree(boolean) 是否同意
   -    refues(string) 拒绝理由
*	return:
   -	通用返回值  
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d 'chatroomid=[v]&isDisturb=[v]' http://180.76.173.200:9999/chatroom/apply-operate.do
	
	
###  群聊: 加群操作同意或拒绝
*   path: /chatroom/get-friends-time.do
*   param:
   -  	timestamp(string) 时间戳
*	return:
   -	通用返回值  
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d 'timestamp=[v]' http://180.76.173.200:9999/chatroom/get-friends-time.do	


###  好友: 附近的好友
*   path: /friends/near-friends.do
*   param:
   -  	px(double) 经度
   -  	py(double) 纬度
*	return:
   -	通用返回值  friendVos  好友信息表  
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d http://180.76.173.200:9999/chatroom/friends/near-friends.do	

###  圈子: 圈子历史操作信息详情
*   path: /circle/get-circle-his.do
*   param:
   -  	historyid(string) id
*	return:
   -	通用返回值    
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d http://180.76.173.200:9999/circle/get-circle-his.do	

###  圈子: 我所有的圈子的操作信息列表
*   path: /circle/get-my-his.do
*   param:
   -  	page(int) 
   -  	limit(int)
*	return:
   -	通用返回值  historyVos  操作历史  
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d http://180.76.173.200:9999/circle/get-my-his.do

###  个人主页: 访问指定好友个人主页
*   path: /homepage/user-homepage.do
*   param:
   -  	page(int) 
   -  	limit(int)
   -  	userid（String） 用户id
*	return:
   -	通用返回值  userVo  用户信息， userCricles用户圈子信息默认4个  
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d http://180.76.173.200:9999/homepage/user-homepage.do

###  个人主页: 谁看过我
*   path: /homepage/visit-to-me.do
*   param:
   -  	page(int) 
   -  	limit(int)
*	return:
   -	通用返回值  userVisitVos  用户访问信息列表  
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d http://180.76.173.200:9999/homepage/visit-to-me.do

###  个人主页: 我看过谁
*   path: /homepage/visit-from-me.do
*   param:
   -  	page(int) 
   -  	limit(int)
*	return:
   -	通用返回值  userVisitVos  用户访问信息列表  
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d http://180.76.173.200:9999/homepage/visit-from-me.do


### 群聊窗口: 删除群聊窗口
*   path: /chatroom/delete-show.do
*   param:
   -  	chatroomid(string) 
*	return:
   -	通用返回值   
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d http://180.76.173.200:9999/chatroom/delete-show.do
	

#附录
## commentVo  
*   commentId(String)     评论id
*   content(String)       评论分类
*   parentid(String)      回复他人评论，其他人的评论id
*   parentUserName(String)回复他人评论，其他人的名称
*   parentUserid(String)  回复他人评论，其他人的id
*   userName(String)      评论的用户名称
*   userid(string)        评论的用户id
*   userSex(String)       评论的用户性别
*   userHeadPic(String)   评论的用户头像
*   userBirth(String)     评论的用户生日
*   createTime(String)    评论时间
*   thumpsubCount(long)   当前评论的点赞数量
*   isMyThumbsup(boolean) 当前用户是否对该条评论点赞


## chatroomVo  
*   id(String)     聊天室id
*   name(String)   聊天室名称
*   type(String)   聊天室类型
*   userid(String)  单人聊天用户id
*   friendid(String)  单人聊天朋友id
*   top(String)      是否置顶
*   description(string)  聊天室介绍或公告
*   isOpen(String)       聊天室是否允许加入
*   isVerify(String)     聊天室加入是否需要验证
*   userNum(String)     聊天室人数
*   userVos(String)     群聊用户信息
######   userVos:  群聊用户对象   
*   userid(String)   当前用户的id
*   username(String) 当前用户用户名称
*   userPic(String) 当前用户的头像
*   role(int) 0 普通用户， 2 群主

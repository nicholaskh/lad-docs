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
*   path: /feedback/insert.do
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
###  如果SEQ不存在，则创建面对面群聊，存在则加入；通过拉人的方式加入面对面群聊，请使用 chatroom/insert-user.do
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

###  标签:创建标签
*   path: /tag/set-tag.do
*   param:
   -    name(String) 标签名称
   -    friendsids(String) 使用英文逗号分隔的好友ID
*   return:
   -	通用返回值 
*   example:
    -   curl -b cookie -d 'name=[v]&friendsids=[v]' http://180.76.173.200:9999/tag/set-tag.do

###  标签:得到指定好友标签
*   path: /tag/get-friend-tag.do
*   param:
   -    friendid(String) 好友ID
*   return:
   -	通用返回值 tag 标签内容
*   example:
    -   curl -b cookie -d 'friendid=[v]' http://180.76.173.200:9999/tag/get-friend-tag.do

###  标签:得到全部好友标签列表
*   path: /tag/get-tag-list.do
*   param:
*   return:
   -	通用返回值 tag 标签内容
*   example:
    -   curl -b cookie http://180.76.173.200:9999/tag/get-friend-tag.do

###  标签:删除标签
*   path: /tag/delete-tag.do
*   param:
   -    tagid(String) 标签表ID
   -    frinedid(String) 朋友的ID
*   return:
   -	通用返回值
*   example:
    -   curl -b cookie -d 'tagid=[v]' http://180.76.173.200:9999/tag/delete-tag.do

###  标签:添加好友
*   path: /tag/tag-add-friends.do
*   param:
   -    tagid(String) 标签表ID
   -    friendsids(String) 使用英文逗号分隔的朋友ID
*   return:
   -	通用返回值
*   example:
    -   curl -b cookie -d 'tagid=[v]&friendsids=[v]'  http://180.76.173.200:9999/tag/tag-add-friends
 
 
###  标签:修改标签名称
*   path: /tag/update-tag-name.do
*   param:
   -    tagid(String) 标签表ID
   -    name(String) 标签名称
*   return:
   -	通用返回值
*   example:
    -   curl -b cookie -d 'tagid=[v]&name=[v]'  http://180.76.173.200:9999/tag/update-tag-name.do
 
 
###  标签:删除标签中的好友
*   path: /tag/cancel-friend-tag.do
*   param:
   -    tagid(String) 标签表ID
   -    friendsids(String) 使用英文逗号分隔的朋友ID
*   return:
   -	通用返回值
*   example:
    -   curl -b cookie -d 'tagid=[v]&friendsids=[v]'  http://180.76.173.200:9999/tag/cancel-friend-tag.do

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
   -    landmark(String)
   -    name(String)
   -    tag(String)
   -    sub_tag(String)
   -    category(String) 圈子类别，比如旅行、文学、美食……
   -    description(String) 简介
   -    isOpen(boolean) 是否5公里加入
   -    head_picture(file) 圈子头像
*   return:
   -	通用返回值
*   example:
    -   curl -b cookie -d 'px=[v]&py=[v]&landmark=[v]&name=[v]&tag=[v]&sub_tag=[v]&category=[v]' 
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
*   return:
   -	通用返回值
*   example:
    -   curl -b cookie -d 'circleid=[v]&reason=[v]'  http://180.76.173.200:9999/circle/apply-insert.do

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
    -   curl -b cookie -d 'userid=[v]&circleid=[v]'  http://180.76.173.200:9999/circle/delete-user.do
 
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
*	return:
   -	通用返回值 noteVoList： nodeid subject content visitCount访问量 commontCount 评论数 transCount转发数
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d 'circleid=[v]' http://180.76.173.200:9999/note/essential-note.do
	

### 帖子:圈子内置顶的 帖子
*   path: /note/top-notes.do
*   param:
   -	circleid(string)
*	return:
   -	通用返回值 noteVoList： nodeid subject content visitCount访问量 commontCount 评论数 transCount转发数
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d 'circleid=[v]' http://180.76.173.200:9999/note/top-notes.do
	

###  帖子:插入新的帖子
*   path: /note/insert.do
*   param:
   -    px(double)
   -    py(double)
   -    subject(String)
   -    landmark(String)
   -    content(String)
   -    circleid(String)
   -    pictures(files)图片或视频文件数组
   -    type(String) 上传文件类型
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
*   return:
   -	通用返回值 
*   example:
    -   curl -b cookie -F "commentid=[v]"  http://180.76.173.200:9999/note/comment-thumbsup.do
 


###  聊天：收藏聊天记录
*   path: /chat/collect-chat.do
*   param:
   -    title(String) 具体的聊天对象或群组名称 
   -    content(String)
*   return:
   -	通用返回值   col-time:聊天收藏时间 (yyyy-MM-dd HH:mm:ss) 
*   example:
    -   curl -b cookie -F "title=[v]&content=[v]" http://180.76.173.200:9999/chat/collect-chat.do
 
 
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
 
 
#附录
## commentVo  
*   commentId(String)     评论id
*   content(String)       评论分类
*   parentid(String)      回复他人评论，其他人的评论id
*   parentUserName(String)回复他人评论，其他人的名称
*   parentUserid(String)  回复他人评论，其他人的id
*   userName(String)      评论的用户名称
*   userid(string)        评论的用户id
*   createTime(String)    评论时间
*   thumpsubCount(long)   评论点赞数量
*   isMyThumbsup(boolean) 当前用户是否对该条评论点赞



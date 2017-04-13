User System APIs
================

###	Common
*   cookie
    -   sessionId: session相关ID
*	return: in json
	-	ret: 0成功，非0为error code
	-	error: 当ret!=0时，error为error message，否则error字段不存在
*   servers
    -   test: 180.76.173.200:9999
*   method
    -   约定：方法只读用get，增删改用post
    
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
	-	通用返回值
*   example:
    -   curl -c cookie/cookie路径 -d 'phone=1234&password=1' 'http://180.76.173.200:9999/login/login.do'
	
### 快速登录 获取验证码
*	path: /login/verification-send.do
*	params:
	-	phone(string): 密码
*	return: 
	-	通用返回值
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
    -   curl -b cookie -d 'username=haha' http://180.76.173.200:9999/personSet/username.do?
    
###    个人设置，设置生日
*   path: /person-set/birthday.do
*   param:
	-	birthday(string)
*	return:
	-	通用返回值
*   example:
    -   curl -b cookie -d 'birthday=haha' http://180.76.173.200:9999/person-set/birthday.do
    
###    个人设置，设置个性签名
*   path: /person-set/personalized-signature.do
*   param:
	-	personalized_signature(string)
*	return:
	-	通用返回值
*   example:
    -   curl -b cookie -d 'personalized_signature=haha' http://180.76.173.200:9999/person-set/personalized-signature.do

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
    
###    个人中心首页，信息插入
*   path: /message/insert.do
*   param:
	-	content(string)
*	return:
	-	通用返回值
*   example:
    -   curl -b  cookie  http://180.76.173.200:9999/message/insert.do
    
###    个人中心首页，点赞
*   path: /message/thumbsup.do
*   param:
	-	message_id(string)
*	return:
	-	通用返回值
*   example:
    -   curl -b  cookie  -d 'message_id=58ecaf0c589b557bced4bbba'  http://180.76.173.200:9999/message/thumbsup.do
    
###    个人中心首页，首页插入
*   path: /homepage/insert.do
*   param:
*	return:
	-	通用返回值
*   example:
    -   curl -b  cookie http://180.76.173.200:9999/message/insert.do
    
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
    -   curl -b  cookie http://180.76.173.200:9999/homepage/new_visitors-count.do
    
###    个人中心首页，我点赞的人
*   path: /homepage/thumbsup-from-me.do
*   param:
*   return:
	-    通用返回值
*   example:
    -   curl -b  cookie http://180.76.173.200:9999/message/thumbsup-from-me.do
    
    ###    个人中心首页，给我点赞的人
*   path: /homepage/thumbsup-to-me.do
*   param:
*   return:
	-    通用返回值
*   example:
    -   curl -b  cookie http://180.76.173.200:9999/message/thumbsup-to-me.do

    
###	退出登录
*   path: /logout
*	params:	无
*	return: 通用返回值


### 手机号码是否正确
*   path: /is-phone-right
*	param:
    -   phone(string)
	-	verification(string)
*	return: 通用返回值

### 意见反馈
*   path: /feedback-set
*   param:
	-	feedback(string)
	-	phone(string)
*   return: 通用返回值

### 绑定QQ
*   path: /qq-bind
*   param:
	-	qq(string)
*   return: 通用返回值


### 绑定微信
*   path: /wechat-bind
*   param:
	-   wechat(string)
*   return: 通用返回值


### 绑定微博
*   path: /microblog-bind
*   param:
	-	microblog(string)
*   return: 通用返回值


*   path: /thumbsup
*   param:
	-	person_from(string)
	-	person_to(string)
*   return: 通用返回值

### 好友动态
*   path: /friends-dynamic
*   param:
	-	person(string)
*	return:
	-	ret: 0成功，非0为error code,ret为数据信息
	-	error: 当ret!=0时，error为error message，否则error字段不存在

### 获得基本信息
*   path: /get-basicinfo
*   param:
	-	person(string)
*	return:
	-	ret: 0成功，非0为error code,ret为数据信息
	-	error: 当ret!=0时，error为error message，否则error字段不存在

###	获取企业信息
*   path: /about
*   return: 
    -	ret: 0成功，非0为error code
    -	info: 介绍的信息

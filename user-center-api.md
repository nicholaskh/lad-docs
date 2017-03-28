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
    
### 注册，发送验证码
*   path: /verification-send
*   param:
    -   phone(string)
*   return:
    -   通用返回值
*   example:
    -    curl -c /Users/gouxubo/cookies -d 'phone=123456' http://180.76.173.200:9999/regist/verification-send.do

### 注册，验证码是否正确
*   path: /is-verification-right
*   param:
    -   verification(string)
*   return: 通用返回值
*   example:
    -    curl -b cookie/cookie路径 -d 'verification=111111' http://180.76.173.200:9999/regist/is-verification-right.do?

###     注册设置密码
*   path: /password-set
*   param:
	-	password1(string)
	-	password2(string)
*	return:
	-	通用返回值
	-	成功后退出登录
*   example:
    -    curl -b cookie/cookie路径 -d 'password1=1&password2=1' http://180.76.173.200:9999/regist/password-set.do?

###	登录
*	path: /login
*	params:
	-	username(string): 用户名
	-	password(string): 密码
*	return: 
	-	通用返回值
*   example:
    -    curl -c cookie/cookie路径 -d 'phone=1234&password=1' http://127.0.0.1:8080/login/login.do?
	
### 快速登录 获取验证码
*	path: /verification_send
*	params:
	-	phone(string): 密码
*	return: 
	-	通用返回值
*   example:
    -    curl -c /Users/gouxubo/cookies -d 'phone=123456' http://180.76.173.200:9999/login/verification-send.do
	
###     快速登录
*	path: /login_quick
*	params:
	-	phone(string): 手机号码
	-	verification(string): 验证码
*	return: 
	-	通用返回值
*   example:
    -    curl -c /Users/gouxubo/cookies -d 'phone=1234&verification=111111' http://180.76.173.200:9999/login/login-quick.do

###	退出登录
*   path: /logout
*	params:	无
*	return: 通用返回值

### 注册
*	path: /register
*	param:
	-	username(string)
	-	verification(string)
	-	password(string)
*   return: 通用返回值
*   example:


### 账户安全
*	path: /accountsecurity-set
*	param:
    -	username(string)
	-	verification(string)
	-	password(string)
*	return: 通用返回值

### 手机号码是否正确
*   path: /is-phone-right
*	param:
    -   phone(string)
	-	verification(string)
*	return: 通用返回值

###	设置新密码
*   path: /password-set
*   param:
    -   old_password(string)
	-	password1(string)
	-	password2(string)
*	return:
	-	通用返回值
	-	成功后退出登录

### 修改密码，验证码是否正确
*   path: /is-verification-right
*   param:
    -   verification(string)
*   return: 通用返回值

### 修改密码，发送验证码
*   path: /verification-send
*   param:
    -   phone(string)
    -   verification(string)
*   return: 通用返回值

### 设置个人信息
*   path: /psersoninfo-set
*   param:
	-   pic_url(string)
	-	nickname(string)
	-	birthday(string)
	-	personalized_signature(string): 个性签名
*   return: 通用返回值

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

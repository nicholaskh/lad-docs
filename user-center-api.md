User System APIs
================

###	Common
*	return: in json
	-	ret: 0成功，非0为error code
	-	error: 当ret!=0时，error为error message，否则error字段不存在

### cookie，session机制说明
*    注册：注册成功后，接收到从服务端传来的{"session_id",[value]},保存在本地cookie下；
*    登陆：从cookie中取得key为"session_id"的值，拼装为{"session_id",[value]}，作为request的参数，传递到服务端，如果session_id为空则不附带此参数；如果接收到服务器端传来的session_id的值：{"session_id",[value]}，则将此值更新到本地cookie中；
*    页面跳转/请求转发：从cookie中取得key为"session_id"的值，拼装为{"session_id",[value]}，作为request的参数；如果从服务端收到{"error":[value]}，则跳转到登陆页面；其他情况下，正常跳转；
*    页面登出：直接跳转到登出页面；

###	登录
*	path: /login
*	params:
	-	username(string): 用户名
	-	password(string): 密码
*	return: 通用返回值

###	快捷登录
*	path: /login-quick
*	params:
	-	phone(string)
	-	password(string)
*	return: 通用返回值

###	登出
*   path: /loginout
*	params:
	-   username(string)
*	return: 通用返回值

### 注册
*	path: /register
*	param:
	-	username(string)
	-	verification(string)
	-	password(string)
*   return: 通用返回值

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

### 手机号码是否重复
*   path: /is-phone-repeat
*   param:
    -   phone(string)
	-	verification(string)
*       return: 通用返回值

###     设置新密码
*   path: /password-set
*   param:
    -   old_password(string)
	-	password1(string)
	-	password2(string)
*      return: 通用返回值

### 验证码是否正确
*   path: /is-verification-right
*   param:
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


*   path: /about
*   return: 
    -	ret: 0成功，非0为error code,ret为介绍的信息

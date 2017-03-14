User System APIs
================

###	Common
*	return: in json
	-	ret: 0成功，非0为error code
	-	error: 当ret!=0时，error为error message，否则error字段不存在
	
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
		

###     登出
*       path: /loginout
*	params:
	-       username(string)
*	return: 通用返回值


###     注册
*	path: /register
*	param:	
	-	username(string)
	-	verification(string)
	-	password(string)
*       return: 通用返回值

###     账户安全
*	path: /accountSecuritySet
*	param: 
        -	username(string)
	-	verification(string)
	-	password(string)
*	return: 通用返回值

###     手机号码是否正确
*       path: /isPhoneRight
*	param: 
        -       phone(string)
	-	verification(string)
*	return: 通用返回值

手机号码是否重复
---
		name: isPhoneRepeat
		return value: 成功返回：{ret: 0}; 失败返回：{ret: 1001，error: "该手机号码已存在"}
		param: String phone
		param: String verification

设置新密码
---
		name: passwordSet
		return value: 成功返回：{ret: 0}; 失败返回：{ret: 1001，error: "密码设置失败"}
		param: String oldPassword
		param: String password1
		param: String password2

验证码是否正确
---
		name: isVerificationRight
		return value: 成功返回：{ret: 0}; 失败返回：{ret: 1001，error: "验证码错误"}
		param: String verification

设置个人信息
---
		name: psersonInfoSet
		return value: 成功返回：{ret: 0}; 失败返回：{ret: 1001，error: "设置失败"}
		param: String picUrl
		param: String nickname
		param: String birthday
		param: String personalizedSignature

意见反馈
---
		name: feedbackSet
		return value: 成功返回：{ret: 0}; 失败返回：{ret: 1001，error: "设置失败"}
		param: String feedback;
		param: String phone;

绑定QQ
---
		name: QQBind
		return value: 成功返回：{ret: 0}; 失败返回：{ret: 1001，error: "设置失败"}
		param: String QQ

绑定微信
---
		name: WeChatBind
		return value: 成功返回：{ret: 0}; 失败返回：{ret: 1001，error: "设置失败"}
		param: String WeChat

绑定微博
---
		name: microblogBind
		return value: 成功返回：{ret: 0}; 失败返回：{ret: 1001，error: "设置失败"}
		param: String microblog

Give the thumbs-up点赞
-----
		name: thumbsup
		return value: 成功返回：{ret: 0}; 失败返回：{ret: 1001，error: "失败"}
		param: String personFrom
		param: String personTo

好友动态
----
		name:friendsDynamic
		return value:成功返回：{ret: [data]}; 失败返回：{ret: 1001，error: "失败"}
		param:String person

获得基本信息
----
		name:getBasicInfo
		return value:成功返回：{ret: [data]}; 失败返回：{ret: 1001，error: "失败"}
		param:String person

关于老友
----
		name:about
		return value:成功返回：{ret: data}; 失败返回：{ret: 1001，error: "失败"}





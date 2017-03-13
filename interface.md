登陆
---
		name: login
		return value: 成功返回：成功返回：{ret: 0}; 失败返回：{ret: 1001，error: "用户名或者密码不正确"}
		param: String username
		param: String password

快捷登陆
---
		name: loginQuick
		return value: 成功返回：成功返回：{ret: 0}; 失败返回：{ret: 1001，error: "用户名或者密码不正确"}
		param: String phone
		param: String password

登出
---
		name: loginout
		return value: 成功返回：成功返回：{ret: 0}; 失败返回：{ret: 1001，error: "用户名或者密码不正确"}
		param: String username

注册
---
		name: register
		return value: 成功返回：{ret: 0}; 失败返回：{ret: 1001，error: "用户名已存在"}
		param: String username
		param: String verification
		param: String password

账户安全
---
		name: accountSecuritySet
		return value: 成功返回：{ret: 0}; 失败返回：{ret: 1001，error: "设置失败"}
		param: String username
		param: String verification
		param: String password

手机号码是否正确
---
		name: isPhoneRight
		return value: 成功返回：{ret: 0}; 失败返回：{ret: 1001，error: "该手机号码不正确"}
		param: String phone
		param: String verification

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





Party APIs
================
#  发起聚会相关接口

##### 聚会参数信息 partyJson
    {
    "title": "聚会标题",
    "content": "聚会内容",
    "startTime": 聚会时间
     ["时间数组"],
    "addrType":  0 线上； 1 线下 int,
    "addrInfo": "具体聚会地点信息，线上必填",
    "landmark": "地理定位地点",
    "circleid": "圈子id",
    "payOrFree":  0  免费； 1收费 int,
    "payAmount": 活动费用金额 double,
    "payName": "活动费用名称",
    "payInfo": "收费费用信息",
    "appointment": 预约天数  int,
    "userLimit": 人数限制  int
    "phone": 是否需要填写手机号码， true 需要 false 不需要,
    "open":  是否允许非圈子人加入， true 是， false 不允许,
    "position":  具体聚会地点的经纬度 double数组
    [
        118.788343,
        32.029075
    ],
    "reminder": "聚会温馨提示",
    "status":  聚会的状态， 1 进行中，2 报名结束，-1 活动结束,
    }
    
### 聚会： 发起聚会
*   path: /party/create.do
*   param:
    -   partyJson(String) 聚会信息参数
    -   backPic(MultipartFile)  背景图片
	-   photos(MultipartFile[]) 聚会图片 
	-   video(MultipartFile)  聚会视频
*   return:
    -   通用返回值， partyid 聚会id
*   example:
    -   curl -c cookie/cookie路径 -d  'http://180.76.173.200:9999/party/create.do'
	
	
### 聚会： 修改聚会
*   path: /party/update.do
*   param:
	-   partyid(String) 聚会id
	-   partyJson(String) 聚会信息参数, 包括修改和未修改的；若任何参数未修改，可为空
    -   backPic(MultipartFile)  背景图片 可为空
	-   photos(MultipartFile[]) 新增的聚会图片  可为空
	-   delPhotos(String[])  删除的聚会图片  可为空 
	-   video(MultipartFile)  聚会视频  可为空
*   return:
    -   通用返回值， partyid 聚会id
*   example:
    -   curl -c cookie/cookie路径 -d  'http://180.76.173.200:9999/party/update.do'
	

### 聚会：聚会详情
*   path: /party/party-info.do
*   param:
    -   partyid(string) 聚会id
*   return:
    -   通用返回值， partyVo
*   example:
    -   curl -c cookie/cookie路径 -d 'http://180.76.173.200:9999/party/party-info.do'	

	
###  圈子:通过聚会申请加入圈子，需要验证的圈子才需要调用此接口，自由加入的不通过这种方式
*   path: /circle/party-apply-insert.do
*   param:
   -    circleid(String)
   -    reason(String) 申请理由
   -    isNotice(boolean) 是否通知好友
   -    addType(int) 加入类型，通过聚会加入 为 1， 正常为0
   -    partyid(string) 聚会id
*   return:
   -	通用返回值
*   example:
    -   curl -b cookie -d 'circleid=[v]&reason=[v]&isNotice=[v]&addType=[v]&partyid=[v]  http://180.76.173.200:9999/circle/party-apply-insert.do


### 聚会：报名聚会
*   path: /party/enroll-party.do
*   param:
    -   partyid(string) 聚会id
    -   phone(String) 报名聚会电话
    -   joinInfo(String) 报名聚会描述
    -   userNum(int) 报名人数
    -   amount(double)报名金额
*   return:
    -   通用返回值
*   example:
    -   curl -c cookie/cookie路径 -d   'http://180.76.173.200:9999/party/enroll-party.do'


### 聚会：获取聚会报名人数
*   path: /party/get-users.do
*   param:
    -   partyid(string) 聚会id
*   return:
    -   通用返回值， partyUserVo
*   example:
    -   curl -c cookie/cookie路径 -d 'http://180.76.173.200:9999/party/get-users.do'	  


### 聚会：我发起的聚会
*   path: /party/my-partys.do
*   param:
    -   page(int) 分页页码
    -   limit(int) 每页展示条数
*   return:
    -   通用返回值， partyListVos  这个是从partyVo获取的部分参数
*   example:
    -   curl -c cookie/cookie路径 -d 
    -   curl -b  /Users/gouxubo/cookiel -d 'page=[1]&limit=[10]' 'http://180.76.173.200:9999/party/my-partys.do'	
    	
	
### 聚会：我参与的聚会
*   path: /party/join-partys.do
*   param:
    -   page(int) 分页页码
    -   limit(int) 每页展示条数
*   return:
    -   通用返回值， partyListVos  这个是从partyVo获取的部分参数
*   example:
    -   curl -c cookie/cookie路径 -d 
    -   curl -b  /Users/gouxubo/cookiel -d 'page=[1]&limit=[10]' 'http://180.76.173.200:9999/party/join-partys.do'
    
	
### 聚会：发起群聊
*   path: /party/launch-talk.do
*   param:
    -   partyid(String) 聚会id
*   return:
    -   通用返回值
*   example:
    -   curl -c cookie/cookie路径 -d 
    -   curl -b  /Users/gouxubo/cookiel -d 'partyid=[v]' 'http://180.76.173.200:9999/party/launch-talk.do'	

	
### 聚会：判断是否已经发起了群聊
*   path: /party/has-chatroom.do
*   param:
    -   partyid(String) 聚会id
*   return:
    -   通用返回值 chatroomid 为空表示尚未发起群聊
*   example:
    -   curl -c cookie/cookie路径 -d 
    -   curl -b  /Users/gouxubo/cookiel -d 'partyid=[v]' 'http://180.76.173.200:9999/party/has-chatroom.do'


### 聚会：收藏聚会
*   path: /party/collect-party.do
*   param:
    -   partyid(String) 聚会id
*   return:
    -   通用返回值 
*   example:
    -   curl -c cookie/cookie路径 -d 
    -   curl -b  /Users/gouxubo/cookiel -d 'partyid=[v]' 'http://180.76.173.200:9999/party/del-collect.do'

	
### 聚会：取消已收藏的聚会
*   path: /party/del-collect.do
*   param:
    -   partyid(String) 聚会id
*   return:
    -   通用返回值 col-time 收藏时间
*   example:
    -   curl -c cookie/cookie路径 -d 
    -   curl -b  /Users/gouxubo/cookiel -d 'partyid=[v]' 'http://180.76.173.200:9999/party/collect-party.do'

### 聚会：删除聚会
*   path: /party/delete-party.do
*   param:
    -   partyid(String) 聚会id
*   return:
    -   通用返回值 
*   example:
    -   curl -c cookie/cookie路径 -d 
    -   curl -b  /Users/gouxubo/cookiel -d 'partyid=[v]' 'http://180.76.173.200:9999/party/collect-party.do'


### 聚会：评论聚会
*   path: /party/add-comment.do
*   param:
    -   partyComment(String) 聚会评论信息json格式，包括 partyid（聚会id）， content(String) 评论内容，isSync(boolean) 是否同步到个人动态， parentid 回复评论的id ，如果不是回复评论，直接回复聚会，设置为空
    -   photos(MultipartFile[]) 图片 
*   return:
    -   通用返回值  commentVos  其中parentUserName，parentUser表示当前回复那条评论的用户名和id，类似微信评论 
*   example:
    -   curl -c cookie/cookie路径 -d 
    -   curl -b  /Users/gouxubo/cookiel -d  'http://180.76.173.200:9999/party/add-comment.do'


### 聚会：获取聚会评论
*   path: /party/get-comments.do
*   param:
    -   partyid(String) 聚会id
*   return:
    -   通用返回值 commentVo
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d   'partyid=[v]' 'http://180.76.173.200:9999/party/get-comments.do'
	

### 聚会：获取圈子内所有聚会
*   path: /party/all-partys.do
*   param:
    -   circleid(String) 圈子id
	-   page(int) 
	-   limit(int) 
*   return:
    -   通用返回值 partyListVos
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d   'circleid=[v]&page=[v]&limit=[v]' http://180.76.173.200:9999/party/all-partys.do	

	
### 聚会：取消报名
*   path: /party/cancel-enroll.do
*   param:
    -   partyid(String) 聚会id
*   return:
    -   通用返回值 
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d   'partyid=[v]' http://180.76.173.200:9999/party/cancel-enroll.do

	
### 聚会：删除我报名的聚会
*   path: /party/delete-join-party.do
*   param:
    -   partyid(String) 聚会id
*   return:
    -   通用返回值 
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d   'partyid=' http://180.76.173.200:9999/party/delete-join-party.do

	
### 聚会：聚会报名详情
*   path: /party/enroll-detail.do
*   param:
    -   partyid(String) 聚会id
	-   userid(String) 报名用户id
*   return:
    -   通用返回值  partyUser
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d   'partyid=[v]&userid=[v]' http://180.76.173.200:9999/party/enroll-detail.do

	
### 聚会：聚会评论点赞或取消点赞
*   path: /party/comment-thumbsup.do
*   param:
    -   commentId(String) 评论id
	-   type(int) 0 点赞， 1 取消点赞
*   return:
    -   通用返回值 
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d   'commentId=[v]&type=[v]' http://180.76.173.200:9999/party/comment-thumbsup.do
	
### 聚会：聚会临时聊天创建
*   path: /party/temp-chatroom.do
*   param:
    -   partyid(string) 聚会id
	-   friendid(string) 创建临时聊天用户id
*   return:
    -   通用返回值  channelId 临时聊天室id
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d   'partyid=[v]&friendid=[v]' http://180.76.173.200:9999/party/temp-chatroom.do


### 聚会：聚会通知发布
*   path: /party/send-notice.do
*   param:
    -   partyid(string) 聚会id
	-   content(string) 通知内容
*   return:
    -   通用返回值 
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d   'partyid=[v]&content=[v]' http://180.76.173.200:9999/party/send-notice.do


### 聚会：聚会通知详情
*   path: /party/notice.do
*   param:
    -   noticeid(string) 聚会id
*   return:
    -   通用返回值  noticeVo  id即为noticeid
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d   'partyid=[v]' http://180.76.173.200:9999/party/notice.do


### 聚会：聚会通知列表
*   path: /party/party-notice.do
*   param:
    -   partyid(string) 聚会id
	-   page(string) 页码
	-   limit(int) 每页条数
*   return:
    -   通用返回值  noticeVos id即为noticeid
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d   'partyid=[v]&page=[v]&limit=[v]' http://180.76.173.200:9999/party/party-notice.do


### 聚会：我收到的聚会通知列表
*   path: /party/get-my-notices.do
*   param:
	-   page(string) 页码
	-   limit(int) 每页条数
*   return:
    -   通用返回值  channelId 临时聊天室id
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d   'page=[v]&limit=[v]' http://180.76.173.200:9999/party/get-my-notices.do
	
#附录
## partyVo  
*   partyid(String)     聚会id
*   title(String)       聚会标题
*   startTime（数组）: 聚会时间
*   addrType（int）:  0 线上； 1 线下
*   addrInfo(String): "具体聚会地点信息，线上必填",
*   landmark(String): "地理定位地点",
*   circleid(String): "聚会所在圈子id",
*   payOrFree(String):  0  免费； 1收费,
*   payAmount(double): 活动费用金额,
*   payName（String）: "活动费用名称",
*   payInfo(String): "收费费用信息",
*   appointment(int): 预约天数,
*   userLimit(int): 人数限制
*   phone(boolean): 是否需要填写手机号码， true 需要 false 不需要,
*   open(boolean):  是否允许非圈子人加入， true 是， false 不允许,
*   position(数组):  具体聚会地点的经纬度
*   reminder(String): "聚会温馨提示",
*   status(int):  聚会的状态， 1 进行中，2 报名结束，-1 活动结束
*   creater(partyUserVo) 聚会创建者信息
*   create(boolean) 当前用户是不是聚会创建者
*   users(partyUserVo) 聚会参与者信息
*   inCircle(boolean)  当前用户是不是已加入聚会所在圈子
*   inParty(boolean)  当前用户是不是已加入聚会
*   isComment(boolean) 当前用户是否已经评论
*   isCollect(boolean) 当前用户是否收藏聚会
*   backPic(String)  聚会背景图片
*   photos(String[]) 聚会图片信息
*   video(String)   聚会视频
*   videoPic(String)  聚会视频缩略图
*   chatroomid(String) 聚会群聊id，若为空，表示尚未建立群聊
*   circlePic(String)  聚会所在圈子图片
*   circleName(String) 聚会所在圈子名称
*   userNum(int)  聚会已报名数量
*   visitNum(int) 聚会阅读数量
*   shareNum(int) 聚会分享数量
*   collectNum(int)  聚会收藏数量
*   reportNum(int)  聚会举报数量
######   partyUserVo:  聚会用户对象信息   
*   userid(String)   当前用户id
*   username(String) 当前用户昵称
*   userPic(String) 当前用户头像


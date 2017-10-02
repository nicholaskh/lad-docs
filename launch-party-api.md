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
    "status":  聚会的状态， 0 进行中，1 报名结束，2 活动结束  3 已取消 ,
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
	

### 聚会：聚会详情
*   path: /party/party-info.do
*   param:
    -   partyid(string) 聚会id
*   return:
    -   通用返回值， partyVo
*   example:
    -   curl -c cookie/cookie路径 -d 'http://180.76.173.200:9999/party/party-info.do'	



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
*   status(int):  聚会的状态， 0 进行中，1 报名结束，2 活动结束  3 已取消 ,
*   creater(partyUserVo) 聚会创建者信息
*   create(boolean) 当前用户是不是聚会创建者
*   users(partyUserVo) 聚会参与者信息
*   inCircle(boolean)  当前用户是不是已加入聚会所在圈子
*   inParty(boolean)  当前用户是不是已加入聚会
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

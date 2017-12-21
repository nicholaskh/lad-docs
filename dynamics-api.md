User System APIs
================
#  动态信息相关接口

###  dynamicVo
*   msgid(String)    动态信息id
*   title(String)    动态信息标题
*   photos(String)   动态图片
*   content(String)  内容
*   transNum(int)    转发数量
*   commentNum(int)  评论数量
*   thumpNum(int)      点赞数量
*   userid(String)      当前动态信息发布人员
*   userPic(String)     当前动态信息人的头像
*   landmark(long)      发布数动态时地址地理位置展示
*   isMyThumbsup(boolean)  我是否对当前动态点赞
*   type(int)   动态类型 0 帖子，1 资讯，3 圈子， 4 聚会， 5 纯动态
*   sourceid(string)   动态id,如帖子id，圈子id， 资讯id等 
*   owner(string)    动态信息来源作者
*   view(string)  转发或评论的说明
*   postion(double[])  经纬度
*   videoPic(string)  视频缩略图
*   video(string) 视频url
*   circleid(string)  帖子的圈子
*   circleName(string)  帖子的圈子名称
*   time(date)  动态发布时间




    
### 动态：发布动态信息
*   path: /dynamic/insert.do
*   param:
   -    px(double)  
   -    py(double)
   -    title(String) 标题
   -    content(String) 内容
   -    landmark(String) 发布时是否展示定位信息
   -    pictures(String) 图片或视频
   -    type   图片或视频类型分类  video 和 pic
*   return:
    -   通用返回值， dynamicid 
*   example:
    -   curl -c cookie/cookie路径 -d  'http://180.76.173.200:9999/dynamic/insert.do'
	

### 动态：获取所有好友的动态信息列表
*   path: /dynamic/all-dynamics.do
*   param:
    -   page(int)  当前页数 从1开始
	-   limit(int)  每页展示条数 
*   return:
    -   通用返回值， dynamicVos
*   example:
    -   curl -c cookie/cookie路径 -d 'page=[v]&limit=[v]'  'http://180.76.173.200:9999/dynamic/all-dynamics.do'	


### 动态：获取所有好友的动态数量
*   path: /dynamic/all-dynamics-num.do
*   param:
*   return:
    -   通用返回值， dynamicNum
*   example:
    -   curl -c cookie/cookie路径 -d   'http://180.76.173.200:9999/dynamic/all-dynamics-num.do'	
	
	
### 动态：获取指定好友的动态信息列表
*   path: /dynamic/friend-dynamics.do
*   param:
    -   friendid(String) 好友id
    -   page(int)  当前页数 从1开始
	-   limit(int)  每页展示条数 
*   return:
    -   通用返回值， dynamicVos  backPic 背景图， headPic 个人头像， signature 个性签名， showUser
*   example:
    -   curl -c cookie/cookie路径 -d 'friendid=[v]&page=[v]&limit=[v]'  'http://180.76.173.200:9999/dynamic/friend-dynamics.do'	


### 动态：获取指定好友的动态数量
*   path: /dynamic/one-dynamics-num.do
*   param:
    -   friendid(String) 好友id
*   return:
    -   通用返回值， dynamicNum
*   example:
    -   curl -c cookie/cookie路径 -d 'friendid=[v]'  'http://180.76.173.200:9999/dynamic/one-dynamics-num.do'		


### 动态：获取自己动态信息列表
*   path: /dynamic/my-dynamics.do
*   param:
    -   page(int)  当前页数 从1开始
	-   limit(int)  每页展示条数 
*   return:
    -   通用返回值， dynamicVos， backPic 背景图， headPic 个人头像， signature 个性签名， showUser 展示最后访问的用户
*   example:
    -   curl -c cookie/cookie路径 -d 'page=[v]&limit=[v]'  'http://180.76.173.200:9999/dynamic/my-dynamics.do'	


### 动态：获取自己的动态数量
*   path: /dynamic/my-dynamics-num.do
*   param:
*   return:
    -   通用返回值， dynamicNum
*   example:
    -   curl -c cookie/cookie路径 -d   'http://180.76.173.200:9999/dynamic/my-dynamics-num.do'
		
### 动态：动态信息详情
*   path: /dynamic/dynamic-detail.do
*   param:
    -   msgid(String)  动态信息id
*   return:
    -   通用返回值， noteVo 帖子详情  dynamicVo 动态详情， partyVo聚会详情
*   example:
    -   curl -c cookie/cookie路径 -d 'msgid=[v]'   'http://180.76.173.200:9999/dynamic/dynamic-detail.do'

### 动态：不看他的动态信息
*   path: /dynamic/dynamic-not-see.do
*   param:
    -   friendid(String)  不看信息的好友id
*   return:
    -   通用返回值
*   example:
    -   curl -c cookie/cookie路径 -d 'friendid=[v]'   'http://180.76.173.200:9999/dynamic/dynamic-not-see.do'

### 动态：转发帖子到我的动态
*   path: /note/forward-dynamic.do
*   param:
   -    noteid(String) 帖子id
   -    view(String) 转发时说明信息
*   return:
    -   通用返回值， dynamicid 
*   example:
    -   curl -c cookie/cookie路径 -d  'http://180.76.173.200:9999/note/forward-dynamic.do' 

### 动态：转发圈子到我的动态信息
*   path: /circle/forward-dynamic.do
*   param:
   -    circleid(String) 圈子id
   -    view(String) 转发时说明信息
*   return:
    -   通用返回值， dynamicid 
*   example:
    -   curl -c cookie/cookie路径 -d  'http://180.76.173.200:9999/circle/forward-dynamic.do' 

### 动态：转发资讯到我的动态信息
*   path: /infor/forward-dynamic.do
*   param:
   -    inforid(String) 圈子id
   -    inforType(int) 资讯类型， 1健康， 2安防， 3 广播， 4视频
   -    view(String) 转发时说明信息
*   return:
    -   通用返回值， dynamicid 
*   example:
    -   curl -c cookie/cookie路径 -d  'http://180.76.173.200:9999/infor/forward-dynamic.do' 

### 动态：转发动态到我的动态信息
*   path: /party/forward-dynamic.do
*   param:
   -    partyid(String) 圈子id
   -    view(String) 转发时说明信息
*   return:
    -   通用返回值， dynamicid 
*   example:
    -   curl -c cookie/cookie路径 -d  'http://180.76.173.200:9999/party/forward-dynamic.do' 

### 动态：谁看过我的动态
*   path: /dynamic/visit-my-dynamic.do
*   param:
   -    page(int) 页数
   -    limit(int) 每页条数
*   return:
    -   通用返回值， visitUserVos 
*   example:
    -   curl -c cookie/cookie路径 -d  'http://180.76.173.200:9999/dynamic/visit-my-dynamic.do'

### 动态：更新动态的背景图片
*   path: /dynamic/update-backpic.do
*   param:
   -    backPic(MultipartFile) 图片
*   return:
    -   通用返回值
*   example:
    -   curl -c cookie/cookie路径 -d  'http://180.76.173.200:9999/dynamic/update-backpic.do'
User System APIs
================
#  动态信息相关接口

###  dynamicVo
*   msgid(String)    动态信息主键
*   title(String)    动态信息标题
*   photos(String)   动态图片
*   content(String)  内容
*   transNum(String)    转发数量
*   commentNum(String)  评论数量
*   thumpNum(list)      点赞数量
*   userid(String)      当前动态信息发布人员
*   userPic(String)     当前动态信息人的头像
*   landmark(long)      发布数动态时地址地理位置展示
*   isMyThumbsup(boolean)  我是否对当前动态点赞




    
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
    -   curl -c cookie/cookie路径 -d  'http://180.76.173.200:9999/infor/dynamic/insert.do'
	

### 动态：获取所有好友的动态信息列表
*   path: /dynamic/all-dynamics.do
*   param:
    -   page(int)  当前页数 从1开始
	-   limit(int)  每页展示条数 
*   return:
    -   通用返回值， dynamicVos
*   example:
    -   curl -c cookie/cookie路径 -d 'page=[v]&limit=[v]'  'http://180.76.173.200:9999/infor/all-dynamics.do'	


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
    -   通用返回值， dynamicVos
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
    -   通用返回值， dynamicVos
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
   

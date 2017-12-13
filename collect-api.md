User System APIs
================
#  收藏相关接口

###  collectVo
*   collectid(String)    收藏信息id
*   content(String)      收藏内容，表示非链接类型的文本内容
*   title(String)        标题
*   path(String)         路径
*   type(int)            收藏类型 1 图片， 2 音乐， 3 视频， 4语音， 5链接 url类或者文件链接
*   sub_type(int)        收藏子类型， 0帖子， 1 资讯， 2 网页 ， 3 待定 ， 4 聚会
*   targetid(string)     收藏内容源id
*   source(String)       收藏内容来源的如圈子 资讯分类名称等
*   sourceType(int)      收藏来源类型，资讯类型来源分类，1 健康， 2安防， 3 广播， 4 视频， 5 圈子
*   userTags(array)      收藏标签
*   collectTime(time)    收藏时间



    
### 收藏：收藏帖子
*   path: /note/col-note.do
*   param:
   -    noteid(string)  
*   return:
    -   通用返回值， col-time 收藏时间 (yyyy-MM-dd HH:mm:ss)
*   example:
    -   curl -c cookie/cookie路径 -d  'http://180.76.173.200:9999/note/col-note.do'


### 收藏：收藏聚会
*   path: /party/collect-party.do
*   param:
    -   partyid(String) 聚会id
*   return:
    -   通用返回值 col-time 收藏时间 (yyyy-MM-dd HH:mm:ss)
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d 'partyid=[v]' 'http://180.76.173.200:9999/party/collect-party.do'


### 收藏：收藏资讯
*   path: /infor/collect-infor.do
*   param:
    -   inforid(String) 资讯id
    -   inforType(int) 资讯类型，1 健康， 2安防， 3 广播， 4 视频
*   return:
    -   通用返回值 col-time 收藏时间 (yyyy-MM-dd HH:mm:ss)
*   example:
    -   curl -b  /Users/gouxubo/cookiel -d 'inforid=[v]' 'http://180.76.173.200:9999/party/collect-infor.do'


### 收藏：添加收藏的标签
*   path: /collect/add-tag.do
*   param:
   -    name(string)  
*   return:
    -   通用返回值， 
*   example:
    -   curl -c cookie/cookie路径 -d  'http://180.76.173.200:9999/collect/add-tag.do'


### 收藏：我的收藏标签
*   path: /collect/my-tags.do
*   param: 
*   return:
    -   通用返回值，tags 
*   example:
    -   curl -c cookie/cookie路径 -d  'http://180.76.173.200:9999/collect/my-tagsg.do'


### 收藏：我的所有收藏
*   path: /collect/my-collects.do
*   param:
   -    page(int)
   -    limit(int)  
*   return:
    -   通用返回值，collectVos 
*   example:
    -   curl -c cookie/cookie路径 -d  'http://180.76.173.200:9999/collect/my-collects.do'


###  聊天：收藏聊天记录
*   path: /collect/chat.do
*   param:
   -    title(String) 具体的聊天对象或群组名称 
   -    content(String)
*   return:
   -	通用返回值   col-time:聊天收藏时间 (yyyy-MM-dd HH:mm:ss) 
*   example:
    -   curl -b cookie -F "title=[v]&content=[v]" http://180.76.173.200:9999/chat/collect/chat.do


###  聊天：获取收藏的聊天记录
*   path: /collect/my-chats.do
*   param:
   -    start_id(String) 分页时最后起始的收藏聊天记录的id，为空则表示从最新一条开发
   -    limit(int) 每页显示条数
*   return:
   -	通用返回值   col-chats 收藏聊天 
*   example:
    -   curl -b cookie -F "start_id=[v]&limit=[v]" http://180.76.173.200:9999/chat/collect/my-chats.do
	

###  聊天：收藏文件类型，包括图片、视频、语音等等
*   path: /collect/col-files.do
*   param:
   -    path(String) 收藏源文件的url 
   -    fileType(int) 类型，1 图片， 2 音乐， 3 视频， 4语音， 5链接 url类或者文件链接
*   return:
   -	通用返回值   col-time:聊天收藏时间 (yyyy-MM-dd HH:mm:ss) 
*   example:
    -   curl -b cookie -F "path=[v]&fileType=[v]" http://180.76.173.200:9999/chat/collect/col-files.do


### 收藏：根据标题关键字或者收藏分类名称查找
*   path: /collect/by-tagName.do
*   param:
*   -   tagName（string）分类名称或关键字
    -   page(int)
    -   limit(int)  
*   return:
    -   通用返回值，collectVos 
*   example:
    -   curl -c cookie/cookie路径 -d  "tagName=[v]&page=[v]&limit=[v]" 'http://180.76.173.200:9999/collect/by-tagName.do'

### 收藏：根据收藏类型查找
*   path: /collect/by-type.do
*   param:
*   -   type（int）类型，1 图片， 2 音乐， 3 视频， 4语音， 5链接 url类或者文件链接
    -   page(int)
    -   limit(int)  
*   return:
    -   通用返回值，collectVos 
*   example:
    -   curl -c cookie/cookie路径 -d  "type=[v]&page=[v]&limit=[v]" 'http://180.76.173.200:9999/collect/by-type.do'
   
### 收藏：给收藏添加标签
*   path: /collect/add-col-tag.do
*   param:
*   -   tags（string）多个以逗号隔开
    -   collectid(string) 收藏id
*   return:
    -   通用返回值，collectVos 
*   example:
    -   curl -c cookie/cookie路径 -d  "tags=[v]&collectid=[v]" 'http://180.76.173.200:9999/collect/add-col-tag.do'
User System APIs
================
#  资讯相关接口

### 健康养生 inforVo
*   inforid(String)   资讯主键
*   module(String)    资讯大分类
*   className(String) 资讯小分类
*   title(String)     资讯题目
*   source(String)    资讯来源
*   sourceUrl(String) 资讯来源url
*   imageUrls(list)   资讯图片url
*   time(String)      资讯发表时间
*   text(String)      资讯内容
*   readNum(long)     资讯阅读数量
*   thumpsubNum(long) 资讯点赞数量
*   selfSub(boolean)  资讯是否被当前用户点赞


### 安防 securityVo
*   inforid(String)   安防资讯主键
*   newsType(String)  安防资讯分类
*   title(String)     安防资讯题目
*   time(String)      安防资讯发表时间
*   text(String)      安防资讯内容
*   city(String)      安防资讯来源城市
*   readNum(long)     安防资讯阅读数量
*   thumpsubNum(long) 安防资讯点赞数量
*   selfSub(boolean)  安防资讯是否被当前用户点赞


    
### 资讯：获资讯下所有分类， 若用户已订阅分类，则返回已订阅的分类
*   path: /infor/group-types.do
*   param:
*   return:
    -   通用返回值， healthTypes 健康资讯数组， securityTypes 安全资讯分类数组
*   example:
    -   curl -c cookie/cookie路径 -d  'http://180.76.173.200:9999/infor/group-types.do'
	

### 资讯：获取健康养生下指定分类下的健康资讯列表信息
*   path: /infor/group-infors.do
*   param:
    -   groupName(string)
	-   inforTime(string) 分页最后一条咨询的时间，因为爬虫抓取的资讯中主键和时间没有关联关系，故使用时间
	-   limit(int)  每页展示资讯数量
*   return:
    -   通用返回值， infoVoList
*   example:
    -   curl -c cookie/cookie路径 -d 'groupName=[v]&inforTime=[v]&limit=[v]'  'http://180.76.173.200:9999/infor/group-infors.do'	


### 资讯：我的频道推荐健康资讯初始信息
*   path: /infor/recommend-groups.do
*   param:
    -   type(int) 1 健康，2 安防，3 广播，4 视频
*   return:
    -   通用返回值， mySubTypes 已订阅的分类， recoTypes 推荐的分类（未订阅） 
*   example:
    -   curl -c cookie/cookie路径 -d 'type=[v]'  'http://180.76.173.200:9999/infor/recommend-groups.do'	
	
	
### 资讯：我的频道推荐健康资讯分类修改
*   path: /infor/update-groups.do
*   param:
    -   groupNames(string) 订阅的分类,多个以逗号隔开
	-   type(int) 1 健康，2 安防，3 广播，4 视频
*   return:
    -   通用返回值
*   example:
    -   curl -c cookie/cookie路径 -d  'groupNames=[v]&type=[v]'  'http://180.76.173.200:9999/infor/update-groups.do'		

		
### 资讯：资讯详情
*   path: /infor/news-infor.do
*   param:
    -   inforid(string)
*   return:
    -   通用返回值， inforVo
*   example:
    -   curl -c cookie/cookie路径 -d   'inforid=[v]'  'http://180.76.173.200:9999/infor/news-infor.do'	
   

### 资讯：获取安防信息指定分类下的资讯列表信息
*   path: /infor/security-list.do
*   param:
    -   newsType(string) 安防资讯分类名称
	-   inforTime(string) 分页最后一条咨询的时间，因为爬虫抓取的资讯中主键和时间没有关联关系，故使用时间
	-   limit(int)  每页展示资讯数量
*   return:
    -   通用返回值， securityVoList
*   example:
    -   curl -c cookie/cookie路径 -d 'newsType=[v]&inforTime=[v]&limit=[v]'  'http://180.76.173.200:9999/infor/security-list.doo'	

### 资讯：安防资讯详情
*   path: /infor/security-infor.do
*   param:
    -   inforid(string)
*   return:
    -   通用返回值， securityVo
*   example:
    -   curl -c cookie/cookie路径 -d   'inforid=[v]'  'http://180.76.173.200:9999/infor/security-infor.do'	
	
### 资讯：评论资讯
*   path: /infor/add-comment.do
*   param:
    -   inforid(string)  资讯id
    -   countent(String) 评论内容
    -   parentid(String) 如回复其他人评论则必须输入，其他人评论的id
	-   inforType(int)资讯类型   1 健康，2 安防，3 广播，4 视频
*   return:
    -   通用返回值， commentVo
*   example:
    -   curl -c cookie/cookie路径 -d    'inforid=[v]&countent=[v]&parentid=[v]'   'http://180.76.173.200:9999/infor/add-comment.do'	
	
	
### 资讯：获取当前资讯的评论
*   path: /infor/get-comments.do
*   param:
   -    inforid(String)
   -	    start_id(string)
   -	    gt(boolean)
   -	    limit(int)
*   return:
   -	通用返回值 commentVoList
*   example:
    -   curl -b cookie -F "inforid=[v]&start_id=[v]&gt=[v]&limit=[v]"  http://180.76.173.200:9999/infor/get-comments.do

 
### 资讯：资讯或评论点赞
*   path: /infor/thumbsup.do
*   param:
    -   targetid(String)  资讯或评论id
    -	type(int) 0表示资讯，1表示评论
   	-   inforType(int)资讯类型   1 健康，2 安防，3 广播，4 视频
*   return:
    -	通用返回值 
*   example:
    -   curl -b cookie -F "targetid=[v]&type=[v]&inforType=[v]"  http://180.76.173.200:9999/infor/thumbsup.do
 
### 资讯：取消点赞
*   path: /infor/cancal-thumbsup.do
*   param:
    -    targetid(String)  资讯或评论id
    -  	type(int) 0表示资讯，1表示评论
    -   inforType(int)资讯类型   1 健康，2 安防，3 广播，4 视频
*   return:
    -	通用返回值 
*   example:
    -   curl -b cookie -F "targetid=[v]&type=[v]&inforType=[v]"  http://180.76.173.200:9999/infor/cancal-thumbsup.do

### 资讯：获取广播列表
*   path: /infor/radio-list.do
*   param:
   -    module(String)  分类
   -	page(int) 页码，从1开始
   -	limit(int)
*   return:
   -	通用返回值 
*   example:
    -   curl -b cookie -F "module=[v]&page=[v]&limit=[v]"  http://180.76.173.200:9999/infor/radio-list.do


### 资讯：获取广播详情
*   path: /infor/radio-infor.do
*   param:
   -    radioid(String)  分类
*   return:
   -	通用返回值 
*   example:
    -   curl -b cookie -F "radioid=[v]"  http://180.76.173.200:9999/infor/radio-infor.do

### 资讯：获取视频列表
*   path: /infor/video-list.do
*   param:
   -    module(String)  分类
   -    className 二级分类
   -	    page(int) 页码，从1开始
   -	    limit(int)
*   return:
   -	通用返回值 
*   example:
    -   curl -b cookie -F "module=[v]&page=[v]&limit=[v]&className=[v]"  http://180.76.173.200:9999/infor/video-list.do


### 资讯：获取视频详情
*   path: /infor/video-infor.do
*   param:
   -    videoid(String)  视频id
*   return:
   -	通用返回值 
*   example:
    -   curl -b cookie -F "videoid=[v]"  http://180.76.173.200:9999/infor/video-infor.do
 
 
### 资讯：健康首页推荐
*   path: /infor/home-health.do
*   param:
*   return:
   -	通用返回值 
*   example:
    -   curl -b cookie -F  http://180.76.173.200:9999/infor/home-health.do
 

### 资讯：健康首页推荐top4
*   path: /infor/home-top4.do
*   param:
*   return:
   -	通用返回值 
*   example:
    -   curl -b cookie -F  http://180.76.173.200:9999/infor/home-top4.do

### 资讯：健康个性推荐
*   path: /infor/user-health.do
*   param:
*   return:
   -	通用返回值 
*   example:
    -   curl -b cookie -F  http://180.76.173.200:9999/infor/user-health.do
 
### 资讯：安防个性推荐
*   path: /infor/user-securitys.do
*   param:
*   return:
   -	通用返回值 
*   example:
    -   curl -b cookie -F  http://180.76.173.200:9999/infor/user-securitys.do
 
 
### 资讯：获取广播module下的二级分类
*   path: /infor/radio-classes.do
*   param:
    -    module(String)  大分类
*   return:
   -	通用返回值  radioClasses 二级分类列表 
*   example:
    -   curl -b cookie -F "module=[v]"  http://180.76.173.200:9999/infor/radio-classes.do
 
 
### 资讯：获取广播下二级分类下广播列表
*   path: /infor/radio-groups.do
*   param:
    -    module(String)  大分类
	-    className(String)  二级分类
	-    start(int) 开始集数  
    -    end(int)   结束集数，如果查询所有 开始集数和结束集数均设置为0
*   return:
   -	通用返回值  radioList 广播信息列表 
*   example:
    -   curl -b cookie -F "module=[v]&className=[v]&start=[v]&end=[v]"  http://180.76.173.200:9999/infor/radio-groups.do
 
### 资讯：删除评论
*   path: /infor/delete-comment.do
*   param:
    -   commnetId(string)  评论id
*   return:
    -   通用返回值
*   example:
    -   curl -c cookie/cookie路径 -d    'commnetId=[v]'   'http://180.76.173.200:9999/infor/delete-comment.do'	


### 资讯：广播个性推荐
*   path: /infor/user-radios.do
*   param:
*   return:
   -	通用返回值 radioClasses 
*   example:
    -   curl -b cookie -F  http://180.76.173.200:9999/infor/user-radios.do
    

### 资讯：视频个性推荐
*   path: /infor/user-videos.do
*   param:
*   return:
   -	通用返回值 videoClasses 
*   example:
    -   curl -b cookie -F  http://180.76.173.200:9999/infor/user-videos.do
 
### 资讯：获取视频module下的二级分类
*   path: /infor/video-classes.do
*   param:
    -    module(String)  大分类
*   return:
   -	通用返回值  videoClasses 二级分类列表 
*   example:
    -   curl -b cookie -F "module=[v]"  http://180.76.173.200:9999/infor/video-classes.do

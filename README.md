# 集成了多个前端视频播放器的Vue工程

[该项目前端基本框架参考](https://github.com/PanJiaChen/vue-admin-template)

## 1.视频流概述
常见的视频协议有：RTMP、RTSP、HTTP。这三个协议都属于互联网 TCP/IP 五层体系结构中应用层的协议。直播一般使用RTMP、RTSP，而点播用HTTP。

### 1.1	RTMP
Real Time Messaging Protocol（实时消息传输协议）

由Adobe公司提出的，未完全公开，基于TCP协议，RTMP协议一般传输的是 flv，f4v 格式流。RTMP一般在 TCP 1个通道上传输命令和数据。
注：只有支持flash插件的浏览器才可以播放RTMP协议的视频，但很不幸的是目前各大主流浏览器已经开始渐渐抛弃flash插件，例如现在最新的Chrome浏览器默认就是屏蔽flash插件的，要使用的话必须手动开启。而谷歌官方也宣布，到2020.12，Chrome将彻底抛弃flash。

### 1.2	RTSP
Real Time Streaming Protocol（实时流传输协议）

RTSP协议是共有协议，并有专门机构做维护。.RTSP协议一般传输的是 ts、mp4 格式的流。RTSP传输一般需要 2-3 个通道，命令和数据通道分离。
海康威视摄像头采集到的视频流数据，使用的传输协议便是RTSP。从这一段时间的调研来看，现在的网页直播，几乎没有使用RTSP协议的。

### 1.3	HLS
HTTP Live Streaming（HTTP直播流）

由苹果公司提出的基于Http协议的的流媒体网络传输协议。具有跨平台性、穿墙能力强、切换码率快，负载均衡的优点。但同时也具有实时性差、文件碎片化严重的缺点。

### 1.4	可用地址
通常进行 RTMP/RTSP 开发时，除了可以自己搭建视频服务器来进行测试外。也可以直接使用一些电视台的直播地址，省时省力。调研过程中总结出几个可用的在线直播地址：

①	湖南台：rtmp://58.200.131.2:1935/livetv/hunantv

②	韩国GoodTV：rtmp://mobliestream.c3tv.com:554/live/goodtv.sdp

若要试验一个直播地址是否可用，建议使用VLC media player播放器测试。

![](https://github.com/GrimmTao/VideoPlayerDemo/blob/master/images/vlcPlayer.png)

输入你要测试的网络直播地址，若可以播放，则说明该地址有效。


## 2.流媒体服务器
### 2.1	 EasyDarwin
#### 2.1.1	概述
EasyDarwin是由国内开源流媒体团队开发和维护的一款开源流媒体平台框架。免费、开源、RTSP流媒体服务器，基于Go语言开发。

官网：http://www.easydarwin.org/ 从官网看，EasyDarwin具有一套非常完整的视频生态链。
GitHub：http://github.com/EasyDarwin/EasyDarwin

#### 2.1.2	使用说明
1.	GitHub上下载相应的压缩包（以Windows版本为例），解压后直接运行EasyDarwin.exe（Linux运行相应的start.bat文件）。
2.	在浏览器输入 localhost:10080,用户名 密码均为 admin，若可以成功登陆，说明EasyDarwin启动成功：
 
 ![](https://github.com/GrimmTao/VideoPlayerDemo/blob/master/images/EasyDarwin_LoginSuccess.png)

3.	在推流端输入相应的推流地址，即可把rtsp视频流数据推送到EasyDarwin服务器上，此时“推流列表”下会新增一条实时推流的信息。
4.	推流地址的格式为：rtsp://{ip}:{port}/{id}，例如 rtsp://10.40.101.112:554/live，其中port值554为DasyDarwin默认的rtsp服务器端口，可在配置文件中修改；id为自定义内容。

### 2.2	 EasyDSS
#### 2.2.1	概述
EasyDSS是一款高性能流媒体服务器。集流媒体点播、转码、管理、直播、录像、检索、时移回看于一体，支持 RTMP 视频流。非开源、非免费，用于商用应该要收费。
官网：http://www.easydss.com/
注意如果登录EasyDSS主页，提示License过期，则重新从官网下载即可。

#### 2.2.2	使用说明
1.	官网下载相应的的压缩包（以windows版本为例），解压后启动EasyDSS.exe（Linux运行相应的start.bat文件）。若要修改配置，可在easydss.ini中修改。

![](https://github.com/GrimmTao/VideoPlayerDemo/blob/master/images/EasyDSS_start.png)
 
2.	在浏览器输入 localhost:10080,用户名 密码均为 admin，若可以成功登陆，说明EasyDarwin启动成功：

![](https://github.com/GrimmTao/VideoPlayerDemo/blob/master/images/EasyDSS02.png)
 
3.	左侧导航栏【视频直播】——主界面【创建直播】，创建一个直播后，直播列表就会新增一条直播，点击该直播的“编辑”，即可获取该直播的RTMP推流地址：

![](https://github.com/GrimmTao/VideoPlayerDemo/blob/master/images/EasyDSS03.png)
 
4.	当有视频流数据推送到该直播地址后，再次点击“编辑”按钮，即可看到各种格式的拉流地址，在前端设置相应的播放地址，即可观看该直播。

![](https://github.com/GrimmTao/VideoPlayerDemo/blob/master/images/EasyDSS04.png)
 

3.3	LiveQing
3.3.1	概述
是一款国内的云平台直播点播流媒体服务，支持RTMP视频流。非开源、非免费，用于商用应该要收费。
官网：https://www.liveqing.com/docs/products/LiveQing.html

3.3.2	使用说明
1.	官网下载相应的的压缩包（以windows版本为例），解压后启动LiveQing.exe（Linux运行相应的start.bat文件）。若要修改配置，可在liveqing.ini中修改。
 
![](https://github.com/GrimmTao/VideoPlayerDemo/blob/master/images/LiveQing01.png)

2.	在浏览器输入 localhost:10080,用户名 密码均为 admin，若可以成功登陆，说明LiveQing启动成功：

![](https://github.com/GrimmTao/VideoPlayerDemo/blob/master/images/LiveQing02.png)
 

3.  左侧导航栏【鉴权直播】——主界面【创建直播】，创建一个直播后，直播列表就会新增一条直播，点击该直播的“编辑”，即可获取该直播的RTMP推流地址。接下来的操作就和EasyDSS大致一样了。

## 3.	前端播放器
### 3.1	 vue-video-player
一款适用于 Vue 的 video.js播放器组件。注意在node中安装vue-video-player时一定要使用npm指令，而不要使用cnpm指令，否则会报错（血泪经验）。不支持RTSP协议的视频流。所以，如果使用EsayDarwin流媒体服务器，则无法用vue-video-player来进行播放。

npm安装vue-video-player : npm install vue-video-player --save

GitHub:  https://github.com/surmon-china/vue-video-player

在测试过程中，我发现vue-video-player播放rtmp视频流延时较为严重，并且其延时时长就随着直播时间的增加而增加。因此弃用该播放器。

### 3.2	 Ckplayer
Ckplayer（超酷网页播放器）是一款在网页上播放视频的免费软件，主要特点是：免费，小巧，功能强大，定制方便。该播放器由国内某团队开发，其网站、帮助文档均为中文，使用起来很方便，在使用过程中发现使用简单、方便。不支持RTSP。

官网：http://www.ckplayer.com/
 
最重要的一点，利用Ckplayer进行视频直播，长时间（2小时）运行，其延时可以稳定在1~2s左右，从视觉效果上看，完全可以接受。
使用方法：将下载下来的ckplayer文件夹，放到vue工程下public文件夹中，并在public文件夹下的index.html文件中，将ckplayer导入，如下：

![](https://github.com/GrimmTao/VideoPlayerDemo/blob/master/images/Ckplayer01.png)
 
### 3.3	 flv.js
该播放器是由国内著名视频网站B站推出的用纯JavaScript编写的HTML5  Flash Video（FLV）播放器，不需要浏览器支持flash，开源，免费。

npm 安装flv.js ：npm install –save flv.js

GitHub： https://github.com/bilibili/flv.js

flv.js的工作原理是将FLV文件流转换为ISO BMFF（分段MP4）段，然后
video标签通过Media Source Extensions API 将mp4段馈送到HTML5 元素中。

![](https://github.com/GrimmTao/VideoPlayerDemo/blob/master/images/flvjs01.png)
 
上面的截图是bilibili官方给出的demo，地址为：http://bilibili.github.io/flv.js/demo/
将flv.js集成到vue工程中，得到的效果如下：
 
![](https://github.com/GrimmTao/VideoPlayerDemo/blob/master/images/flvjs02.png)

### 3.4	LivePlayer
是一款H5直播/点播 播放器，免费使用。官方说明支持MP4、m3u8/HLS、HTTP-FLV、WS-FLV、RTMP播放。
MP4尝试成功（无需Flash支持）；m3u8/HLS尝试成功（无需Flash支持）；RTMP可以播放，但是画面极卡；HTTP-FLV播放存在跨域问题，没有尝试成功。

官网：https://www.liveqing.com/docs/manuals/LivePlayer.html

![](https://github.com/GrimmTao/VideoPlayerDemo/blob/master/images/LivePlayer01.png)
 
官网中有关于如何在vue中使用LivePlayer的说明，但官网中的说明是基于vue工程中有webpack.config.js这种文件的vue工程，如果是没有这个文件的工程，如何配置liveplayer？
首先还是安装LivePlayer的相关依赖：

npm install @liveqing/liveplayer

然后找到vue工程根目录下的vue.config.js文件，进行如下编辑：
 
![](https://github.com/GrimmTao/VideoPlayerDemo/blob/master/images/LivePlayer02.png)

![](https://github.com/GrimmTao/VideoPlayerDemo/blob/master/images/LivePlayer03.png)

其实就是把原来在webpack中编辑的内容换到了vue.config.js中。
最后在public/index.html中引入相应的js就可以了：
 
![](https://github.com/GrimmTao/VideoPlayerDemo/blob/master/images/LivePlayer04.png)

以上步骤是自己摸索出来的，参考链接为：https://segmentfault.com/a/1190000016101954

### 3.5	Ali-Player

![](https://github.com/GrimmTao/VideoPlayerDemo/blob/master/images/AliPlayer01.png)
 
该播放器没有自带的工具栏，需要自己调用函数去实现功能。

官网：https://www.alibabacloud.com/help/zh/doc-detail/57314.htm
     https://help.aliyun.com/document_detail/125574.html

GitHub：https://github.com/slacrey/vue-aliplayer

### 3.6	html5_rtsp_player
写该文档的时候，新发现的一个支持rtsp协议的前端播放技术，目前还没有尝试，有兴趣的话可以尝试一下。

Npm安装：cnpm install html5_rtsp_player

GitHub： https://github.com/Streamedian/html5_rtsp_player

### 3.7	 JW Player
也是一款优秀的网页媒体播放器，但目前网上关于它的例程较少，未能尝试成功。

官网：https://developer.jwplayer.com/jwplayer/docs

GitHub：https://github.com/jwplayer/jwplayer

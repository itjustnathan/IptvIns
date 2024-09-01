
大部分网上找的源都无法正常使用，需要自行筛选是否可播放

五星上将麦克阿瑟表示：
在N多个文件里找到N多个可用的源并合并到一个文件是程序该做的事情

（主要是太懒了，不想随时为了看电视还要随时检查源是否可播放）

# 程序功能和用法:

## 前置条件

1. 网络：需要有IPv4+IPv6双协议栈
2. 主机：需要Linux/Windows系统，并且必须是amd64（x86）/arm64 架构CPU
3. 有手就行

## 安装部署

上传文件到Linux环境下，解压得到 iptvIns、ffmpeg、ffprobe文件

对文件进行授权操作 : `chmod +x iptvIns* ffmpeg ffprobe`

即可完成安装

## 程序用法

打印帮助
```bash
[root@MacBook-Pro src]#  ./iptvIns_linux-x86_v2.1.16 -h
Usage of ./iptvIns_linux-x86_v2.1.16:
  -e    Adapt show list according to media source   # 节目单匹配模式：在epg源中找到匹配m3u8输入源的节目单输出
  -v    Print version # 没用的玩意
```

运行示例

```bash
[root@MacBook-Pro src]# ./iptvIns_linux-x86_v2.1.16
Usage:
  # 示例：输入源可用性检查：对多个m3u8进行检测，并输出可用源到自定义目录output下
  # 使用-c参数指定使用检测功能，后接并发数，建议和文件数保持一致
  Playable:      ./iptvIns -c 2 in1.m3u8 in2.m3u8 in3/*.m3u8 output  
  # 示例：输入源可用性检查：对多个输入源全部合并到out.m3u8文件,输出文件支持m3u8和txt格式
  # 注意：程序会拿第一个输入源作为m3u8文件中的频道节目信息，所以一般建议做一个只有频道信息的的文件作为第一个源
  Mergation:     ./iptvIns in1.m3u8 in2.m3u8 [in3.m3u8 in...] out.m3u8
  # 示例：使用 -e 参数，开启epg匹配模式， 依据source.xml文件作为epg源，只匹配input.m3u8中的频道节目单并输出到epg.xml
  Programme:     ./iptvIns -e input.m3u8 source.xml epg.xml
```

## 注意事项

1. 流地址检测除了本身能否播放外，还依赖本地环境，所以确保双协议就位
2. 程序本身只是实现了核心流程，想要实现全自动化，需自行配合脚本使用

   比如: 单个文件检测后 --> 对检测的多文件合并 --> 再匹配epg节目单
3. 程序会过滤低于1080分辨率的视频源，代码写死了,后期看需求要不要写成可配项
4. 第三方程序ffmpeg、ffprobe仅提供amd64下的Linux环境下运行的文件，其他环境需自行获取安装
    - 官方下载地址：https://ffmpeg.org//download.html
    - 旧版本下载地址【推荐4.x版本】：https://www.videohelp.com/software/ffmpeg/old-versions
    - Windows版本：https://www.videohelp.com/download/ffmpeg-4.4.1-full_build.7z
    - Linux Amd64版本：https://www.johnvansickle.com/ffmpeg/old-releases/ffmpeg-4.4.1-amd64-static.tar.xz
    - Linux Arm64版本：https://www.johnvansickle.com/ffmpeg/old-releases/ffmpeg-4.4.1-arm64-static.tar.xz
    - Darwin Intel版本：https://evermeet.cx/pub/ffmpeg/
   
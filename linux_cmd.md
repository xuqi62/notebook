linux查看库依赖
ldd libname.so
android 查看库依赖
readelf -d libname.so


gstreamer命令
播放：gst-launch-1.0 playbin video-sink=waylandsink uri="file:///mnt/UDISK/1.mp4"
    gst-launch-1.0 filesrc location=/mnt/UDISK/1.mp4 ! qtdemux ! h264parse ! omxh264dec ! queue ! fakesink
	
测试同编同解命令为：
    gst-launch-1.0 filesrc location=/mnt/UDISK/input.h264 ! omxh264dec ! queue ! omxh264videoenc ! filesink location=/tmp/output.h264
    /mnt/UDISK/input.h264为需要推进小机器里的h264码流，/tmp/output.h264为输出码流的位置。
	
查看；gst-inspect-1.0

调整gst打印级别
export  GST_DEBUG=2
测试同编同解命令为：
    gst-launch-1.0 filesrc location=/mnt/UDISK/input.h264 ! omxh264dec ! queue ! omxh264videoenc ! filesink location=/tmp/output.h264
    /mnt/UDISK/input.h264为需要推进小机器里的h264码流，/tmp/output.h264为输出码流的位置。


1663 Linux命令
去除打印
echo 0 > /proc/sys/kernel/printk
export LD_LIBRARY_PATH='/mnt/install/lib:/mnt/install/lib/tools_lib'

1667 Linux
export LD_LIBRARY_PATH='/mnt/UDISK/lib/'

2.mount sdcard
cat /proc/partitions 
mount /dev/mmcblk0p1 /mnt/

连接wifi
在/usr/bin目录下
有的话执行wifitest wifi名称 wifi密码
执行以上命令之后，如果有报这个错误：
udhcpc wlan0 timeout!
Connected timeout!
则再执行以下命令：
udhcpc -i wlan0 


http://we.china-ota.com/WeChatSurvey/22.mp3

set url: file:///mnt/usb/UDISK/1.mov
set url: file:///mnt/data/A024-480P_AVC_AAC LC_2M_24F.mp4
set url: file:///mnt/data/A079_480P_AVC_AAC_221K_24F.mov

set url: /mnt/Media/Video/A037_480P_MPEG4_AMR_361K_18F.3gp
/mnt/install/bin/5ch_dd_25fps_acmod_7.mp4

./demoDecoder file:///mnt/Media/Video/A037_480P_MPEG4_AMR_361K_18F.3gp /mnt/ 0


ulimit -c unlimited

linux 查看 *.a *.so 符号表
objdump -tT libName.so | grep symbel symbolName
nm -D libName.so | grep symbel symbolName


cedarx_release仓库代码
upstream        ssh://liweihai@172.16.1.19/git_repo/cedarx_release/cedarx_release.git (push)
密码： lwh%1121

替换库
LD_PRELOAD=libcdx_debug.so ./playerdemo
set url: /mnt/SDCARD/1.mp3





ffmpeg转码
要转h264需要先安装libx264，aac需要安装libfaac
安装后configure时选择 --enable-libfaac --enable-nonfree --enable-libx264
ffplay.exe -f rawvideo -video_size 1280x536 E:\yuv1.yuv


 
 
 
 
 
 


adb 如何查看进程cpu和内存占用率
1. adb shell
2. top | grep PID
top -m 20 -t 查看某个线程占用cpu资源

toolbox top -t -s cpu -m 20

###############################################################################
A50开四核
echo 1800000 4 0 0 1800000 4 0 0 > /sys/devices/platform/soc/cpu_budget_cooling/roomage
chmod 440 /sys/devices/platform/soc/cpu_budget_cooling/roomage

检查一下 roomage节点是不是 1800000 4 0 0 1800000 4 0 0， 这样就是 定在最高频 四核全开
####################################################################################

 查看进程跑在哪个cpu上
 ps -A -o NAME -o CPU | grep media
#######################################################################

查看中断号
cat  /proc/inter*

把中断绑定到其他核上
假设中断号为197 
/proc/irq/197 # cat smp_affinity_list

echo 2 > smp_affinity_list
########################################################################

抓包：tcpdump -i wlan0 -s 0 -w /sdcard/rtmp.pcap -v

看网卡：busybox ifconfig

查看系统时钟资源：
  /sys/kernel/debug/clk/clk_sum

u盘读/写速率的测试命令分别如下：
1、测试写速率：
time dd if=/dev/zero of=/mnt/usb/test.bin bs=500000 count=1000
2、测试读速率：
time dd if=/mnt/usb/test.bin bs=500000 count=1000 of=/dev/null

设置cma内存
sunxi#env set cma 650M
sunxi#env save
Saving Environment to SUNXI...
saveenv storage_type = 2
sunxi#env print cma
cma=600M

androidO 显示帧率
 setprop debug.hwc  on.fps  显示帧率；
  setprop debug.hwc  on.show  每一帧的layer信息都会打印出来


adb logcat
去除某个文件里的打印 adb logcat IMGSRV:s  (IMGSRV文件)


adb 启动apk
adb shell am start -n [package name]/[apkMainActivity]
由AndroidManifest.xml中package="com.example.helloworld"得到package name
<activity
            android:name=".MainActivity"
            android:label="@string/app_name" >
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
		activity属性得到MainActivity
如： am start -n com.example.helloworld/com.example.helloworld.MainActivity

启动tvdLauncher
am start -n com.softwinner.launcher/com.softwinner.launcher.Launcher

启动华为视频通话啊pk
am start -n com.huawei.iptv.stb.videotalk.activity/.MainActivity

H3启动图库apk
am start -n com.android.gallery3d/com.android.gallery3d.app.GalleryActivity
com.android.gallery3d.app.GalleryActivity

启动相机
am start -n com.android.camera2/com.android.camera.CameraActivity

启动播放器
am start -n com.softwinner.TvdVideo/com.softwinner.TvdVideo.TvdVideoActivity -d https://fs-sq-1.kfs.io/201307/2d8qY-MrgmhzkHYXl7UFKIgDA33jUomeZ1o9vMsUN8I=?play_mode=openapi&__gda__=1468392340_1dde9aad4adf195519096edbbcc60bfc

"http://pl.youku.com/playlist/m3u8?ts=1456996755&keyframe=1&vid=XMTQzMDE1NTMwOA==&type=hd2&ctype=20&sid=345699675553920d0a321&token=9056&ev=1&oip=1900834927&did=eabca10cf602692b8e64b59d908e6c0deabca10c&ep=9Jk5MdwNbw3S9D0W4mdWvPo8Nk2qa0cfqmdMtQyb%2FiRx94SJlur%2Ff0u15eVSknm%2B%0A"

http://60.19.28.11:18011/4k/8.mp4

http://192.168.152.7:8080/h265.ts



SN&MAC试试?
00000100000760600001AC4AFE2BAAA6
HS0471000098@IPTV
030014


fastboot下执行命令烧写MAC&&SN
pst erase 
save_userdata mac  AC:4A:FE:2B:AA:A0 

save_userdata specialstr 00000100000760600001AC4AFE2BAAA6 

查看VE频率
root@rabbit-p1:/sys/class/sunxi_dump # echo 0x01c20018 > dump                  
root@rabbit-p1:/sys/class/sunxi_dump # cat dump    
0x91000e00
24*N/M，其中N a=(14:8 bit), b=(3:0 bit), N=a+1, M=b+1; 如 0x91000e00， 则为 360M


串口波特率
115200

android7.0 drm视频测试
账号 liling19930619@gmail.com
密码 ling1993

leegreatworld
egreatworld


hls动态码率片源
http://www.youtube.com/api/manifest/hls_variant/id/0168724d02bd9945/itag/5/source/youtube/playlist_type/DVR/ip/0.0.0.0/ipbits/0/expire/19000000000/sparams/ip,ipbits,expire,id,itag,source,playlist_type/signature/773AB8ACC68A96E5AA481996AD6A1BBCB70DCB87.95733B544ACC5F01A1223A837D2CF04DF85A3360/key/ik0/file/m3u8

关闭selinux


echo 4 > /sys/kernel/autohotplug/lock
echo 0-3 > /dev/cpuset/foreground/cpus

锁核：  /sys/kernel/autohotplug/enable   // 1 默认打开
        　echo 4 > /sys/kernel/autohotplug/lock  //锁4核

定频：  echo 1200000 > /sys/devices/system/cpu/cpu0/cpufreq/scaling_max_freq
        　echo 1200000 > /sys/devices/system/cpu/cpu0/cpufreq/scaling_min_freq   //4个核跑在1.2G 

　　　cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_cur_freq  //查看0号cpu当前频率


内存调试
lsof | grep dmabuf|grep mem

cts 测试单项测试方法

有activity 
直接am am start -n 包名/activity 路径名类名

没有activity

am instrument -r -e class android.media.cts.AdaptivePlaybackTest#testHEVC_adaptiveDrc -w android.media.cts/android.support.test.runner.AndroidJUnitRunner

参数说明
android.media.cts.AdaptivePlaybackTest#testHEVC_adaptiveDrcs 是包名类名加方法名。
android.media.cts  包名
android.support.test.runner.AndroidJUnitRunner AndroidManifest 里面 instrument 这个选项


参考
http://www.bkjia.com/Androidjc/1009016.html

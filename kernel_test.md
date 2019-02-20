内核调试

1.单独编译成一个模块
      修改linux3.10/.config文件     CONFIG_VIDEO_ENCODER_DECODER = m
   把/dev/cedar_dev单独编译成一个模块ko

2.编译生成cedar.ko

3.ko推入小机， insmod cedar.ko

查看内核打印  cat /proc/kmag


1. 打印进程堆栈 (android 版本4.2以上)
        # debuggerd -b [进程号]
 
2. 找出最近更新的库，并且推到小机 (linux)
    $ find ${OUT}/system/lib -name '*.so' -type f -mmin -30 | xargs -i adb push {} /system/lib
 
 3. Android截屏
      # adb shell screencap -p /sdcard/1.png
   
 4. 查看ion使用情况 
      # cat /sys/kernel/debug/ion/carveout
		# cat /sys/kernel/debug/ion/heaps/cma
  
 5. BOX原型机打开adb调试USB端口
    A80: cat /sys/bus/platform/devices/sunxi_otg/usb_device
    H3:  cat /sys/bus/platform/devices/sunxi_usb_udc/usb_device
 
  6. 查看ion使用情况 
     cat /sys/kernel/debug/ion/carveout
  
  7. 系统监控
     DE图层
     cat /sys/class/disp/disp/attr/sys
     看cpu的打开情况：
     cat /sys/devices/system/cpu/online
     看指定cpu的频率
     cat /sys/devices/system/cpu/cpu0/cpufreq/cpuinfo_cur_freq
     各CPU运行情况
     busybox mpstat -P ALL 2  
  
	
一. 锁定4核命令:
echo 0 > /sys/kernel/autohotplug/enable?
echo 1 > /sys/devices/system/cpu/cpu0/online 
echo 1 > /sys/devices/system/cpu/cpu1/online 
echo 1 > /sys/devices/system/cpu/cpu2/online 
echo 1 > /sys/devices/system/cpu/cpu3/online 
echo 0 > /sys/devices/system/cpu/cpu4/online 
echo 0 > /sys/devices/system/cpu/cpu5/online 
echo 0 > /sys/devices/system/cpu/cpu6/online 
echo 0 > /sys/devices/system/cpu/cpu7/online 
二. 锁定1.6G命令:
echo userspace > /sys/devices/system/cpu/cpu0/cpufreq/scaling_governor 
echo 1608000 > /sys/devices/system/cpu/cpu0/cpufreq/scaling_setspeed

锁核：  /sys/kernel/autohotplug/enable   // 1 默认打开
        　echo 4 > /sys/kernel/autohotplug/lock  //锁4核

定频：  echo 1200000 > /sys/devices/system/cpu/cpu0/cpufreq/scaling_max_freq
        　echo 1200000 > /sys/devices/system/cpu/cpu0/cpufreq/scaling_min_freq   //4个核跑在1.2G 

　　　cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_min_freq/scaling_cur_freq  //查看0号cpu当前频率



查看系统带宽
 cd sys/class/script
echo dram_para > dump;cat dump

关闭dram动态调频
echo 1 > /sys/class/devfreq/dramfreq/adaptive/pause
 cat /sys/class/devfreq/dramfreq/cur_freq
 
 
 
 
 查看内存（内存泄露）
adb shell top -s vss -m
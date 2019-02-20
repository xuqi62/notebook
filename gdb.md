
gdb 命令
1.设置动态库绝对路径
set solib-search-path /home/xuqi/1663/install/lib/

2.查看动态库是否加载
info sharedlibrary

生成core文件
ulimit -c unlimited
gdb ./a core

l
生成backtrace
bt

adb connect [IP adrress]

不能推库
adb shell
su
mount -o remount,rw /dev/block/nandc /system

查看各个线程是否卡住
debuggerd -b `busybox pidof mediaserver`



配置tool-chain路径


解压后放在编译服务器某个文件下 以tools为例
 
1.在编译服务器目录~ 下执行
vi .bashrc
把工具链路径添加到该文件最后
export PATH=$PATH:/home/xuqi/tools/toolchain_arm_uClibc/staging_dir/toolchain-arm_cortex-a7+neon_gcc-4.8-linaro_uClibc-0.9.33.2_eabi/bin
export STAGING_DIR=/home/xuqi/tools/toolchain_arm_uClibc/staging_dir
 
2.执行source .bashrc，使环境变量生效
 
3.编译时makefile这几个变量设置为如下
CC    = arm-openwrt-linux-uclibcgnueabi-gcc
LD    = arm-openwrt-linux-uclibcgnueabi-gcc
CPP   = arm-openwrt-linux-uclibcgnueabi-g++
STRIP = arm-openwrt-linux-uclibcgnueabi-strip
AR    = arm-openwrt-linux-uclibcgnueabi-ar
 

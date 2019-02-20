SELinux 权限问题

1. 串口出现类似打印 type=1400 audit(1433736357.070:64): avc: denied { execmem } for pid=32468 comm="app_process32" scontext=u:r:zygote:s0 tcontext=u:r:zygote:s0 tclass=process permissive=0
   是SELinux的权限控制问题

解决办法：allow zygote zygote:process execmem;

230.452058] CPU2: Booted secondary processor
[  230.457034] CPU2: update cpu_power 1968128
[  230.543800] type=1400 audit(1433914421.077:23): avc: denied { create } for pid=11812 comm="ndroid.systemui" key=-1 scontext=u:r:platform_app:s0 tcontext=u:r:platform_app:s0 tclass=sem permissive=0
[  230.578798] type=1400 audit(1433914421.077:24): avc: denied { create } for pid=11812 comm="ndroid.systemui" key=-1 scontext=u:r:platform_app:s0 tcontext=u:r:platform_app:s0 tclass=sem permissive=0

解决办法：allow platform_app self:sem create;

100643] [dramfreq] 336000KHz->672000KHz ok
[ 1271.455667] CPU Budget hotplug: cluster0 min:0 max:4
[ 1271.466130] CPU Budget hotplug: cluster0 min:0 max:4
[ 1271.587352] type=1400 audit(1433917015.877:34): avc: denied { unix_read unix_write } for pid=1365 comm=4173796E635461736B202333 key=-1 scontext=u:r:untrusted_app:s0 tcontext=u:r:platform_app:s0 tclass=sem permissive=0
[ 1271.702854] CPU Budget hotplug: cluster0 min:0 max:4
[ 1272.074441] CPU3: shutdown
[ 1272.077664] psci: CPU3 killed.
[ 1272.270763] CPU2: shutdown
[ 1272.274794] psci: CPU2 killed.



[   67.143954] type=1400 audit(1433919139.869:15): avc: denied { unix_read unix_write } for pid=7066 comm="ngs.android.pop" key=-1 scontext=u:r:untrusted_app:s0 tcontext=u:r:platform_app:s0 tclass=sem permissive=0


快速刷boot命令
1.在android下编译bootimage
make bootimage -j32
生成的bootimage在 \android\out\target\product\tulip-t1\boot.img

2.在串口输入 reboot bootloader
3.windows下cmd命令
 1) fastboot -i 0x1f3a flash boot X:\AndroidL\android\out\target\product\tulip-t1\boot.img
  2)fastboot -i 0x1f3a reboot
  
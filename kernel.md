
1.查看java heapsize
adb shell getprop | grep dalvik.vm.heapsize

2.adb shell cat /proc/meminfo查看RAM
MemTotal：可以使用的RAM总和（小于实际RAM，操作系统预留了一部分）
MemFree：未使用的RAM
Cached：缓存（这个也是app可以申请到的内存）
HightTotal：RAM中地址高于860M的物理内存总和，只能被用户空间的程序使用。
HightFree：RAM中地址高于860M的未使用内存
LowTotal：RAM中内核和用户空间程序都可以使用的内存总和（对于512M的RAM: lowTotal= MemTotal）
LowFree: RAM中内核和用户空间程序未使用的内存（对于512M的RAM: lowFree = MemFree）

 3.应用程序如何绕过dalvikvm heapsize的限制
（1）、创建子进程
      创建一个新的进程，那么我们就可以把一些对象分配到新进程的heap上了，从而达到一个应用程序使用更多的内存的目的，当然，创建子进程会增加系统开销，而且并不是所有应用程序都适合这样做，视需求而定。
创建子进程的方法：使用android:process标签
（2）、使用jni在native heap上申请空间（推荐使用）
      nativeheap的增长并不受dalvik vm heapsize的限制，从图6可以看出这一点，它的native heap size已经远远超过了dalvik heap size的限制。
只要RAM有剩余空间，程序员可以一直在native heap上申请空间，当然如果 RAM快耗尽，memory killer会杀进程释放RAM。大家使用一些软件时，有时候会闪退，就可能是软件在native层申请了比较多的内存导致的。比如，我就碰到过UC web在浏览内容比较多的网页时闪退，原因就是其native heap增长到比较大的值，占用了大量的RAM，被memory killer杀掉了。
（3）、使用显存（操作系统预留RAM的一部分作为显存）
       使用 OpenGL textures 等 API ， texture memory 不受 dalvik vm heapsize 限制，这个我没有实践过。再比如 Android 中的 GraphicBufferAllocator 申请的内存就是显存。

4、Bitmap分配在dalvik heap上
从代码中可以看到bitmap对象是通过env->NewOject( )创建的，到这里疑惑就解开了，bitmap对象是虚拟机创建的，JNIEnv的NewOject方法返回的是java对象，并不是native对象，所以它会分配到dalvik heap中。

5.java程序如何才能创建native对象
必须使用jni，而且应该用C语言的malloc或者C++的new关键字。实例代码如下：
JNIEXPORT void JNICALLJava_com_example_demo_TestMemory_nativeMalloc(JNIEnv *, jobject)
{      
         void * p= malloc(1024*1024*50);
         SLOGD("allocate50M Bytes memory");
         if (p !=NULL)
         {       
                   //memorywill not used without calling memset()
                   memset(p,0, 1024*1024*50);
         }
         else
                   SLOGE("mallocfailure.");
   ….
   ….
free(p); //free memory
}

这里对代码中的memset做一点说明：
       new或者malloc申请的内存是虚拟内存，申请之后不会立即映射到物理内存，即不会占用RAM，只有调用memset使用内存后，虚拟内存才会真正映射到RAM。

	
		 
git生成patch
git format_patch -1

打patch
git am --signoff < newpatch.patch

分享git patch的功能：
git打补丁有2种方法，
1. git diff生成标准patch，用git apply xxx.patch来打补丁；
2. git format-patch生成git专用补丁，用git am xxx.patch来打补丁。
git diff生成的Patch兼容性强；git format-patch生成的补丁中含有这个补丁开发者的名字，因此在应用补丁时，这个名字会被记录进版本库。第一种方法感兴趣的参考下相关链接资料，这里分享下第二种方法。
例如针对A20的修改为master分支666882bd50befe91fe919948cc693d90309d3041提交，需要往box-stable分支打上补丁，步骤：
1. 切换到master分支：git checkout master
2. 切到对应版本：git reset --hard 666882bd50befe91fe919948cc693d90309d3041
3. 生成补丁：git format-patch -M box-stable 
此时可以看到从box-stable基础版本到666882bd50befe91fe919948cc693d90309d3041版本的每次提交，都产生一个patch，1.patch, 2.patch, ..., 13.patch，假设需要打的补丁为13.patch
4. 切换到要打补丁的分支：git checkout box-stable
5. git am 13.patch
如果代码没有冲突，则打好补丁，只需要push就可；如果代码冲突，则整个patch都不会被集成。需要做如下操作：
   a. git apply 13.patch --reject （打补丁，若有冲突则生成冲突内容）
   b. 根据.rej文件手动解决所有冲突
   c. git add  FIXED_FILES
   d. git am --resolved
6. git push origin box-stable:box-stable


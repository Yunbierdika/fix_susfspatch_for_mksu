## 修复MKSU在应用SUSFS4KSU补丁时报错导致没有应用完的问题（补丁的补丁）

### 使用方法：

克隆MKSU专用补丁修补文件
```bash
git clone https://github.com/Yunbierdika/fix_susfspatch_for_mksu.git
```
在**打完所有SUS4KSU补丁后**将本仓库的补丁修补文件复制到MKSU的目录里，然后进入MKSU目录中，应用补丁
```bash
cd fix_susfspatch_for_mksu  #进入本仓库目录
```
```bash
# 复制补丁文件到MKSU目录
cp core_hook.patch ../KernelSU/
cp sucompat.patch ../KernelSU/
```
```bash
#进入MKSU目录
cd KernelSU
#应用补丁
git apply core_hook.patch
git apply sucompat.patch
```
以上步骤**无报错**完成后进入以下内核目录
```bash
cd common/fs/devpts/
```
还原SUSFS4KSU对***common/fs/devpts/inode.c***文件的修改（由于MKSU和原版KSU相比，去掉了在kernel/sucompat.c中的“**int ksu_handle_devpts(struct inode *inode)**”，如果不还原会导致提示“ksu_handle_devpts”未定义）
```bash
git restore inode.c
```
完成。

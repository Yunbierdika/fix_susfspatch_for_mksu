## 修复 MKSU 在应用 SUSFS4KSU 补丁时报错导致没有应用完的问题（补丁的补丁）

### 使用方法：

克隆 MKSU 专用补丁修补文件

```bash
git clone https://github.com/Yunbierdika/fix_susfspatch_for_mksu.git
```

在**打完所有 SUS4KSU 补丁后**将本仓库的补丁修补文件复制到 MKSU 的目录里，然后进入 MKSU 目录中，应用补丁

```bash
cd fix_susfspatch_for_mksu  #进入本仓库目录
```

```bash
# 复制补丁文件到MKSU目录
cp core_hook.patch ../KernelSU/
```

```bash
#进入MKSU目录
cd KernelSU
#应用补丁
git apply core_hook.patch
```

以上步骤**无报错**完成后进入 KernelSU 目录

```bash
cd KernelSU
```

还原 MKSU 对 devpts hook 的删除（authored by liqideqq）

```bash
git revert -m 1 $(git log --grep="remove devpts hook" --pretty=format:"%h") -n
```

完成。

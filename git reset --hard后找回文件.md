## 需求

* 说明：git reset —hard <commit>命令可将工作区和暂存区都回到上一次版本，并删除之前的所有信息提交。有时误使用该命令会造成文件丢失。
* 需求：使用git reset —hard <commit>命令后，将丢失文件找回

---

## 实现

1. 使用命令

   ```bash
   $ git fsck --lost-found
   ```

2. 通过.git/lost-found/other这个路径，可以恢复任何git add过的文件

   注：没有git add过的文件尸骨难寻

3. 使用命令，可以找到最近被add到本地仓库的60个文件

   ```bash
   $ find .git/objects -type f | xargs ls -lt | sed 60q
   ```

   注：数字可改

**没事不要随便用 git reset —hard <commit> 命令**

---

## git reset命令补充

```bash
git reset [--soft | --mixed | --hard] [HEAD]
```

**--mixed** 为默认，可以不用带该参数。暂存区回到上一版本，工作区保持不变

```bash
git reset  [HEAD] 

$ git reset HEAD^            # 回退所有内容到上一个版本  
$ git reset HEAD^ hello.php  # 回退 hello.php 文件的版本到上一个版本  
$ git  reset  052e           # 回退到指定版本
```

**--soft** 参数用于回退到某个版本

```bash
git reset --soft HEAD

$ git reset --soft HEAD~3 # 回退上上上一个版本
```

**--hard** 工作区和暂存区都回到上一次版本，并删除之前的所有信息提交 【慎用！】

```bash
git reset --hard HEAD

$ git reset –hard HEAD~3  # 回退上上上一个版本  
$ git reset –hard bae128  # 回退到某个版本回退点之前的所有信息
$ git reset --hard origin/master    # 将本地的状态回退到和远程的一样 
```
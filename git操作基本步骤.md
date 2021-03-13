## git操作基本步骤

---


1. git全局配置

   ```bash
   git config --global user.name "name" //全局配置
   git config --global user.email "email" //全局配置
   ```
   注：git的每一次提交都会使用这些信息，并且会写入每一次提交中

   

2. 创建仓库，并设置SSH密钥

   ```bash
   1. 创建SSH KEY：`$ ssh-keygen -t rsa -C "email"
   2. 进入.ssh文件
   3. cat id_rsa.pub
   4. gitlab中New SSH key，并添加公钥
   ```

---

###方式一、克隆远程仓库到本地，再推到远程仓库

1. 远程仓库克隆到本地

   ```bash
   git clone http://gitlab.platdep.shuyun.com/zehui.zhang/test.git
   ```

   1. http克隆和ssh克隆的区别：

      http：每次fetch和push代码都需要输入账号和密码

      ssh：需要在克隆之前先配置和添加好SSH key，故非项目拥有者不能使用该方法

      

   2. 克隆内容包括：

    1）完整的远程仓库

   ```bash
   urnotzzh@urnotzzhdeMBP desktop % cd test
   ```

    2）初始化本地库

   ```bash
   urnotzzh@urnotzzhdeMBP test % ls -al
   total 0
   drwxr-xr-x  3 urnotzzh staff  96 12 17 19:18 .
   drwx------+ 15 urnotzzh staff 480 12 17 19:18 ..
   drwxr-xr-x  9 urnotzzh staff 288 12 17 19:18 .git
   ```

    3）创建origin远程地址别名

    ```bash
    urnotzzh@urnotzzhdeMBP test % git remote -v
    origin	ssh://git@gitlab.platdep.shuyun.com:2222/zehui.zhang/test.git (fetch)
    origin	ssh://git@gitlab.platdep.shuyun.com:2222/zehui.zhang/test.git (push)
    ```

   思考：哪怕是一个新建立的空的仓库，克隆下来已有别名和初始化，故不用再连接远程仓库和初始化

   

2. 本地仓库推到远程仓库

   重复方式二中的操作，且省略【初始化】和【连接远程仓库】步骤

---

###方式二：直接在本地建立项目，再推到远程仓库

1. 创建项目，并进入该目录

   ```bash
   urnotzzh@urnotzzhdeMBP desktop % cd test
   ```

   

2. 初始化**（克隆可省）**

   ```bash
   urnotzzh@urnotzzhdeMBP test % git init
   ```

   注：该命令将创建一个名为 .git 的子隐藏目录，可使用 git ls -al 命令查看；

   .git含有初始化的git仓库中所有的必须文件，也是git保存数据记录的地方，非常重要，不要轻易改动

   

3. 在test中新建文件readme.txt至本地**【工作区】**

  ```bash
  urnotzzh@urnotzzhdeMBP test % touch readme.txt
  ```

  

4. 把文件readme.txt添加到**【暂存区】**

  ```bash
  urnotzzh@urnotzzhdeMBP test % git add readme,txt
  ```

  ​	注：git add . ：添加所有文件至暂存区，慎

  

5. 将暂存区内容添加到**【本地仓库】**，每次添加可提交备注

  ```bash
  urnotzzh@urnotzzhdeMBP test % git commit -m "content"
  ```

  

6. 将本地仓库与**【远程仓库】**建立联系**（克隆可省）**

  ```bash
  urnotzzh@urnotzzhdeMBP test % git remote add origin git@gitlab.platdep.shuyun.com:2222/zehui.zhang/test.git
  ```

  ​	思考：此处操作实质为创建origin远程地址别名，即将远程仓库地址赋给origin

  

7. 将本地仓库内容推到远程仓库中的**【master分支】**

  ```bash
  urnotzzh@urnotzzhdeMBP test % git push -u origin master
  ```

  ​	注：新建的远程仓库为空，故需加-u，下次不用

---

##git区域理解

![friedChicken](https://www.runoob.com/wp-content/uploads/2015/02/1352126739_7909.jpg)


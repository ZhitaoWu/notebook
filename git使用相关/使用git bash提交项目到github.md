# 使用git bash提交项目到github

## 一、准备工作

**git **的工具安装这就先省略了，以下是讲述如何使用 **git hash **提交项目到 **github** 上。

由于**本地仓库**和**github远程仓库**是根据**ssh加密传输**的，所以要先建立起两者之间的通信协议。

* **第一步：创建ssh key。**

  * 1.1.1 一般先查看自己用户目录下是否有**.ssh**文件夹(路径如下)

  * ```
    C:\Users\Administrator\.ssh
    ```

  * 1.1.2 查看该目录下是否有 **id_rsa** 和 **id_rsa.pub** 两个文件(私钥和公钥)

  * ![image-20201216111705146](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201216111705146.png)

  * 1.2.1 该.ssh文件夹下没有这两个文件的话，就需要自己创建ssh key

  * ```
    $ ssh-keygen -t rsa -C "1843781561@qq.com"
    ```

  * 邮箱是github账户绑定的邮箱。一直默认确定下就会在 **.ssh** 目录下看到 1.1.2 的截图标记文件。

* **第二步：登录github**，**点击右上角的头像icon** -> **settings** -> **SSH and GPG keys**

  * 如果之前在其他 PC 端上创建过 **SSH key**，要在新的PC上与远程仓库建立通信连接，就需要 **NEW SSH KEY**
  * ![image-20201216113628446](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201216113628446.png)
  * 填上自己的 **title**(这个随意填写)，**key**就要复制之前创建好的 **id_rsa.pub** (公钥)的内容告知**远程仓库**(github)。在最后 **Add SSH key** 点击添加ssh key。
  * 生成成功就会跳转到上一个界面，显示你创建成功的ssh key
  * ![image-20201216114146243](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201216114146243.png)

* **第三步：创建远程仓库**

  * 点击头像icon旁边的 **+** -> **New repository** ，创建新的远程仓库
  * ![image-20201216115647873](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201216115647873.png)

  * 接下来就是对远程仓库的一些简单信息配置
  * ![image-20201216120704580](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201216120704580.png)

  *  这里我写了一个 **testRep** 作为该远程仓库命名，创建成功如下
  * ![image-20201216122853824](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201216122853824.png)

## 二、本地仓库实操

**git bash实操指令(上图也有)：**

* 先在本地创建一个英文命名的空文件夹，右击启用 **git bash**
  
  * ![image-20201216123947942](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201216123947942.png)
  
* **git init**                                          // 初始化本地仓库
  * 该文件夹下会出现一个.git的隐藏文件
  * ![image-20201216124443348](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201216124443348.png)

* **git add <文件夹/文件>**               // 添加文件或者资源到暂存区

* **git commit -m "提示信息文本"** // 提交文件或资源并备注提交信息
  
* ![image-20201216140315241](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201216140315241.png)
  
* **与远程仓库建立连接**
  * **git remote add origin git@github.com:ZhitaoWu/testRep.git**       // 默认协议：git@...。这里ZhitaoWu/testRep.git分别是个人的git账户和仓库名.git。如果要上传个人的要改成自己对应的信息。
  * **git remote add origin https://github.com/ZhitaoWU/testRep.git**   // https协议

* **git branch -M main**                   // 规避种族歧视 master 弃用，转而使用main作为主分支
  
* ![image-20201216140742238](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201216140742238.png)
  
* **git push -u origin main**            // 将本地仓库中的项目提交到git仓库中

  * ![image-20201216140824562](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201216140824562.png)

  * 之前我都是用 **https** 协议连接的，所以为了展示这次采用 **git** 协议上传。第一次使用 **push** 或者 **clone** 会出现 **RSA key** 的警告提示(警告文本如下)

    * ```
      The authenticity of host 'github.com (13.229.188.59)' can't be established.
      RSA key fingerprint is SHA256:nThbg6kXUpJWGl7E1IGOCspRomTxdCARLviKw6E5SY8.
      Are you sure you want to continue connecting (yes/no/[fingerprint])?
      ```

  * ![image-20201216141320767](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201216141320767.png)

  * 由于**git使用SSH连接**，而SSH连接在**第一次验证**GitHub服务器的key时，需要确认github的key的指纹信息是否真的来自github的服务器。这时候，可在问号后输入 **yes** 并回车即可。

  * 在上述操作之后，会出现一个 **warning** 警告。(文本如下)

    * ```
      Warning: Permanently added 'github.com,13.229.188.59' (RSA) to the list of known hosts.
      ```

    * 该警告是提示该 **RSA** 已经加入主机 **hosts** 的信任列表中了。

  * 最后就是上传到 **github** 的远程仓库中了。

    * ![image-20201216142401446](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201216142401446.png)

## 三、github远程仓库一些微调

* 现在有个历史遗留的小问题：刚刚远程仓库的命名是 testRep
* ![image-20201216144236195](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201216144236195.png)
  
* 进入要更改的项目(testRep) **Settings** 中修改
  
  * ![image-20201216144538960](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201216144538960.png)
  
* 修改成功会跳转到该远程仓库主页
  
  * ![image-20201216144629806](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201216144629806.png)
* 添加单个文件：readme.md

    * ![image-20201216145928728](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201216145928728.png)
  * 连接远程仓库那步没必要，本地已经 **hosts** 记载信任名单了，那一步忽略。
  * 查看远程仓库是否添加成功
  * ![image-20201216150313020](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201216150313020.png)

## 四、常见问题：

1. 添加文件时，报出的**warning: LF will be replaced by CRLF in** 

* 缘由是存在符号转义问题：
  * windows中的换行符为 CRLF， 而在linux下的换行符为LF，所以在执行add 时出现提示
  * 解决办法：**git config --global core.autocrlf false**

2. 其他问题或者使用方法，下次有遇见或者使用到再另外起一个篇幅更新。
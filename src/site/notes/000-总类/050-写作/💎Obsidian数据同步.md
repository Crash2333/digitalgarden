---
{"dg-publish":true,"permalink":"/000-总类/050-写作/💎Obsidian数据同步/","tags":["Obsidian/Syntax"],"noteIcon":""}
---

# Obsidian『windows和Android』数据同步
这篇是原稿，没怎么润色。感兴趣的直接点下面链接进行了解。
[用 Git 在 Android 和 Windows 间同步 Obsidian 数据库 - 少数派](https://sspai.com/post/68989)
## 前言
少数派的编辑问我为什么选择 git 作为 Android 端同步 Obsidian 的方式，一下子把我问倒了。
这个问题我想了一下午，总结了下面几点供大家参考
### Git的优点
- 目前世界上最先进的分布式版本控制系统（没有之一）
- 它是开源的（安全性有保证）
- 它是免费的
- 支持团队协同编辑文档、代码
- 多平台支持（[Gitee](https://gitee.com/)、[GitHub](https://github.com/)、[GitLab](https://about.gitlab.com/)、[CODING](https://coding.net/products/repo)）
- 它可以多端（Windows、MacOs、Adnroid、IOS、Linux）同步文档数据（不限于文档）
### Git的缺点
- 有一定的学习成本，对纯新手不友好
- 多设备修改，容易产生冲突
- 需要手动备份存档，如果忘了就没法找回历史版本


我选择Git，仅仅是因为它是我最常用、最熟悉的数据同步和备份的方式而已。作为一名开发人员，我真的想不到比它更好用的同步方式了。
如果你不了解Git，那么本文食用起来会比较困难。
[点这里了解，Git教程 - 廖雪峰的官方网站](https://www.liaoxuefeng.com/wiki/896043488029600)


## Windows准备工作
### 安装Git
>请按照[安装Git - 廖雪峰的官方网站](https://www.liaoxuefeng.com/wiki/896043488029600/896067074338496)这篇教程在你的PC上安装Git之后再食用下面的内容
>如果你已经安装了，那么你可以跳过这一步
### Gitee
- [点这里进官网注册 - Gitee.com](https://gitee.com/)
- 在Gitee里面创建“远程仓库”

![](https://i0.hdslb.com/bfs/album/287a79274b9933fe568d49093cdc4522f177bc89.png@1e_1c.webp)
### sshKey生成
> 1.  在目标路径下创建一个空白的txt（后缀为".txt"）文档
> 2.  将下面的代码复制粘贴到上面的空白文档中并**保存**
> 3.  修改用户名和邮箱
> 4.  修改文档后缀为”.sh“并保存
> 5.  双击修改后的".sh"文档执行脚本


```shell
#
titleLeft="【"
titleRight="】"
splitLine="====================================================="
#用户名
userName="这里改成你的用户名"
#邮箱
email="这里改成你的Email"
#模块项目名
projectName="ObsidianRepositorys"
#echo 域名：${titleLeft}${domain}${titleRight}
echo 用户名：${titleLeft}${userName}${titleRight}
echo 邮箱：${titleLeft}${email}${titleRight}
echo PS：用户名非本人时，请将脚本中的userName和email修改为本人

#配置git用户名和邮箱
git config --global  user.name ${userName}
git config --global user.email ${email}
git config --global  --list 
echo "无需设置密码，直接点击enter或者y键确认即可"
ssh-keygen -t rsa -C "${email}"

echo "copy下面的公钥添加到远程仓库"
#打印公钥
echo ${splitLine}
cat ~/.ssh/id_rsa.pub
echo ${splitLine}
#执行完毕之后不自动关闭窗口
echo 按任意键退出
read -n 1
echo 继续运行
```

>如果你本地之前生成过sshKey，那么脚本会提示你是否覆盖。输入“y”即可
>后续还会让你输入密码等参数，这里为了方便。建议大家直接回车不设置参数，当然你也可以设置参数后回车。
>脚本执行完后，将分割线里面的内容复制出来保存好。后面会用到。
>PS：如果手残，不小心关掉了脚本窗口。不要慌，双击“.sh”文件重新执行脚本即可。
![](https://i0.hdslb.com/bfs/album/edbbc7280220c8a7e6ac52e2f1a46fb02d8a4119.png@1e_1c.webp)

### 上传sshKey
1. 登陆Gitee
2. 点击右上角“头像”，进入设置页面
![](https://i0.hdslb.com/bfs/album/ab50a0847c7ba262069b0e3902b10c8a81e2a127.png@1e_1c.webp)
3. **点击左边导航栏的"SSH公钥"**

![](https://i0.hdslb.com/bfs/album/2c24ace0f56946ffaecd3f897624ca5d4539af2b.png@1e_1c.webp)
4. 填写完之后，点击确认即可

### 创建本地仓库
>根据Gitee网页提示创建本地仓库

![](https://i0.hdslb.com/bfs/album/dd39d3feb79c8e1358bf17348fbfce234bc9d8f6.png@1e_1c.webp)

### 上传Obsidian工作空间
>将整个Obsidian工作空间目录下的所有文件都放到本地仓库里面
>效果参考下面截图

![](https://i0.hdslb.com/bfs/album/5c26b7fd1f6566ae4a064090dc830ac612072c50.png@1e_1c.webp)
![](https://i0.hdslb.com/bfs/album/c331d07ecbaa0a355b021cbee6fe052473e65402.png@1e_1c.webp)
#### 安装GitKraken
>[https://www.aliyundrive.com/s/MrTRdAjd2h2](https://www.aliyundrive.com/s/MrTRdAjd2h2)
>6.5.1安装完之后不要打开软件，打开安装目录。
>删除下面目录中的**update.exe**文件
>```
>C:\Users\lenovo\AppData\Local\gitkraken
>```
>使用下面路径的中的**gitkraken.exe**，作为快捷方式启动程序
>```
>C:\Users\lenovo\AppData\Local\gitkraken\app-6.5.1
>```
>使用GitKraken打开本地仓库，**提交、推送**即可
>到目前为止，Windows上的准备工作都做完了

![](https://i0.hdslb.com/bfs/album/8ae1fc2d799631cb9570b01769577547721e4cc6.png@1e_1c.webp)
## Android准备
>安装**MGit**客户端app
>安装**Obsidian**客户端app
>[https://wwa.lanzoui.com/b010t9vef](https://wwa.lanzoui.com/b010t9vef)  
密码:2yfq

1.  进入设置页面，配置远程仓库下手机的下载路径
2. 进入设置页面，点击**管理SSHKEY**
3. 点击右上角的“+”生成sshKey
4. 进入生成的文件，点击右上角的**复制**按钮。复制sshKey
5. 参考前面的方法上传到Gitee
6. 从Gitee复制ssh链接，填入远程地址。点击克隆。
7. 成功之后，打开Obsidian。一般来说，Obsidian自动扫描到你克隆到手机的工作空间。如果没有扫描到，那么你就手动从Obsidian进入**步骤1**中设置的路径。手动打开**工作空间**


![](https://i0.hdslb.com/bfs/album/7291633746068a805504cd545c3210a8daa7b60c.png@1e_1c.webp)

![](https://i0.hdslb.com/bfs/album/a8e7498d87b7f2397a413c1ec933923965f0e888.png@1e_1c.webp)

![](https://i0.hdslb.com/bfs/album/73cc9894bc35abacd6d3957a079a816ee7ade3bc.png@1e_1c.webp)

![](https://i0.hdslb.com/bfs/album/b9f888510e0368d251ecb76c6136f366bce5ab44.png@1e_1c.webp)

![](https://i0.hdslb.com/bfs/album/359ce7650bf46ada9b45093187cb0fba0b9415f8.png@1e_1c.webp)
## 同步成功
![](https://i0.hdslb.com/bfs/album/98c30a93c1a7dfe7bf52583e3706f697c1cda396.png@1e_1c.webp)
## 结语
>细心的朋友可能已经看出来了，就是Obsidian的工作空间在PC和手机上都是通用的。这方面要为Obsidian的开发团队点赞。
>个人不建议在手机端编辑文档，屏幕太小影响体验和发挥。手机端只负责查阅即可，编辑还是放到PC端比较好。
>如果大家有什么更好的建议，可以在评论区告诉我
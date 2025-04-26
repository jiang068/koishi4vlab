# koishi4vlab
面向vlab用户，用Napcat登录无头NTQQ，对接koishi的onebot适配器，打造封号概率几乎为零的、不易失效的、占用电脑端口的QQbot.
# 特性
### 1、napcat登录，不会被限制登录或者封号
### 2、koishi支持社区内容，但不多
### 3、onebot是常见机器人框架，有资料可供参考
### 4、(重要)占用电脑端端口！所以如果在其他地方用电脑(包括windows和linux)登录了，QQbot会被踢下线！
# 如何搭建？
## 一、你要有一个服务器或者虚拟机
用学号登录vlab.ustc.edu.cn，进入“虚拟机管理”——>“新虚拟机”创建一个虚拟机，建议选择Ubuntu22.04版本带桌面的，便于后续操作；    
或者你在外面买其他虚拟机、云服务器也行，随意.  
然后记得“sudo apt update”一下。
## 二、Napcat的安装和配置(原文档仓库：https://github.com/NapNeko/NapCatQQ)
### 1、安装NapCat.Installer - Linux一键使用脚本(支持Ubuntu 20+/Debian 10+/Centos9)：
    
    curl -o napcat.sh https://nclatest.znin.net/NapNeko/NapCat-Installer/main/script/install.sh && sudo bash napcat.sh
vlab的网可能会很慢，稍安勿躁。
### 2、登录你的QQbot
安装好之后在浏览器里去以下端口登录你用于机器人的的QQ:
    
    http://localhost:6099/webui
PS：token在哪里？新版直接默认为“napcat"，老版的在 webui.json 里：
    
    /opt/QQ/resources/app/app_launcher/napcat/config/webui.json
浏览器进入webui页面后，点击QRCode进行二维码登录。    
登录成功后，你的QQbot就以电脑端形式上线了！不要在其他电脑上登录你的QQbot，以免被踢下线。
之后点击进入网络配置。
### 3、给koishi留一个ws代理
在网络配置中，选择新建一个“WebSocket Client 配置”，将“启用”勾选，    
URL里填写
    
    ws://localhost:5140/onebot
消息格式选Array，其他都默认即可。    
配置完成后，点击“保存”即可生效。Napcat就准备就绪了。    
## 三、Koishi的安装和配置(原文档：https://koishi.chat/zh-CN/manual/starter/linux.html)
进入koishi的releases页面
    
    https://github.com/koishijs/koishi-desktop/releases
找到你服务器对应系统的zip包进行下载，比如我的是学校给的Ubuntu22.04, 就选择：
    
    koishi-desktop-linux-x64-版本号.zip
下载到本地后把文件发给你的虚拟机(也可以直接在虚拟机里下载，不过网速很慢), vlab自带文件传输功能，自己探索。    
文件传到虚拟机里之后，解压文件夹，双击“koi”可执行文件就开始运行了，不过没有可视化界面。    
前往

    http://localhost:5140/
即可打开koishi面板。如果打不开说明你没有启动koishi, 回去多双击koi文件试试。

## 四、将Koishi和Napcat对接
Koishi只是外面的一个框架，里面我用的是onebot。所以要先安装onebot。    
进入koishi配置端口

    http://localhost:5140/
左侧找到“插件市场”(形状是一片拼图)，搜索“adapter-onebot”，点击“添加”、“安装”。    
然后左侧找到“设置”，右上角找到“添加插件”(形状是一个插头)，搜索并添加“adapter-onebot”。    
进入“adapter-onebot”的配置页面。    

selfid填你刚刚在Napcat里登录的QQ号；    

token填你刚刚在Napcat里填的token；    

protocol选择“ws-reverse”；    

path填：/onebot    

其他的默认。    
填好后右上角点“保存”按钮，再点“启动”按钮，onebot适配器就成功启动了。    
## 五、添加功能
做完前面的一到四，你的QQbot已经安装好了。但是你发现它什么功能都没有。因为你要自己添加功能。    
功能都在“插件市场”添加，我就不一一说了。
## 六、记住几个端口
Napcat的端口是6099，配置页面是

    http://localhost:6099/webui
koishi的端口是5140，配置页面是

    http://localhost:5140
## 七、虚拟机开机的时候如何启动QQbot的所有服务？
### 1、启动Napcat
打开控制台，输入

    sudo napcat start 12345678(这里是你的QQbot账号)
### 2、启动koishi
找到你的koi文件双击即可

# ServerStatus-HostLoc： 

![GitHub](https://img.shields.io/github/license/mashape/apistatus.svg)

* ServerStatus-Toyo版是一个酷炫高逼格的云探针、云监控、服务器云监控、多服务器探针~
* 该云监控（云探针）是ServerStatus（ https://github.com/ToyoDAdoubi/ServerStatus-Toyo ）项目的优化/修改版。
* Web使用了hostloc上分享的皮肤，故此库名字为hostloc（https://www.hostloc.com/thread-494384-1-1.html ）
* 将一键脚本内的连接修正为本库。预防外联库失联

![screenshot](https://github.com/hao35954514/ServerStatus-HostLoc/blob/master/screenshot.jpg)

# 目录介绍：

* clients  客户端文件
* server   服务端文件
* service  系统服务文件
* web      网站文件  

# 更新说明：

* 2021.12.13, 添加无法连接的解决方法
* 2020.5.4, 修改样式，隐藏了 类型、服务器位置（均为用注释隐藏）
* 2020.5.4, 美化主题，效果见 https://github.com/stilleshan/ServerStatus
* 2017.10.12, 负载Load 优化，并且支持CentOS6系统
* 2017.10.10, 修改负载 Load 的值为：当前服务器上链接SSR等软件的IP总数(只要软件监听IPv6那么就能统计，例如SSH)
* 2017.04.30, 优化手机显示式样
* 2017.04.29, 去除主机名设定
* 2017.04.27, 增加一键部署脚本

# Web修改显示
* 只显示卡片-修改index.html
``` bash
<table class="table table-striped">
改为
<table class="table table-striped" style="display:none">
保存即可
```
* 如果需要将刷新显示到最下方
``` bash
将81行到103行整体剪贴到第41行的下方(在41行<body>末尾回车、然后粘贴保存即可)
```

# 安装教程：     

执行下面的代码下载并运行脚本。
``` bash
wget -N --no-check-certificate https://raw.githubusercontent.com/hao35954514/ServerStatus-HostLoc/master/status.sh && chmod +x status.sh
```
下载脚本后，根据需要安装客户端或者服务端：
``` bash
# 显示客户端管理菜单
bash status.sh c
 
# 显示服务端管理菜单
bash status.sh s
```
运行脚本后会出现脚本操作菜单，选择并输入` 1 `就会开始安装。

一开始会提示你输入 网站服务器的域名和端口，如果没有域名可以直接回车代表使用` 本机IP:8888`

## 简单步骤：

首先安装服务端，安装过程中会提示：

``` bash
是否由脚本自动配置HTTP服务(服务端的在线监控网站)[Y/n]
 
# 如果你不懂，那就直接回车，如果你想用其他的HTTP服务自己配置，那么请输入 n 并回车。
# 注意，当你曾经安装过 服务端，同时没有卸载Caddy(HTTP服务)，那么重新安装服务端的时候，请输入 n 并回车。
```

然后 添加或修改 初始示例的节点配置，注意用户名每个节点配置都不能重复，其他的参数都无所谓了。

然后安装客户端，根据提示填写 服务端的IP 和前面添加/修改 对应的 节点用户名和密码（用于和服务端验证），然后启动就好了，有问题请贴出 详细步骤+日志(如果有)联系我。

## 部分客户端无法与服务端通信的解决方式：

查看客户端日志可看到报错：

``` bash
Connecting...
Caught Exception: a bytes-like object is required, not 'str'
```
这是因为 客户端的Python版本 与 服务端的Python版本 有兼容性问题。如 服务端为 2.X 版本，客户端为 3.X 版本，则会出现这种问题。

将双方的Python版本都调整到 2.X 版本就能解决问题。

先卸载 Python 3.X 版本，然后安装 Python 2.X 版本。

然后 Python2.X 版本的运行方式可能会是 python2.X xxxx。这时你改下  /etc/init.d/status-server  or  /etc/init.d/status-client 中的执行命令即可。也可以直接 alias ?


# 使用说明：

进入下载脚本的目录并运行脚本：

``` bash
# 客户端管理菜单
./status.sh c
# 服务端管理菜单
./status.sh s
```

然后选择你要执行的选项即可。

``` bash
ServerStatus 一键安装管理脚本 [vx.x.x]
-- Toyo | doub.io/shell-jc3 --
 
0. 升级脚本
————————————
1. 安装 服务端
2. 卸载 服务端
————————————
3. 启动 服务端
4. 停止 服务端
5. 重启 服务端
————————————
6. 设置 服务端配置
7. 查看 服务端信息
8. 查看 服务端日志
————————————
9. 切换为 客户端菜单
 
当前状态: 服务端 已安装 并 已启动
 
请输入数字 [0-9]:
```
# 其他操作

### 客户端：

启动：service status-client start

停止：service status-client stop

重启：service status-client restart

查看状态：service status-client status

### 服务端：

启动：service status-server start

停止：service status-server stop

重启：service status-server restart

查看状态：service status-server status

### Caddy（HTTP服务）：

启动：service caddy start

停止：service caddy stop

重启：service caddy restart

查看状态：service caddy status

Caddy配置文件：/usr/local/caddy/caddy

默认脚本只能一开始安装的时候设置配置文件，更多的Caddy使用方法，可以前去搜索引擎学习

——————————————————————————————————————

安装目录：/usr/local/ServerStatus

网页文件：/usr/local/ServerStatus/web

配置文件：/usr/local/ServerStatus/server/config.json

客户端查看日志：tail -f tmp/serverstatus_client.log

服务端查看日志：tail -f /tmp/serverstatus_server.log

# 其他说明

网络实时流量单位为：G=GB/s，M=MB/s，K=KB/s

服务器总流量单位为：T=TB，G=GB，M=MB，K=KB

### CentOS7系统 负载显示异常的问题

CentOS7系统 默认可能没有安装 netstat 依赖，所以会造成IP检测(负载)出错，手动安装即可：
`yum install net-tools -y `

# 相关开源项目，感谢： 

* ServerStatus：https://github.com/BotoX/ServerStatus
* mojeda: https://github.com/mojeda 
* mojeda's ServerStatus: https://github.com/mojeda/ServerStatus
* BlueVM's project: http://www.lowendtalk.com/discussion/comment/169690#Comment_169690

- GitHub [stilleshan/ServerStatus](https://github.com/stilleshan/ServerStatus)
- Docker [stilleshan/serverstatus](https://hub.docker.com/r/stilleshan/serverstatus)
- 原版项目Github [ToyoDAdoubi/ServerStatus-Toyo](https://github.com/ToyoDAdoubi/ServerStatus-Toyo)
- Dockerfile参考 [cppla/ServerStatus](https://github.com/cppla/ServerStatus)

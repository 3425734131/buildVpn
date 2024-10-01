# 本文仅供学习参考,无任何盈利性质,不承担任何法律责任
# 本文仅供VPN技术的学习记录，请勿传播
# 如果有人看到本文章，请勿私自搭建进行违法犯罪行为
# 2022.02.23 目前经过其他同学尝试还是可以搭建成功的
### Vultr页面UI变了，但是丝毫不影响流程，这里就先不更新图片了，一样的不影响

# buildVpn 
### 图文教程搭建一个vpn


接下来我们就可以搭建VPN了。距离成功已经很近了。

首先如果我们是Windows系统需要下载一个软件（Mac 或 Linux不需要），Xshell或者SecureCRT。这里我用的是SecureCRT。
填写你的IP地址，用户名为root，点击链接，点击接受保存，输入你的密码，成功连接。

![第十四步](https://github.com/yukaiji/buildVpn/blob/master/image/20180307101823784.jpg)
![第十五步](https://github.com/yukaiji/buildVpn/blob/master/image/20180307101836775.jpg)

其次要设置编码格式，不然一会的中文会显示乱码。菜单栏 选项-会话选项-外观-字符编码-UTF8-确认。
关闭软件，重新连接（直接双击IP就可以了）。

![第十六步](https://github.com/yukaiji/buildVpn/blob/master/image/20180307101848327.jpg)

然后复制下面的一键部署管理脚本，粘贴到窗口中（鼠标右键一下即可粘贴）

CentOS6/Debian6/Ubuntu14 ShadowsocksR一键部署管理脚本(可以把下面命令按行拆开分步执行)：

wget --no-check-certificate https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocksR.sh

chmod +x shadowsocksR.sh

./shadowsocksR.sh 2>&1 | tee shadowsocksR.log

### 主脚本安装SSR：
第一步：设定密码，default 为默认密码

![第十六-1步](https://github.com/yukaiji/buildVpn/blob/master/image/new2.png)

第二步：设定端口，default 为随机生成默认端口
![第十六-2步](https://github.com/yukaiji/buildVpn/blob/master/image/new3.png)

第三步：设定加密方式，default 为默认加密方式
![第十六-3步](https://github.com/yukaiji/buildVpn/blob/master/image/new4.png)

第四步：设协议，default 为默认协议
![第十六-4步](https://github.com/yukaiji/buildVpn/blob/master/image/new1.png)

第五步：设定混淆方式，default 为默认混淆
![第十六-5步](https://github.com/yukaiji/buildVpn/blob/master/image/new5.png)

第六步：安任意键，回车开始进行安装，安装完成后自动启动
![第十六-6步](https://github.com/yukaiji/buildVpn/blob/master/image/new7.png)

当安装出现问题时，有可能是centOS中缺少相应c编译器，可以分别执行以下指令安装编译器后再安装SSR：

yum -y install gcc automake autoconf libtool make

yum -y install gcc-c++

最终：安装完成，展示你所设置的内容，可以按照链接信息进行连接(最近较严有可能被墙或者端口被封)
![第十六-7步](https://github.com/yukaiji/buildVpn/blob/master/image/new6.png)

安装过后如果想要修改，运行如下相关命令

启动：/etc/init.d/shadowsocks start

停止：/etc/init.d/shadowsocks stop

重启：/etc/init.d/shadowsocks restart

状态：/etc/init.d/shadowsocks status

配置文件路径：/etc/shadowsocks.json  修改文件用vi 或者 vim命令，使用方法百度

日志文件路径：/var/log/shadowsocks.log 

安装路径：/usr/local/shadowsocks/shadowsoks

卸载./shadowsocksR.sh uninstall



### 备用脚本安装SSR：（如果此时链接断了，重连后输入./ssr.sh 就可以进入下面安装操作，以后修改时也输入./ssr.sh）
备用脚本（上面的脚步不可用再输入这个）：

wget -N --no-check-certificate https://raw.githubusercontent.com/ToyoDAdoubi/doubi/master/ssr.sh && chmod +x ssr.sh && bash ssr.sh

如果在输入命令式提示wget:command not found，则表示没有wget工具，先输入下面指令进行安装，然后再部署管理脚本
yum -y install wget

第一步：选择1 

![第十七步](https://github.com/yukaiji/buildVpn/blob/master/image/20180307101902154.jpg)

第二步：直接默认即可。（理论上说是可以随便的，1 - 65535）

![第十八步](https://github.com/yukaiji/buildVpn/blob/master/image/20180307101913385.jpg)

第三步：设置密码

![第十九步](https://github.com/yukaiji/buildVpn/blob/master/image/20180307101927773.jpg)

第四步：加密方式，选择aes-128-cfb就可以

![第二十步](https://github.com/yukaiji/buildVpn/blob/master/image/20180307101937845.jpg)

第五步：协议插件，为了使SS也能够使用，这里选择origin

![第二十一步](https://github.com/yukaiji/buildVpn/blob/master/image/20180307101948387.jpg)

第六步：选择混淆plain

![第二十二步](https://github.com/yukaiji/buildVpn/blob/master/image/20180307101957836.jpg)

第七步：设置连接数量，默认回车即可。然后开始进行安装。

![第二十三步](https://github.com/yukaiji/buildVpn/blob/master/image/20180307102008416.jpg)

如果遇到输入项，问y还是n时，输入y 回车确认。

![第二十四步](https://github.com/yukaiji/buildVpn/blob/master/image/20180307102018140.jpg)

### 到此安装就完成了。可以通过客户端进行链接翻墙上网了。

![第二十五步](https://github.com/yukaiji/buildVpn/blob/master/image/2018030710205260.jpg)

如果SSR成功安装，但是不能正常启动，在centOS中主要原因是缺少python环境，利用以下指令进行安装

yum -y install python36

cd /usr/bin

ln -s python3 python

### 为了能够提高上网速度，YouTube从480 体验为1080。我们接下来进行安装加速软件（速锐、BBR两者选其一，不可共存）。

### BBR加速（如果需要速锐，跳过此段）

BBR加速特别简单，复制下面脚本代码即可。
谷歌BBR加速脚本：

第一个指令：wget --no-check-certificate https://github.com/teddysun/across/raw/master/bbr.sh

第二个指令：chmod +x bbr.sh

第三个指令：./bbr.sh

1、遇到停顿按回车即可。然后继续安装。（多等一会）

![第二十六步](https://github.com/yukaiji/buildVpn/blob/master/image/20180307102104748.jpg)

2、安装完成后问你是否重启，这里输入y，回车。

![第二十七步](https://github.com/yukaiji/buildVpn/blob/master/image/20180307102114503.jpg)

3、重新连接后，输入 lsmod | grep bbr 查看BBR是否启动，可以看到已经启动了。

![第二十八步](https://github.com/yukaiji/buildVpn/blob/master/image/20180307102126665.jpg)

### 备用脚本安装SS：
wget --no-check-certificate -O shadowsocks-all.sh https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks-all.sh

第一项选1 python安装，其他选择与主脚本描述一样


### 速锐加速
1、首先输入
uname -a 查看内核为

2、然后输入
cat /etc/redhat-release  查看系统版本

3、下载CentOS 6.6版本的内核（速锐支持6.6版本的）
wget http://ftp.scientificlinux.org/linux/scientific/6.6/x86_64/updates/security/kernel-2.6.32-504.3.3.el6.x86_64.rpm

4、安装内核
rpm -ivh kernel-2.6.32-504.3.3.el6.x86_64.rpm --force

5、重启服务器
reboot

6、安装速锐
wget -N --no-check-certificate https://raw.githubusercontent.com/91yun/serverspeeder/master/serverspeeder-all.sh && bash serverspeeder-all.sh

这时正常情况速锐就已经安装完成并且启动了。

![第二十九步](https://github.com/yukaiji/buildVpn/blob/master/image/20180307102140531.jpg)

service serverSpeeder status     查看速锐的状态
service serverSpeeder start | stop | restart  停止暂停重启锐速


### 到此为止，通过BBR或速锐加速的VPN服务器已经全部搭建完成了。

### 接下来使用SSR或者SS客户端连接即可

MAC：https://github.com/shadowsocksr-backup/ShadowsocksX-NG/releases
WIN：https://github.com/shadowsocksr-backup/shadowsocksr-csharp/releases
IPHONE：FirstWingy、potatso lite  （商店里有，实在找不到可以弄个美国APPLEID，什么都能下）

以iphone为例：首先右上角加号，添加服务器配置信息。

![第三十步](https://github.com/yukaiji/buildVpn/blob/master/image/20180307102153178.jpg)

然后：填写一开始安装时的信息,保存。如果忘了记得 ./ssr.sh  选择5 查看连接信息

![第三十一步](https://github.com/yukaiji/buildVpn/blob/master/image/20180307102204995.jpg)

这时你可以愉快的翻墙上网了。

![第三十二步](https://github.com/yukaiji/buildVpn/blob/master/image/20180307102258394.jpg)

### 如果使用SSR无法连接网络，则可能是centOS未开放相关端口，接下来查询并开启端口

./ssr.sh 选择5 查看配置信息中的端口号

假如我们使用的是2333端口

用以下指令可以查看是否开启对应端口

firewall-cmd --list-ports

![第三十三步](https://github.com/MaxwellHawk/buildVpn/blob/master/image/port.png)

如果没有出现2333/tcp的字样，那么该端口还没有开放。使用以下命令开放相应端口并重启：

firewall-cmd --zone=public --add-port=2333/tcp --permanent

reboot

等待1分钟左右，端口已开放，SSR可以连接

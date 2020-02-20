# 搭建v2ray科学上网教程 (vmess+ws+tls)

## 准备工作

1. 购买服务器

   这里推荐阿里云[^温馨提示] 的香港服务器，价格便宜，每月24RMB，对于学生党很友好，得益于香港的地理位置，延迟很低，网速也可以接受，总体上网络体验不错。

2. 购买域名并解析

   阿里爸爸的万网下，可以申请.xyz的域名，一年6RMB，经济实惠，并用自带的DNS解析[^时间]到所购买的IP下。

[^温馨提示]: 在阿里爸爸下，你是实名认证的，所以科学上网请低调，自己偷偷着用就好了，别搭机场，出了事情一律后果自负~
[^时间]: 阿里云上免费版本的一般需要10分钟生效，可以在cmd中ping一下自己的域名看看IP是否已经成功解析

## 部署服务器

1. 更新系统

   `sudo apt-get update`

   `sudo apt-get upgrade`

2. 运行一键部署脚本

   ```
wget -N --no-check-certificate -q -O install.sh "https://raw.githubusercontent.com/paniy/V2Ray_ws-tls_bash_onekey/master/install.sh" && chmod +x install.sh && bash install.sh
   ```
   
   其间只要核对时间与输入域名,然后静静等待，一般需要十几分钟，完成后用客户端连接试一试是否能成功的连接。
   
3. 安装BBR-PLUS加速

   ``` 
   wget -N --no-check-certificate "https://raw.githubusercontent.com/chiakge/Linux-NetSpeed/master/tcp.sh" && chmod +x tcp.sh && ./tcp.sh
   ```

   先选择更换BBR-PLUS的内核，然后重启服务器后再次运行脚本，选择启动BBR-PLUS，就OK了。

## 玄学优化

1. 更换服务器 DNS

   ​		`vi /etc/resolvconf/resolv.conf.d/base` (这个文件默认是空)

   按 i 进入编辑模式，添加下面两行代码进去

   ```
   nameserver 8.8.8.8
   nameserver 8.8.4.4
   ```

   然后按 esc 退出后，输入`:wq` 保存并退出

   执行更新：`resolvconf -u`

2. 修改反向代理地址(非必须，强迫症患者使用)

   在`nginx/conf/conf.d` 下，把`www.idleleo.com`修改成任何想要网址，比如`www.baidu.com` ,只要是人畜无害的网址就行。


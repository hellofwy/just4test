使用`ssh`的tcp_forword功能。现在linux下ssh使用比较广泛的是openssh包

###ssh相关选项：###
* `-V`  
显示版本：
`ssh -V`
`OpenSSH_6.6.1p1 Ubuntu-2ubuntu2, OpenSSL 1.0.1f 6 Jan 2014`

* `-f`   
输入密码后进入后台模式(Requests ssh to go to background just before command execution.)  

* `-N`   
不执行远程命令,用于端口转发( Do not execute a remote command.  This is useful for just for warding ports (protocol version 2 only).)  

* `-D`  
socket5代理(Specifies a local “dynamic” application-level port forwarding.Currently the SOCKS4 and SOCKS5 protocols are supported, and ssh will act as a SOCKS server.)  

* `-L`  
tcp转发(Specifies that the given port on the local (client) host is to be forwarded to the given host and port on the remote side.)

* `-C`   
使用数据压缩,网速快时会影响速度(Compression is desirable on modem lines and other slow connections, but will only slow down things on fast networks.The compression algorithm is the same used by gzip)  

###建立SOCKS5代理:###
`ssh -f -N -D bindaddress:port name@server`  
* bindaddress： 指定绑定ip地址  
* port： 指定侦听端口  
* name： ssh服务器登录名  
* server： ssh服务器地址  

**例：**
`ssh -f -N -D 127.0.0.1:1080 xiaoming@158.123.45.37`  
这样就建立SOCKS5代理。  

###使用SOCKS5代理###
**例：**
* **chrome：**
chrome需要使用命令指定SOCKS5代理：  
`google-chrome --proxy-server="socks://127.0.0.1:1080"`  

* **firefox:**  
在preferences=>advanced=>Network->connection->Settings里，勾选Manual proxy configuration，并将其它项清空，SOCKS Host设置为127.0.0.1，port设置为1080， 并勾选Remote DNS（勾选后可防止本地DNS污染），如图。  
![firefox socks config][1]
* **其它，请搜索具体关于各自配置的文章：**
 + 使用代理插件switchysharp等  
 + 在系统自带的代理设置全局代理  
 + 使用其它SOCKS客户端实现代理，比如redsocks  

###参考###
* [SSH隧道与端口转发及内网穿透][2]
* [OpenSSH官网][3]


  [1]: http://static.oschina.net/uploads/space/2014/1107/174131_xrw4_1382972.png
  [2]: http://blog.creke.net/722.html
  [3]: http://www.openssh.com/

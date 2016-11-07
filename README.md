# linetest.rtc.io

本stun client运行方式：
1、在web容器中运行，依托于apche或nginx等容器运行。然后在浏览器中打开。
譬如，apche安装在D:\apache\，访问端口设置为8080，然后将本项目代码下载后解压到apache的文件访问目录下(D:\apache\htdocs\linetest)。
本机通过localhost:8080/linetest访问项目。
2、运行依托于本机环境。需要安装python和node.js。同时信令服务器部署在国外的，linetest.rtc.io，因此要正常访问，本机需要翻墙（搜索“蓝灯”）。
另外stun server，如果采用国外的，也是需要翻墙的。这里也有开源的stunman，可自行下载部署在公网环境下：http://www.stunprotocol.org/ 。
3、启动测试方式：
<p>========================================</p>
<p>Usage:</p>
<p>1. open this page in browser . Then click the button "create room" .</p>
<p>2. copy the "test url" on the page and open it in any browser.</p>
<p>========================================</p>



----------------------------------------------------------------------------------------
以下是stun server(stunman)的安装及运行方法：

1. tar  xvfz stunserver.xxx

2.  yum install -y boost-devl   （编译需要使用boost）
(如果不用yum安装，就手动下载boost: 
下载地址：http://www.boost.org/users/history/version_1_62_0.html
安装：
（1）./bootstrap.sh
（2）./bjam  install  )

3. cd ./stunserver

4. make 
如果error为找不到 boost 
更改common.inc  看BOOST_INCLUDE 是都被注掉，引用路径是否正确
更改完后 makeclean,
make 
make 成功后回生产 stunserver,stunclient等二进制文件（这里的stunclient只能用于做nat类型检测）

5. 启动   默认端口号 3478
nohup ./stunserver --altport [端口号] > output 2>&1   （这里使用默认端口，--altport参数不填）

6. NAT检测：./stunclient --mode basic --localport 7777 stun.sipgate.net

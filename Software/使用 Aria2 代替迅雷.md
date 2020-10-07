# 使用 Aria2 代替迅雷

## 一、原因

* 迅雷下载速度一般，thunder:// 开头的链接也逐渐被 bt 链接替代。
* 迅雷很流氓，安装后 (尤其是 Windows 系统) 浏览器默认使用迅雷下载，对于小文件来说使用浏览器内置下载可能更快。

## 二、安装

1. 如果是 **Linux/MacOS** 系统，使用**命令行**安装 Aria2 (本文之后以 Deepin Linux 说明)

   ```bash
   sudo apt install aria2 -y  	# Debian/Ubuntu/Deepin
   brew install aria2 -y		# MacOS
   ```

   如果是 **Windows**　系统，进入 <a href="https://github.com/aria2/aria2/releases/tag/release-1.35.0">Aria2 的 GitHub Release</a> 下载

   [![Download Aria2c](https://s1.ax1x.com/2020/10/07/0dHDAI.md.png)](https://imgchr.com/i/0dHDAI)

2. 配置

   ```bash
   sudo mkdir /etc/aria2
   sudo touch /etc/aria2/aria2.session
   sudo chmod 777 /etc/aria2/aria2.session
   sudo vi /etc/aria2/aria2.conf
   ```

   编辑 */etc/aria2/aria2.conf*

   ```bash
   #dir="YOUR/DOWNLOAD/DIRECTORY"
   disable-ipv6=true
   enable-rpc=true
   rpc-allow-origin-all=true
   rpc-listen-all=true
   continue=true
   ```

   测试 Aria2 安装是否成功

   ```bash
   sudo aria2c --conf-path=/etc/aria2/aria2.conf
   ```

   如果无错误提示即为成功，Ctrl+C 停止运行
   
3. 设置 Aria2 开机启动

   ```bash
   sudo vi /etc/init.d/aria2c
   ```

   添加如下内容：

   ```bash
   #!/bin/sh
   ### BEGIN INIT INFO
   # Provides: aria2
   # Required-Start: $remote_fs $network
   # Required-Stop: $remote_fs $network
   # Default-Start: 2 3 4 5
   # Default-Stop: 0 1 6
   # Short-Description: Aria2 Downloader
   ### END INIT INFO
    
   case "$1" in
   start)
    
    echo -n "已开启Aria2c"
    sudo aria2c --conf-path=/etc/aria2/aria2.conf -D
   ;;
   stop)
    
    echo -n "已关闭Aria2c"
    killall aria2c
   ;;
   restart)
    
    killall aria2c
    sudo aria2c --conf-path=/etc/aria2/aria2.conf -D
   ;;
   esac
   exit
   ```

   保存文件，然后执行以下命令

   ```bash
   sudo chmod 755 /etc/init.d/aria2c
   sudo update-rc.d aria2c defaults
   sudo service aria2c start
   ```

   查看服务状态：

   ```bash
   sudo systemctl status aria2c
   ```

   

## 三、浏览器集成（以 Chrome 浏览器为例）

1. 进入这个网站：<a href="https://chrome.google.com/webstore/detail/aria2-for-chrome/mpkodccbngfoacfalldjimigbofkhgjn">戳这里</a>（国内用户确保能访问 google.com）

2. 安装插件

3. Enjoy~

   这是一张配置完成的图片：

   ![0dL9XD.png](https://s1.ax1x.com/2020/10/07/0dL9XD.png)

   
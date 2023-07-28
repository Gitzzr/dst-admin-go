
脚本可能不适用于CentOS 8系统。在CentOS 8上安装Don't Starve Together服务器需要进行一些调整。

你可以尝试以下步骤来在CentOS 8上安装DST服务器：

1. 更新系统软件包：
   ```
   sudo dnf update
   ```

2. 安装所需的依赖库和工具：
   ```
   sudo dnf install -y glibc.i686 libstdc++.i686 libcurl.i686 screen
   ```

3. 创建steamcmd目录并下载SteamCMD安装文件：
   ```
   mkdir ~/steamcmd
   cd ~/steamcmd
   wget https://steamcdn-a.akamaihd.net/client/installer/steamcmd_linux.tar.gz
   ```

4. 解压SteamCMD安装文件：
   ```
   tar -xvzf steamcmd_linux.tar.gz
   ```

5. 使用SteamCMD安装和更新DST服务器：
   ```
   ./steamcmd.sh +login anonymous +force_install_dir ~/dst-dedicated-server +app_update 343050 validate +quit
   ```

6. 复制32位的libstdc++.so.6文件到DST服务器的bin/lib32目录下：
   ```
   cp ~/steamcmd/linux32/libstdc++.so.6 ~/dst-dedicated-server/bin/lib32/
   ```

7. 创建用于存储服务器配置文件的目录：
   ```
   mkdir -p ~/.klei/DoNotStarveTogether/MyDediServer
   ```

请注意，在执行以上步骤之前，请确保你具有管理员或root权限，并且在执行脚本时仔细检查和备份你的数据。

CentOS 已经停止维护的问题。2020 年 12 月 8 号，CentOS 官方宣布了停止维护 CentOS Linux 的计划，并推出了 CentOS Stream 项目，CentOS Linux 8 作为 RHEL 8 的复刻版本，生命周期缩短，于 2021 年 12 月 31 日停止更新并停止维护（EOL），更多的信息可以查看 CentOS 官方公告。如果需要更新 CentOS，需要将镜像从 mirror.centos.org 更改为 vault.centos.org
🥎那么针对上面提到的第二种情况，给出的解决方法如下：
参考连接：https://blog.csdn.net/Ceiee/article/details/127189579

🔔 首先，进入到 yum 的 repos 目录
```
cd /etc/yum.repos.d/
```

🔔其次，修改 centos 文件内容
```
sed -i 's/mirrorlist/#mirrorlist/g' /etc/yum.repos.d/CentOS-*
sed -i 's|#baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g' /etc/yum.repos.d/CentOS-*
```

🔔 然后，生成缓存更新（第一次更新，速度稍微有点慢，耐心等待两分钟左右）
```
yum makecache
```

🔔 最后，运行 yum update 并重新安装依赖
```
yum update -y
```

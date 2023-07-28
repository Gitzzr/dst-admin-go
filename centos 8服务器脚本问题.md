
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

# Minecraft建服

选择CentOS系linux，比如阿里云默认的Alibaba Cloud Linux。

包管理器可选yum或dnf。CentOS8中，yum已被dnf取代。

### 1 ssh连接服务器

使用root账户登录

```
sudo ssh 47.113.222.186
```

### 2 常用工具安装

```
dnf -y install vim lrzsz lsof wget zip unzip tar screen vsftpd
```

### 3  JAVA运行环境安装

尝试搜索 java-17，得到程序包名 java-17-openjdk

```
dnf search java-17
```

安装OpenJDK 17

```
dnf -y install java-17-openjdk
```

验证安装是否成功

```
java -version
```

### 4 Minecraft Server 下载

右键复制.jar下载链接

```
https://www.minecraft.net/zh-hans/download/server
```

在服务器中新建文件夹，并下载

```
mkdir minecraft
cd minecraft/
curl -O https://piston-data.mojang.com/v1/objects/c9df48efed58511cdd0213c56b9013a7b5c9ac1f/server.jar
```

重命名

```
mv server.jar minecraft_server.1.19.3.jar
```

### 5 导入地图数据

若创建新地图则跳过该步骤

解除root不能使用fpt的权限

```
cd /etc/vsftpd
vim user_list	#删除root
vim ftpusers	#删除root
```

启动ftp服务

```
service vsftpd start
```

查看ftp服务

```
service vsftpd status
```

如FileZilla报错Server sent passive reply with unroutable address. Using server address instead，则将transfer mode改为Active（主动模式）。

### 6 启动服务器

启动前同意许可证

```
vim eula.txt
```

将文件中的 ```eula=false``` 改为 ```eula=true```，保存文件

新建窗口

```
screen -R minecraft
```

在新窗口中输入启动命令

```
java -Xmx1024M -Xms1024M -jar minecraft_server.1.19.3.jar nogui
```

当服务器返回 Done (x.xxxs)! For help, type "help” 的信息后，即代表服务器创建完成

使用ctrl+a，然后输入d，挂起当前窗口

列出当前所有的会话

```
screen -ls
```

重新连接会话

```
screen -r <session id>
```

退出窗口

```
screen -d <session id>
```

清除窗口

```
screen -wipe <session id>
```


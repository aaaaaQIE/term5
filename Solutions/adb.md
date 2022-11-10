# adb常用命令

### ```adb```

```devices``` ：查看手机是否已经连接，成功连接会显示设备序列号

```connect <ip>``` ：连接到局域网设备

```disconnect <ip>``` ：断开连接局域网设备。单独输入 ```adb disconnect``` 可断开所有设备

```install <example.apk>``` ：安装软件进手机

```shell dumpsys battery``` ：查看电池电量的相关信息

```shell dumpsys wifi``` ：查看无线网络相关信息

```shell dumpsys cpuinfo``` ：查看当前系统CPU使用情况

```shell dumpsys meminfo``` ：查看内存使用情况

```shell top``` ：查看进程占用情况

```push "local file" "remote directory"``` ：将电脑文件上传到手机中

```pull "remote file" "local directory"``` ：将手机文件下载到电脑中

# 实例：

### 1、华为无线调试：

华为没有自带的无线调试开关，连接会出现：

```
cannot connect to 192.168.1.101:5555: 由于目标计算机积极拒绝，无法连接。 (10061)
```

1. 先用USB线连接手机和电脑

2. 打开开发者模式，勾选USB调试，和“仅充电”模式下允许ADB调试

3. 打开终端输入 ```adb devices``` 

   若出现类似：

   ```
   List of devices attached
   CMBNW20526001488		device
   ```

   说明USB线连接成功

4. 输入 ```adb tcpip 5555``` （这个是从usb模式切换到无线连接，后面的5555为端口，可以指定其他的端口，前提是端口未被调用）

5. 输入 ```adb connect 192.168.***.***:5555``` （ ```192.168.***.***``` 为你手机的ip地址，5555为刚才设置的端口号）

   若出现类似：

   ```
   List of devices attached
   CMBNW20526001488		device
   192.168.1.101:5555		device
   ```

   说明无线连接成功，这时可以拔下数据线了。在手机未被路由器重新分配ip之前连接就都无需数据线了，可以直接无线调试。

   
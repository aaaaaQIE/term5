# Cent OS添加虚拟内存

### 1、先删除swap分区：

```
swapoff -a
```

### 2、创建swap分区的文件：

```
dd if=/dev/zero of=/root/swapfile bs=1M count=2048
```

一般的建议是，小于2G内存，swap分区建议是内存的2倍，大于2g的内存，跟内存等倍即可。

其中 bs是每块的大小，count是块的数量，bs\*count，就是swap文件的大小了，这里就是1M\*2048=2G。大家可以自己调整count的数量。

此外， ```/root/swapfile``` 是swap文件的路径，可以根据需求修改。

### 3、格式化交换分区文件：

```
mkswap /root/swapfile
```

这里的路径和之前的路径要对应起来。

### 4、启用swap分区文件：

```
swapon /root/swapfile
```

### 5、添加开机启动：

修改 ```/etc/fstab``` 这个文件，添加或者修改这一行：

```
/root/swapfile	swap	swap	defaults	0 0
```

注意，路径还是要对应。最后两个是零，不是字母o。

### 6、修改 ```/root/swapfile``` 权限：

这个文件权限是0644，除了“所有者”外，“用户组”和“公共”都有读取权限（不安全），建议创建swap文件时仅保留“所有者”的读写权限，关闭其他所有用户的权限，也就是设置为0600（0600也是广大主机商的默认做法）

```
chmod 0600 /root/swapfile
```

好了，重启机器之后可以再看一下swap的大小了
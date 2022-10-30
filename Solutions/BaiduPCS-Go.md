# BaiduPCS-Go常用命令

#### ```baidupcs```

```login -bduss=<BDUSS>``` ：使用百度 BDUSS 来登录百度帐号。在浏览器F12的cookies里找，或者用edit this cookie。

```loglist``` ：列出帐号列表

```who``` ：获取当前帐号

```su <uid>``` ：切换已登录账号

```logout``` ：退出当前账号

```quota``` ：获取网盘储存空间配额

```d <file or dir 1> <file or dir 2> ...``` ：下载文件/目录。下载网盘内所有文件：```d /```

```config set -savedir <savedir>``` ：自定义下载文件夹

```--mode <value>``` ：更改下载模式。可选值： ```pcs, stream, locate``` ，默认为 ```locate```。

- ```pcs``` ：通过百度网盘的 PCS API 下载(不建议使用)
- ```stream``` ：通过百度网盘的 PCS API, 以流式文件的方式下载，效果同 ```pcs``` （不建议使用）
- ```locate``` ：默认的下载模式。从百度网盘 Android 客户端，获取下载链接的方式来下载


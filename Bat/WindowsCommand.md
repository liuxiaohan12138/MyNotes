---
title: windows命令行记录
---

# 命令

```
# 查看所有本地服务的端口号和进程号
netstat -ano

# 查看进程
tasklist

# 过滤 不区分大小写
findstr code /i

# 杀进程
taskkill /pid 进程号 /f

# 在windows下查看某个运行程序（或进程）的命令行参数
wmic process get caption,commandline /value

# 查询某一个进程的命令行参数
wmic process where caption="cmd.exe" get caption,commandline /value

# 复制文件夹
xcopy 源文件夹路径 目标文件夹路径 /e/h/i/y
```


# picom

## 目录

* ### [下载](#下载)

* ### [配置文件](#配置文件)

* ### [个人配置](#个人配置)

## 下载

在终端中使用如下代码下载picom混成器

```
sudo pacman -S picom
```

## 配置文件

> picom的配置文件路径应为：~/.config/picom.conf

如果首次下载picom并且目录中没有配置文件，在终端中执行如下命令创建配置文件：

```
mkdir ~/.config/picom.conf
```

我个人的配置文件GitHub路径：

```
https://github.com/pawnEkko/arch/blob/master/config/picom/picom.conf
```

在i3-wm的配置文件中加入如下代码，以确保开机启动

```
exec_always --no-startup-id picom -b
```
# ArchLinux 折腾日记

## 目录

* [git](#git)

* [feh](#feh)

* [picom](#picom)
* [rofi](#rofi)

* [Terminator](#Terminator)

* [声音](#声音)

* [科学上网](#科学上网)

* [zsh](#zsh)

## git

通过如下代码安装git（git为必装项目之后很多配置会用到）

```
sudo pacman -S git
#回车后直接回车全选下载
```

## feh

feh是壁纸软件，使用如下代码下载

```
sudo pacman -S feh
```

下载完成后在i3的配置文件中加入如下代码（个人已同步i3配置文件）

```
#每次开机启动后自动从路径中选择一张图片作为壁纸
exec_always --no-startup-id feh --randomize --bg-fill ~/Download/壁纸/*
# 路径填写自己对应的
```



## picom混成器

下载

```
sudo pacman -S picom
```

配置文件在本机的路径

```
sudo cp /etc/xdg/picom.conf .config/
```

个人配置文件在GitHub的路径：

```
https://github.com/pawnEkko/arch/blob/master/config/picom/picom.conf
```

在i3的配置文件中加入如下代码以启动（个人已同步i3配置文件）

```
exec_always --no-startup-id picom -b
```

## rofi

使用如下代码安装rofi

```
sodo pacman -S rofi
```

在i3的配置文件中做如下修改用以替换i3-wm原来的搜索

```
将原来的  bindsym $mod+d  代码段整体修改为：
bindsym $mod+d exec rofi -show drun
```

如果需要配置rofi的主题 按照如下方式进行操作

```
1.创建下载主题的文件夹：
2.进入文件夹下载主题（以下链接为个人使用的主题包可以自行到github寻找）
git clone https://github.com/lr-tech/rofi-themes-collection.git
3.创建安装主题的目录
mkdir -p ~/.local/share/rofi/themes/
4.使用如下代码将主题复制到程序可以选择的目录中
cp themes/<你选择的主题包> ~/.local/share/rofi/themes/
#下面这两段复制的主题是我使用的主题，复制两段是因为该主题是颜色文件调用格式文件的组合，两端都要复制
cp themes/rounded-common.rasi ~/.local/share/rofi/themes
cp themes/rounded-nord-dark.rasi ~/.local/share/rofi/themes
5.在终端输入如下代码进入rofi的主题选择界面选择完成后按回车确定并按Alt+a 保存
rofi-theme-selector
```

添加图标（如果需要的话），使用编辑器打开使用主题的rasi文件，加入如下代码

```
configuration{
	show-icons:true;
	/*drun-icon-theme:"图标主题包名称"*/   /*此行代码是用来使用已下载的图标主题*/   
}
```



## Terminator

terminator的配置文件路径为（个人配置已同步）

```
～/config/terminator/config
```



## 声音

用如下代码安装获取声音的软件

```
sudo pacman -S pipewire-pulse pipewire-alsa pipewire-jack
```

或者这些软件

```
sudo pacman -S alsa-utils pulseaudio pavucontrol
```



## 科学上网

> 经过本人实际使用，部分软件的下载与配置需要科学上网，所以这一步是必不可少的

* 使用如下代码安装 cfw //使用cfw只是因为比较简单 不一定是因为好用

```
yay -S clash-for-windows-bin
```

* 安装完成后 使用如下代码寻找clash内核

```
pacman -Ql clash-for-windows-bin
```

* 输入以上指令如果没有报错会出现目录，在其中寻找 以‘clash-linux’结尾的对应内核目录并复制
  然后使用如下代码格式开启tun

```
sudo setcap cap_net_admin=ep 目录
```

* 如上配置完成后打开cfw导入机场即可食用
  如果终端也要连接外网，须在终端配置文件中设置如下环境变量（已使用 zsh 即配置文件为.zshrc ）

```
export https_proxy=http://127.0.0.1:7890
export http_proxy=http://127.0.0.1:7890
export all_proxy=socks5://127.0.0.1:7890
```





## zsh

> zsh 是一个终端中的shell软件，用来代替linux默认的bash，以下是它的安装与配置方法

> 个人配置为 zsh + oh my zsh 插件+ PowerLevel10k 主题

> 配置文件为 ～/.zshrc  同步GitHub

### 安装并配置zsh

使用如下代码安装zsh 

```
sudo pacman -S zsh
```

安装完成后创建或者下载配置文件   //配置文件路径与配置文件名称应为（个人已同步配置）

```
~/.zshrc
```

终端中输入如下命令并输入密码将系统的bash替换为zsh

```
chsh -s /bin/zsh
```

### 安装插件

> oh my zsh 插件

如已翻墙使用如下代码安装或访问[oh my zsh官网](ohmyz.sh)：

```
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"   
```

如未翻墙使用如下[国内镜像](https://gitee.com/Devkings/oh_my_zsh_install?_from=gitee_search)（gitee）：

```
sh -c "$(curl -fsSL https://gitee.com/Devkings/oh_my_zsh_install/raw/master/install.sh)"
```

### 安装主题

> 我这里使用的是powerlevel10k的主题

如已翻墙使用如下代码

```
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ~/powerlevel10k
```

如未翻墙使用如下代码

```
git clone --depth=1 https://gitee.com/romkatv/powerlevel10k.git ~/powerlevel10k
```

安装完成后需要使用如下代码下载依赖的字体

```
yay -S ttf-meslo-nerd-font-powerlevel10k
```

安装完成后执行如下代码将主题应用到zsh（.zsh是zsh的配置文件）

```
echo 'source ~/powerlevel10k/powerlevel10k.zsh-theme' >>~/.zshrc
```

执行完成后执行如下代码或者重新打开终端就会进入主题配置页面

```
p10k configure
```

[picom](https://github.com/pawnEkko/arch/blob/master/note/picom.md)